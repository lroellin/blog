+++
title = "To automate, you must document"
date = 2014-03-04T01:25:14+02:00
+++

Automation in IT is all about turning your dreading manual task into a one-shot click, with parameters given for just this run.

As an example, I'll show you how I automated the creation of our customized Firefox ESR version. By customized, I mean one with a special add-on created by ourselves (by the great [CCK Wizard](https://addons.mozilla.org/De/firefox/addon/cck2wizard/)) and some other important stuff. My weapon of choice was Windows PowerShell and 7-Zip CLI, but as you won't see any code listings here, that doesn't matter, who reads them anyway?

Since I don't want to have any problems related to plagiarism, this post was inspired by [this great book by Tom Limoncelli](http://www.amazon.de/Management-System-Administrators-Thomas-Limoncelli/dp/0596007833). But for now, let's go on topic.

Oh no, I sad the bad, bad word. _Documentation_. Let it stand there for a while and horrify you to hell.

Let's face it, we are bad at documentation. Documentation to us is like writing about a single wave on the sea, as soon as it's written out, it's outdated. But if you want to automate a task, you have to be sure what exactly you are doing.

# Why is this needed?

Because creating this customized Firefox ESR was such a complicated task manually, I documented it. This had two advantages

*   If you are run over by a bus, your co-workers may take over this job, and (less dangerous):
*   It helped me free my mind, because I didn't need to remember all the steps, their correct order and the pitfalls to avoid (great idea by Tom!)

And if you automate it, this brings even more advantages

*   A program does not get distracted, it doesn't make errors
*   It's faster than any human
*   You have to describe each step as precisely as possible
*   These steps are in their correct order
*   If commented _well_, your program is a living documentation, so it's not outdated! How great is that?

# Why so precise?

We are told many times, computers are just number crunchers. They do what they're told, no more than less. To a human, you may say "peel that apple". To a computer, you have to say

*   Open the cutlery drawer
*   Search for the section related to knifes
*   Take the peeler out
*   Hold the apple in the other hand
*   Carefully turn the peeler around the apple
*   If end is reached, turn apple sideways
*   Repeat until no more peel is on the apple
*   Stop

So this is exactly what we are going to do later.

# Step 1: instructions for yourself

Now what did I do? In a first version, I just wrote out a version for _me_. That means, some instructions that took multiple steps were squashed into one, because _I_ knew what exactly that meant. That first version looked like:

1.  Download Firefox ESR
2.  Unzip with 7-Zip
3.  Start CCK Wizard, click through, change nothing but version numbers
4.  Copy new directory to unzipped Firefox
5.  Copy the other important stuff to that unzipped Firefox
6.  Re-assemble it with some bizarre 7-Zip options
7.  Store it in a particular folder with a particular name

For now, let's assume that step 3 was the tricky one. The handling of directories by CCK Wizard is something you just have to know, it's simple, but you have to try once or twice.

That version was ok, since (1) I  didn't need to remember it anymore and (2) my co-workers could do it, maybe with an additional manual from the internet, or by pure fiddling around.

# Step 2: instructions for co-workers

So this documentation needed some improvement. I took this CCK Wizard step and expanded it to every single click I made. Additionally, I made it easier since I included more precise information and a link to a known-to-work version of 7-Zip on our network file share. So it looked like this now:

1.  Download Firefox from [here](https://www.mozilla.org/en-US/firefox/organizations/all/)
2.  Copy 7-Zip from ...
3.  Unzip with 7-Zip to a local folder called ...
4.  Start CCK wizard
    1.  Load configuration from file ...
    2.  Click through and change _these_ and _those_ values
    3.  Save configuration file as ...
    4.  Save add-on as ...
5.  Copy this directory to ...
6.  Copy the other important stuff to ...
7.  Start the command line from ...
    1.  Paste this line
    2.  Edit ...
    3.  Execute
8.  Store it in a particular folder with a particular name

I want to remind you, that this is not a dumbed-down version, but a more precise one. Don't look at your co-workers and think "they know nothing about this job", but "how can I make this clear so nobody understands that important bit wrong".

# Step 3: look for manual intervention

When your list is complete, it's now time to fire up your IDE and turn these human instructions into computer constructions.

If you look at the list above, you may spot one thing that doesn't seem to be easily automatable: CCK Wizard. These are steps that require a GUI that does some magic things, most of the time. This is where you really need to take a moment, this is the tricky part of your automation now.

## Technical Bla

Fortunately, I found a way around. I took a before and an after version and did a quick diff, to see that all my clicking around does, is to change a string in a configuration file. Bwahaha, I can do that too! I made a configuration file with some text markers, where that string was going. In my script, I then read that file and replaced those markers with my version string, then wrote it out again.

So after all this time, I had a working version that was doing its job completely automatic. Before, you needed about 15 minutes of undistracted work time. Now, you just supply a file name to this script, it reads out all the other important parameters, and just does its job. Wait 1 minute and you're done.

PS: this [great music](http://www.youtube.com/watch?v=jiwuQ6UHMQg) helped me write this post!