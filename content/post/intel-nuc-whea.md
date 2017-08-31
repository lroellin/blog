+++
title = "Intel NUC6I5 WHEA error"
date = 2016-03-17T15:07:59+02:00
+++

After my HTPC-turned big old ASUS PC died (ok, I may have made a mistake while mounting a new GPU), it was time for a new one. The NUC platform seemed to match my needs:
* Quick boot, all around fast machine
* Small form factor, not looking too geeky
* Can play low-level games (Sims)

I then bought the new Swift Canyon NUC with a Skylake i5 and fitted 2x4GB RAM. I bought the H version (which stands for High I guess) contrary to the K version. The H version can fit a SATA disk, which is what I needed since I didn't wanna spend money on a M.2 when I don't need the speed.

The platform matched all my expectations. There was a small problem with wireless periphery receivers, such as the Logitech Unifying dongle. Apparently, the USB 3 port interferes with devices in the 2.4 GHz band. A simple solution is to use a small USB cable extension and put it away just a few centimeters.

There is now a serious problem though: whenever I boot, I get a bluescreen telling me of a WHEA error. This points to a serious hardware problem, I checked replacing RAM but that didn't work. Intel knows of this problem (check this [thread](https://communities.intel.com/message/381202#381202)) and is currently investigating it, it seems to be connected to overheating and fans that don't run properly. I think this will lead to a recall as it's affecting more and more users.

I hope Intel gets this right as the NUC platform is exactly what I need. When this issue is resolved, I will post a more thorough review.