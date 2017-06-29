+++
title = "Installing Check Point R70.20/R70.30 on IPSO 6.2 Disk-based"
date = 2014-08-19T04:42:59+02:00
+++

I've run into several problems today, so this is a public mental note for anyone who ever runs into the same problem. I know I will, so why not make it easier for everyone.

If you're not into Check Point, this post will make no sense at all. Skip it :)
# Prerequisites
* IPSO 6.2-xxx.tgz (or .zip)
* Check Point R70.tgz (IPSO, disk-based*)
* Check Point R70.20/R70.30 (IPSO, disk-based)
* Laptop with FTP server and username/password

**If it's not called disk or flash-based, it's probably disk-based**

# Install IPSO
To install IPSO, you need a .tgz file of your IPSO version.  *If you only have .zip, the .tgz is in there.** Boot the machine and break at the boot manager. At the prompt, enter `install` and follow the instructions for FTP.

When prompted, use the Voyager setup. Enter an IP for this machine and go through Voyager. You'll need to install a package under Configuration > System Configuration > Packages > Install Packages.
# Install Check Point
For R70.20/R70.30, you'll need R70 as a prerequisite. Upload and install R70 via Voyager in your browser. This will take about 10 minutes.

Then, you'll be able to install R70.20/R70.30. However, it's not possible via Voyager because (for some obscure reason) there's no `Application.xml`. They've done this on purpose somehow, because there's a note stating: you need to do this on the CLI.

**Upload** R70.20/R70.30 via Voyager, but **don't install** it yet. Switch to CLI and go to /opt/packages (uploads are stored here). Then, enter two commands to extract and install:

```bash
# Extract file
gtar -zxvf filename.tgz
# Install
./UnixInstallScript
```

This will take another 10 minutes. Then, reboot your machine and you're fine.

* There is no IPSO 6.2 GA029, it's always GA029a02 (MR1)
* The .tgz is hidden in the .zip
* No comment in file name means disk-based
* Application.xml is only needed for Voyager
* R70.20/R70.30 needs R70 as prerequisite