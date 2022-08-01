# Powershell Scripting

{% embed url="https://learnxinyminutes.com/docs/powershell/" %}

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

#### Using Get-Help

Get-Help displays information about a _cmdlet._ To get help about a particular command, run the following:

`Get-Help Command-Name`

You can also understand how exactly to use the command by passing in the `-examples` flag. This would return output like the following:&#x20;

![](https://i.imgur.com/U5Mlirh.png)

#### Using Get-Command

Get-Command gets all the _cmdlets_ installed on the current Computer. The great thing about this _cmdlet_ is that it allows for pattern matching like the following

`Get-Command Verb-*` or `Get-Command *-Noun`

Running `Get-Command New-*` to view all the _cmdlets_ for the verb new displays the following:&#x20;

![](https://i.imgur.com/KEzbPUI.png)

#### Object Manipulation

In the previous task, we saw how the output of every _cmdlet_ is an object. If we want to actually manipulate the output, we need to figure out a few things:

* passing output to other _cmdlets_
* using specific object _cmdlets_ to extract information

The Pipeline(|) is used to pass output from one _cmdlet_ to another. A major difference compared to other shells is that instead of passing text or string to the command after the pipe, powershell passes an object to the next cmdlet. Like every object in object oriented frameworks, an object will contain methods and properties. You can think of methods as functions that can be applied to output from the _cmdlet_ and you can think of properties as variables in the output from a cmdlet. To view these details, pass the output of a _cmdlet_ to the Get-Member _cmdlet_

`Verb-Noun | Get-Member`&#x20;

An example of running this to view the members for Get-Command is:

`Get-Command | Get-Member -MemberType Method`

![](https://i.imgur.com/OlwXSbS.png)

From the above flag in the command, you can see that you can also select between methods and properties.

#### Creating Objects From Previous _cmdlets_

One way of manipulating objects is pulling out the properties from the output of a cmdlet and creating a new object. This is done using the `Select-Object` _cmdlet._&#x20;

Here's an example of listing the directories and just selecting the mode and the name:

![](https://i.imgur.com/Zdxicjj.png)

You can also use the following flags to select particular information:

* first - gets the first x object
* last - gets the last x object
* unique - shows the unique objects
* skip - skips x objects

#### Filtering Objects

When retrieving output objects, you may want to select objects that match a very specific value. You can do this using the `Where-Object` to filter based on the value of properties.&#x20;

The general format of the using this _cmdlet_ is&#x20;

`Verb-Noun | Where-Object -Property PropertyName -operator Value`

`Verb-Noun | Where-Object {$_.PropertyName -operator Value}`

The second version uses the $\_ operator to iterate through every object passed to the Where-Object cmdlet.

**Powershell is quite sensitive so make sure you don't put quotes around the command!**

Where `-operator` is a list of the following operators:

* \-Contains: if any item in the property value is an exact match for the specified value
* \-EQ: if the property value is the same as the specified value
* \-GT: if the property value is greater than the specified value

For a full list of operators, use [this](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-6) link.

Here's an example of checking the stopped processes:

![](https://i.imgur.com/obTvbWW.png)

#### Sort Object

When a _cmdlet_ outputs a lot of information, you may need to sort it to extract the information more efficiently. You do this by pipe lining the output of a _cmdlet_ to the `Sort-Object` _cmdlet_.

The format of the command would be

`Verb-Noun | Sort-Object`

Here's an example of sort the list of directories:

![](https://i.imgur.com/xob5cqe.png)

### Powershell Commands

Recursively Locate File

```
Get-ChildItem -Path C:\ -Include *file.txt* -File -Recurse -ErrorAction SilentlyContinue
```

Get-Content

```
Get-Content "C:\Program Files\interesting-file.txt"
```

MD5 Hash

```
Get-FileHash -Path "C:\Program Files\interesting-file.txt" -Algorithm MD5
```

Base 64 Decode

```
certutil -decode "C:\Users\Administrator\Desktop\b64.txt" decode.txt
```

Local users in System

```
Get-LocalUser
```

IP Address Info

```
Get-NetIPAddress
GEt-NetTCPConnection 
```

Get Processes

```
Get-Process
```

Find API\_KEY in strings

```
Get-ChildItem C:\* -Recurse | Select-String -pattern API_KEY
```
