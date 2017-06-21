+++
date = "2013-07-28T20:14:31+02:00"
title = "Why I love PowerShell"

+++

# Preface

Please don't prejudice me, I'm a Linux user too and I love Bash. I just wanna write, why I love having the great power of Bash, sometimes imho improved in usability, on Windows.

# History

(no, this isn't gonna be a history lesson from your Volvo-driving teacher (Top Gear pun intended), just a brief summary of what was on the Windows platform before) Please take this section with a bit of salt, I'm not always sure and these things may be historically wrong, it's just how so far I know.

## Batch (CMD)

Please everyone, don't call this "the DOS box". It's just visually similar to DOS, but has improved from then on. Personally, I _hate_ CMD and avoid it, where possible. It works, but writing it in the correct syntax often means mangling around a lot, sometimes working around ~~odd bugs~~ unexpected features and behaviours. You also have to consider on what platform you are working on, sometimes features have gotten a lot easier, but you can't use them, or you'll risk non-understandable error messages spitting in the user's face. Especially the syntax is always making me sick. I know that Batch isn't so 2010 and may be old, but you can't tell me that

    %directory_where_this_script_resides_in% = %~dp0

is intuitive.

## VBS (Visual Basic Script)

Things have gotten a lot better there: You got object-orientation, better and easier syntax, error handling and all the nice stuff you've learned from other languages you're used to. There are only two bad things about VBS:

* Everything is one big pile I sometimes think, features were just pilled onto this language without thinking about modularizing, e.g. the math features like `Tan`.
* No shell If you got used to VBS for writing your system-administration scripts, then you're thrown back in history when wanting a shell.

# Powershell

Back in 2006, Microsoft gave us Powershell. I didn't know about this until late 2008 or something, and because I started my IT-apprenticeship in 2010, it wasn't until late 2012 that I have started learning it for doing real work, instead of just admiring the things you can now do on a Windows-shell. I always get excited a lot when talking about the Powershell, so I hope to get this in some kind of order. Bear with me, I have a lot to tell

## Consistency

Everything named the same _is_ the same in Powershell. When some command has a parameter `-Computername`, it _always_ is about which computer to connect to. If it has a parameter `-Filter`, it _always_ expects a wildcard-enabled string which the command tests its results against. Of course, this is up to the developer to follow, but the community sticks to those rules. And as always, sensible exceptions are allowed. Also, there is the CMDlet naming consistency. It's always *Verb-Subject*, where verbs are limited to about 6 and the subjects are freer. This means, you can gather what a command does by just reading its name. This is where all other shells and languages have a lot of work to do, pwd isn't just as intuitive as Get-Location

## Shell

As I wrote in the VBS section, I like to use my knowledge in a shell as well. Like this, getting only HTML-files
```powershell
# V3 syntax
Get-ChildItem | Where Extension -eq ".html"

# V2 and older syntax
Get-ChildItem | Where {$_.Extension -eq ".html"}
```
I know that this is possible in other ways, but I just like the simplicity of this. As an added bonus, everyone is going to know what it's going to do, or at least make an assumption, without having to read a man page.

## Strongly connected to Unix

A very good [quote](http://stackoverflow.com/questions/573623/is-powershell-ready-to-replace-my-cygwin-shell-on-windows/573861#573861) from one of the core developers (yes, they are out in the Internet as well):

> My original intent was to include a set of Unix tools in Windows and be done with it (a number of us on the team have deep Unix backgrounds and a healthy dose of respect for that community.) What I found was that this didn't really help much. The reason for that is that awk/grep/sed don't work against COM, WMI, ADSI, the Registry, the cert store, etc, etc. In other words, UNIX is an entire ecosystem self-tuned around text files. As such, text processing tools are effectively management tools. Windows is a completely different ecosystem self-tuned around APIs and Objects. That's why we invented PowerShell.

Read the whole post, it's really informative. I think, the best example are the list of aliases. How to get there? Take a minute to think about. If you did not succeed, simply type  `Get-Alias`. Did you see that there are `ls`, `tee` and `mv`? And if you're on the move from Unix to Windows, then type

```powershell
PS C:\Users\Dreami> Get-Alias mv
CommandType Name
----------- ----
Alias mv -> Move-Item 
```

to see what you should use when you're working with people that have no Unix background.

## Parsers

I really love the included parsers (in both directions) that Powershell uses, You can put all your variables as settings into an XML file and then just read them in by navigating down the XML tree, without having to know about all the caveats XML has. Since in Powershell, everything is an object, you can create your own objects and work with them. If you want, you can write them out in a table, or even export them to CSV or something like that.

## Coupled to .NET

Personally, I've never programmed in .NET, but it's on my to do-list. It simply means, you can use all the libraries and functions of .NET; most users will probably see this when needing `[Math]::` functions, to refer to my view about VBS.

## Drawbacks

However, there are two things that I don't like about Powershell; however I can understand why they did it that way

* You have to sign your code or it won't run, or you have to change (read: you have to tell your users to change) your execution policy to Unrestricted, which needs administrative permissions This is a major drawback when programming for clients you do not control, but is understandable when thinking about e-mail viruses like [ILOVEYOU](http://en.wikipedia.org/wiki/ILOVEYOU); it's more difficult to fool users. If you want all users to run your script, just buy a certificate and sign it
* Tabs are not supported in the Powershell ISE (the IDE that comes with Powershell). Not supported means it converts them to spaces, or doesn't let you use them and does nothing at all. They say that Powershell treats Tab ALWAYS as expand, like you know from Linux-shells, which can lead to undefined behaviour. If you really want tabs, add them in another editor, reload it in the ISE and save it there again, to check for unwanted changes introduced to tabs - I have never had any strange problem due to this and I _always_ use tabs.

# When to use what

For me, I use the best scripting language available on Windows where possible.

* VBS is installed on all versions since 2000/ME
* Powershell is available pre-installed in versions
    * 1.0 on Vista/Server 2008 (NT 6.0)
    * 2.0 on 7/Server 2008 R2 (NT 6.1)
    * 3.0 on 8/Server 2012 (NT 6.2)


Which leads to the following decision:

* When writing scripts for myself or for environments I know good (like at work), I use **Powershell**. Real world usage: compile or release scripts for the installer
* When writing scripts and not knowing what environment is used, I use **VBS**. It is available in all supported OS versions and features all features I currently use, though not so intuitive and sometimes not that powerful (check AD-Join scripts in VBS against Powershell for an example) Real world usage: script to check an installed component on client machines
* When writing quick and dirty, or I just need to copy a couple of files, I use **Batch**. As I said, I hate writing it, but once you get used to it and all of it quirks, it's not that hard (if you don't want to read it ever again) Real world usage: copying a plugin into an application directory

