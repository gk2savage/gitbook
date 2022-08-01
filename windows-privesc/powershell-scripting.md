# Powershell Scripting

Powershell is the Windows Scripting Language and shell environment that is built using the .NET framework.

This also allows Powershell to execute .NET functions directly from its shell. Most Powershell commands, called _cmdlets,_ are written in .NET. Unlike other scripting languages and shell environments, the output of these _cmdlets_ are objects - making Powershell somewhat object oriented. This also means that running cmdlets allows you to perform actions on the output object(which makes it convenient to pass output from one _cmdlet_ to another). The normal format of a _cmdlet_ is represented using **Verb-Noun**; for example the _cmdlet_ to list commands is called `Get-Command.`

Common verbs to use include:

* Get
* Start
* Stop&#x20;
* Read
* Write
* New
* Out

{% embed url="https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7" %}
