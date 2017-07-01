+++
title = "\"How to hack any PC in 2 minutes\"... with physical access"
date = 2016-10-08T16:00:13+02:00
+++

Can we please get a little knowledge out to all the script kiddies? If you're in physical possession of a device, hacking it is not difficult. Let me make it a quote so people skipping will read it 

> Hacking with physical access is like climbing over a garden fence

There are many tutorials on YouTube if you search for Hack Windows PC or the like. Most of the time it's some teenager searching for help in getting more computer time or one that wants to stalk his crush. The second one is actually worrying. The tutorials are often like 

1. Boot some tool / into fail-safe mode
2. Change Windows Password
3. Reboot, log in
4. Do whatever you want
Now you might say "yeah, Windows/`<insert OS>` is broken, they're so stupid, haha". Well, they're not. You could just as well read the hard disk and get to your data. Oh you use a BIOS password? I'll just take the disk out and analyse it in my computer. Oh you use a disk password in your BIOS? Same thing. 

The only thing that actually works is encrypting your disk, known as full disk encryption. But I could do other things then. I could install a physical keylogger on the back of your computer where you never actually look. Or if I'm desperate, I could take the disk out and wait several million years to decrypt it. 

Even IT security appliances have stuff like that built-in, even on purpose. There's a password reset procedure for almost any device that will not wipe the data. Usually, you can do something until 30 seconds after boot or you can press a button during boot that will take you to a special shell. You can then connect via a serial console (a separate cable port) and do some pre-defined tasks. Why is that? You got access to my switch configuration then, right? 

Well, those manufacturers think the same. If your physical access layer is broken, there's nothing you can do. So any protection would actually be useless. So let's do it the other way and make it easy for administrators to reset passwords in case its forgotten, or for some lab machine where the user forgot to reset it afterwards. Of course, there are others like a single-sign on (SSO). device, where physical tampering will wipe the key to decrypt all the passwords. But then too, it's a cat-and-mouse game between detecting a physical break-in to the machine vs. opening it undetected. Cause once you're in, you can tamper with it. 

Another important aspect is that devices have to trust their environment. It's like kids, they trust you to navigate them through the first years of their life. If you tamper with the SSO device and the break-in fuse didn't trigger, you can do whatever you want. You could apply logic analyzers to the mainboard (while running) and find stuff out about it. Of course there are counter measures, but generally the device has to have a trusted base workspace. 

So if you ever hear someone "Hey, I cracked that computer over there" you can just say "Oh cool. Anyway, ..."