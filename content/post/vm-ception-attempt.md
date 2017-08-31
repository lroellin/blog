+++
title = "VM-ception attempt (Windows 10 to XP)"
date = 2016-05-11T15:35:21+02:00
+++
This is something I wanted to do since forever. VM in a VM in a VM in a... you get it. That test will focus on desktop OSs.

The software used here will consist of VMware Workstation Pro for the host and VirtualBox for each guest-host thingy.

I set up a folder on my host, consisting of the VM folder, an ISO folder and a share which I will be mounting through each instance. Note that my current plan does not contain licenses, but I do have them at hand if needed.

I will install any Guest Additions though because in my experience it makes it run much smoother.
# Windows 8
I fired up VMware Workstation and gave it a shot. I'm using Easy Install because it's taking care of most of the things and saves me time. If there's a problem, I will revert to normal install though.

I then configured the CPU and the RAM, followed by 100GB of disk. They were provisioned in advance

A quick screenshot from my Task Manager on the hypervisor shows the 16GB of RAM provisioned, the CPU working slowly and the disk sometimes in use.

![](/post/tm-host.png)

One thing to note is that you enable Virtualization Passthrough. This seems to be a problem on VirtualBox, so we will have to live without VT-d and VT-x on Windows 7 onwards. One limitation will be that our guests will only have 32 Bit support. We'll see how that works out.

So first on, VMware installed its VMware Tools and I mounted my network drive. This is how it looks for now:

![](/post/state-win8.png)

I then installed VirtualBox and configured Windows 7.
# Windows 7
From here on, we only have VirtualBox support. One thing I saw happen is that the limiting factor seems to be the disk. I don't have any better disk at hand as the physical disk is already a WD Red here. We'll see if that will be a problem here.

It installed fairly quickly and I could install the Guest Additions. Here's how it looks so far:

 ![](/post/state-win71.png)

So up to the next, the behemoth. Windows Vista!

# Windows Vista
So I need you to know that I'm already using SP1 which was a big improvement in Vista's resource usage. This will be the biggest player to install although I do not think that it will be much of a problem.

Personally, I was using Vista all the way from 2007 to 2009. I did not have many problems because I got a new computer back then and it did not have a major performance impact. I did have Windows XP installed in a dual-boot configuration but never used it much. So if you trust a guy who's really used Vista, it wasn't THAT bad.

Here's where I ran into a problem. Apparently my Vista CD is x64 only and I need VT-x for that. Also I can't put any more than 1 CPU in it which would certainly be a problem for Vista. So I decided to re-do Windows 7 on VMware Workstation inside Windows 8. I shouldn't run into any licensing issues here, I hope, since I'm not really using it and my student copy is officially an evaluation copy anyway, so we'll see.

I won't re-do any screenshots though because I don't expect anything to change performance-wise.

So after losing about half an hour, I'm back where I left the action. The installation of Windows Vista seems to start at least.

Note that this install took the longest yet. I was through from Windows 10 up to Windows 7 after one hour, then had to reconfigure everything, and I'm now 45 minutes into the install phase and it's only finishing up the "Windows is installing" wizard where it's basically copying archives from the ISO to the HDD and extracting them. I'm not sure if its due to the Vista slowness or the VM-ception effect, but installations before did not show that problem. Maybe we'll have a better look at it in Windows XP.

After the desktop started, this is the first build where there's a notable lag in using it. This is again, either due to the VM or Vista's resource usage. I'm going to install SP2 because VMware Workstation does not run without that and I'll have a look again.

So after installing SP2 I discovered that I was still not able to install VMware Workstation. Apparently, the MSI is using another Installer version which I can't install to Vista. So I'm going with VirtualBox again for my last step. The non-supported VT-x from inside Windows XP will be no problem, since I don't plan to take it any further. And if I do, there's no plan for more than 1 CPU.

We've seen to have hit the limit though. Windows Vista is in itself very slow to run and a VM inside of it is even slower. Therefore, I will go back to Windows 7 and install Windows XP in it directly. I will make an OVF export of Vista though so I can play with it if I want.

So this will maybe be continued at a later stage because right now Windows XP does not seem to be installing. Maybe it's the same problem as Vista, maybe not. So the conclusion...
# Conclusion

One VM in a VM is fine. Everything more is gonna be shit. I'll check on more configurations once I'm done exporting everything.
# General
One thing you may have noticed is that I was having less and less screen space for each VM. This was a conscious choice so I could show of the Task Manager of each VM in one shot. I could have just as easily gone full-screen for everything.

Note that in a configuration like I used, you're going to get a small screen very soon. I was using 2560x1440 as a starting point which is already much more than most people. For example, Windows 7 was running at 2210x1149. Make sure to keep that in mind when playing because anything below 1024x768, which is very small in itself, is gonna be a pain in the ass.

Something I was actually astonished are the "network" speeds. The share which is mounted through those several instances had a download speed of 40-50 MB/s (this is megabyte not megabit). I thought it would be slower since it's essentially copying data on the same drive to another disk file or even memory, one at a time.