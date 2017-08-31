+++
date = "2013-11-25T18:41:57+02:00"
title = "SysWoW64"
+++

This post will blow your mind. I'm really not making this up. 

In your normal C:WindowsSystem**32** are actually **64** bit binaries. Are you searching for **32** bit ones? Well head to SysWoW**64** then.

Why did Microsoft make it this complicated?
Remember, Windows is all about compatibility, so your bookkeeping application from '95 might still work. There are a lot of improvements to Windows Microsoft denies because of "would break compatibility to very old programs which will never ever get an update, but a great share of users is still using".
On x64 systems, x86 applications are actually living in their own nice world. The OS redirects calls to the file system (as well as the registry), so when a x86 program thinks it's reading from `C:\Program Files`, it's actually doing this from `C:\Program Files (x86)` without notice.
System32 is one of these folders that were made way back when Windows was switching from a 16 bit code base to 32 bit in Windows 95. Since then, a great deal of applications relied on this path to find a lot of useful tools.

Since then, a lot of developers have gone the wrong way of thinking, ye olde System 32 path will never change, and hardcoded it. If you would create a System64 folder for the 64 bit applications to use, they would either not find it, or compiling for it would mean to have switches in your application that, depending on your compilation target, would either go to System32 or System64.
There comes another choice of Microsoft: make it as easy to develop for as possible. That's not easy, so screw that, having a x64 application at all is far more important.

To overcome all these problems, Microsoft made this SysWOW64 folder. WoW actually has nothing to do with this nerdy MMORPG that so many people seem to got lost in, but does mean Windows [32] on Windows 64. There was actually a Windows 16 on Windows 32, still living on in all 32 bit versions of Windows.

To put it simple: calls to System32 from x64 applications would go to the real System32 folder, x86 applications would be redirected "one step down the ladder". Sounds ok but seems like a drunk decision when you first hear about this.

Fortunately, most people will never notice this. I first ran into a problem when using ODBC in an x86 application. I configured a connection in my ODBC Manager, but that application could not find it. Why? Remember, nice own world and so on... my x64 ODBC Manager connections did not make it through the gates. My old application was searching in its own nice world, and all that the old ODBC Manager said, was "Get lost". Bad, bad world!