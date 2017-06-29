+++
title = "Fixing a real git history problem"
date = 2017-02-16T16:11:24+02:00
+++

I'm recently involved in translating the old German comments in the LibreOffice codebase to English ones. It's quite a challenge, since you need your translation brain and also your coder brain. The end result should be a comment that is technically correct while still sounding English. 

I ran into a small problem I made myself: at first, I used the web editor when I started, a week ago. I didn't do any work since then until today, where I picked up again. Of course, someone else has made changes to that file, although in a different area. 

Since I didn't like the editor, I cloned the whole repo and used the setup scripts to commit and publish from my local machine. 

Now instead of downloading the diff from the web version, I downloaded the whole file as-is and replaced the git version with that one. I then went on with my translations, eventually publishing it (applying for code review). 

Now you might already know what I did wrong. When you commit in git, you essentially create a linked list of diff patches, all pointing to each other. So when I just downloaded and re-applied my complete version, my patch included reversing the change. Oops. 

Of course, a code reviewer saw this, so nothing really happened. Now I still needed to fix this. My plan was:

1. Put my complete new file in a new branch based on master
2. Get a diff from that change someone else made
3. Apply that diff
4. Publish the new version where the patch is just my changes

And that worked out. To get a diff for a specific commit and only the part for a specific file:

    git format-patch -1 <sha> specific/file.cxx

Then you just apply the patch via:

    patch < file.patch

Note that this may not work completely, so check for the error messages patch provides. For me, I had to manually apply a small edit where it couldn't find the surroundings. Now, if this were multiple commits, you would just apply each patch sequentially, in the right order. 

And then you can safely add, commit and publish as usual. 