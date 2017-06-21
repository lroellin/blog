+++
date = "2013-11-15T10:28:17+02:00"
title = "You can't install anything while installing updates"

+++

Windows has many quirks one does not even want to know about. I've compiled some of these, along with an explanation. Most of the time, I can perfectly understand it from a technical viewpoint, but it does often make NO sense at all from a user perspective

If you want to read more about them, read Raymond Chen's famous blog, [The Old New Thing](http://blogs.msdn.com/b/oldnewthing/). I've taken some of my favourites from his blog or his book. He's the guy that even brought me into those kind of quirks :)

# Windows Update blocks installer

Ok, I just needed my laptop that I had laying around for a while. I turned it on, then went to installing a software I need for my current task. While doing this, I confirmed to install updates. Oh dear...

The software's installer failed randomly and I had no clue at first. Then I remembered that I forgot to observe something that I usually do: never install updates while installing software.

Why? We have to remember that Microsoft uses the Windows Installer component to install MSIs. Most software should come in an MSI (an installation package together with installation code) rather than a setup.exe (a program that does the job of installing), I won't go into depths why MSI is far more superior. One of Windows Installer's features is to do safety checks. One of those checks is "Is there any other installation running?". The reason is obvious, two installations at a time may come in conflict and overwrite each other.

This was where my installation failed. It used the Windows Installer, which saw that another instance was running (for updates). Therefore, it crashed. There was no nice error message, because those errors should have been popped up at the beginning of the installation. Since my installation was already running when I confirmed Windows Updates, it got into a sort of race condition.

I then canceled Windows Updates and re-ran my installation. Failed again. Why? One of those other checks is "Is a reboot needed?". One of the updates set that very flag.