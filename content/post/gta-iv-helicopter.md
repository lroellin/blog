+++
title = "GTA IV PC: Helicopter climb in last mission (Revenge, Out of Comission) not working"
date = 2014-11-17T14:23:16+02:00
+++

**Warning:** this post contains **spoilers**, if you're not in the last mission!

This is a post I should've done a year ago, but didn't have time to. This has cost me several playthroughs of this mission, since there are no check points in this mission. And no, I'm not James May and live in the past, but it was on sale last winter, so I tried to get through it.

If you chose Revenge at the end, you have to hunt down an escaping Pegorino. There is one sequence where Roman and Jacob arrive in a helicopter, in which you have to jump. Like many post-CoD 4 games, there is a cinematic scene where you have to press buttons to climb into the helicopter. In this case, it's a rapid succession of Space needed. However, you can do it as fast as you want, it won't work. Why?

It seems that Rockstar has problems with multi-threaded CPUs. That means, with every CPU that has more than one core, which on gamer PCs is anything later than 2006. To me, it looks like the pace is calculated on multiple cores, therefore yielding much bigger results than any human being can meet. So for this last mission, you should force GTA to use less cores. Yes, you'll be playing this last mission in single-core mode. But just this game, not your whole PC (thanks God). And yes, this works with Steam too.

To do this, fire up GTA IV to the main menu, but don't start the real game yet. Then start Task Manager and search for GTAIV.exe. There, click on "Set Affinity". You will then be presented with a list of all your cores. Uncheck the first "All processors" box, then check `CPU0` as the one and only.

Click OK and switch to GTA IV again. Fire up the game (you may notice less performance, but this is just for this last mission), and play through this mission. You now still have to be fast, but in a humanly possible way.