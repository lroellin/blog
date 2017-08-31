+++
title = "Windows Image Backup/Restore done right"
date = 2016-03-11T14:48:09+02:00
+++

Recently my Lenovo's SSD gave way. Writing to it was slow and sometimes the whole system would halt for several minutes, only to replay everything afterwards. So I called support and they sent someone to replace it, which went quite good.

There's the need to backup and restore your PC though. Having worked with Acronis before, I'm a bit of a spoiled kid, but I didn't want to spend money just for that.So I had a look at the Windows Image Backup that was introduced into Windows 8.

Backup is quite easy: you need a drive (hard drive, SSD, USB drive, *network drive*) with enough storage. Note that the size needed is not the same as reported as utilization on your C: drive. Things like your page file or hibernation file are automatically left out. Just follow this [guide](http://www.windowscentral.com/how-make-full-backup-windows-pc)
In the folder you specify during this process, it will create a folder structure as follows:

* WindowsImageBackup
  * `<hostname>`
     * `<actual backup files>`

Note that the files that are created are not meant to be readable in any way. Don't mess with those or delete something. All you need to think about from now on is that WindowsImageBackup folder as a whole.

Now restoring is a bit difficult. Starting it is easy though: Boot from any Windows installation (DVD, USB drive, etc.) and use "Repair your computer" (you don't need the actual Windows installation, just the repair environment). Then you can find your way to the Windows Image Restore process.

The difficult bit is getting Windows to recognize your backup image. A few things I found out:

* It needs to be either an HDD or a DVD drive. **USB stick drives do not work!** I couldn't get the network option to work either.
* The WindowsImageBackup folder needs to be at the top/root level. It should still be organized as discussed above.
* If you're not sure if Windows recognized your drive, use the command line option. Two commands are important:
  * `mountvol`Display the mounted volumes. You're shown a UUID and a drive name (C:, D:). Use these in the next command. **Note that C: or D: etc. do NOT refer to the drive names from your normal Windows installation,** they are just chosen in an arbitrary order of mounting.
  * `dir C` or whatever drive you choose: See what files are on that drive.

When it's found your image, you're presented with a list of backups it found. Just choose the one you want and restore. This is taking a bit of time but is mostly copying data, so it's just limited by your source and restore drive.

I hope you can get it to work with this guide. It was tested on Windows 10 and if you have any questions, just comment here. I'm usually quite quick to respond even though there's not much on the blog for now.