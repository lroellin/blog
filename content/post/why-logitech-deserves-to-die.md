+++
title = "Why Logitech deserves to die"
date = 2016-05-06T15:14:11+02:00
+++

Some time ago, Logitech announced they were in big financial trouble and they needed to do a turnaround on their products. Instead of periphery devices for computers, they're focusing on mobile periphery, like stands and Bluetooth keyboards for iPads.

That is a good thing. Here's some stories of my last stuff I bought. Note first that I'm actually kinda loyal to Logitech, especially being a Swiss company. But they fucked up badly in the last years.

First for my profile: I'm a CS student, so I need to have an easily-typable keyboard. But I'm also a gamer, so I need features like anti-ghosting. But I've never had problems with ghosting on normal keyboards so I guess the games I play (mostly FPS) are not that demanding, at least at my skill level.

The worst offender here is my trusty keyboard, the Logitech Illuminated. It features flat keys and an illuminated backplane. Nothing fancy, just some FN keys for media control and such. I loved this keyboard that much that I bought it again after my old one died (of drowning in iced tea). So I fired up some CoD and played single player. But there was one run-jump that I couldn't do if my life depended on it. Since this was a replay, I was fairly sure I made jump some time ago. Upon closer inspection I saw that I didn't even jump, just run and fall to your death. Could it be they... no, no, no, I'm incapable. So I got my wireless media keyboard (K800) over and tried again. Worked perfectly on the first try. What the actual fuck?

I then heard from a friend that Logitech are now introducing extra-ghosting into their keyboards. And that's exactly what was happening here. I could do whatever I wanted, play normal FPS games, but I couldn't press Shift (run) + Space (jump) at the same time. They blocked it so you will buy their more expensive gaming keyboards. Deliberately.

Another offender was the mouse. I bought a Logitech Performance MX. It's wireless and charges via microUSB which is nice. Note that I didn't have plans to be top-notch in games, so don't hate for using wireless for gaming. That's not the point here.

I usually put more controls on the mouse than the usual game controls. Here's my setup

* Left mouse: shoot
* Right mouse: aim
* Middle mouse: reload (typically R)
* Back: crouch (typically CTRL)
* Forward: use (typically E)

Playing some CoD again (which is click-and-hold for crouching) I saw that I was crouching down but standing right up again. What the fuck again?

Turns out that Logitech doesn't send the actual keypress, but do an interpretation via their software, stored in the driver. They are sending "Web: Back" and this is a one-time event. So this is either a safe mode for people who don't know that you should let keys go after you're done, or again some limitation for gamers. You decide.

Fortunately, there's help for that problems. On an [older post]({{< relref "post/logitech-thumb-buttons-dont-hold.md" >}}) I described the problem and a solution, using uberOptions. Note that this is the only working solution and I don't like that, another step that I have to do when reinstalling my system.

So for these two, one shows clear evidence and the other is up to you to decide, but for me it looks like Logitech is deliberately pushing you to their more expensive gaming products for no technical reason.

This has led me to not consider a Logitech product for my rig here anymore. I'm now perfectly fine with Razer products, they may not be the best but at least you're not getting screwed. I was thinking of buying the G933 from Logitech but will now probably go with the Corsair VOID. So for anyone who wants to screw up their company, have a look at Logitech.