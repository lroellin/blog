+++
title = "How to take notes as a CS student - revised"
date = 2017-02-24T15:53:02+02:00
+++

This is a follow-up to my [older post]({{< relref "post/take-notes-as-a-cs-student.md" >}}). Not everything in there is still valid.

First, I switched to a Mac starting this semester. The reason being that I need a Unix-like system but Linux is sometimes just too cumbersome. I also like that for certain tools, there's just a "Mac" section instead of one for every kind of package manager out there.

The problem started when I saw, that OneNote is really not up to the job on the Mac. My usually 50 pages (read: images) long lectures and notes along them, are just laggy to load and scroll. It's really not an issue on my other notebook which has about the same CPU specs as my MacBook Pro (I bought the old one for reasons).

# What I now do is the following

For every lecture we have, I copy it from my `sync` folder to a special `lecture notes` folder. I then open it in Preview and annotate it with notes from the lecture.

After the lecture, there's a step I didn't do before. In the evening or on the weekend, I go through the pages and write a summary for the current lecture. I think I'll still have to go through the actual lectures in my study period before the exams, but it's more a step of rethinking and maybe following up on things I didn't have time during the lecture. You can find these at https://github.com/lroellin/hsr-zusammenfassungen. To actually find them useful, you should be able to read German, but I think you'll see the way it works.

To actually type up these summaries, I use [Typora](https://www.typora.io). Some reasons I particularly chose this:

In Typora, you type in WYSIWYG but it's still Markdown and you see just a live rendering. This helps me spot errors as I type. It does support Markdown syntax (so you can also type an asterisk and it'll create a list), but also menu items/keyboard shortcuts for choosing your formatting as you would in a word processor. It also supports Github Flavored Markdown, a flavor I personally see as the de-facto standard.

The feature that's made it stand out the most, is picture pasting from the clipboard. See, some graphics are best simply copied from the lecture. Typora supports this very easily. You specify a folder where Typora can copy the picture files to (should be a folder in the same folder as your Markdown file). Whenever you paste an image, Typora will save the image in that folder and automatically add that image to your Markdown.

Additionally, it supports LaTeX Math Mode inline and block-style. This is not GHF, but as it's enabled by `$$`/`$$$$` (as in LaTeX), anyone rendering it on GitHub will just see what looks like LaTeX and can then figure out what that means. I think this is reasonable, as LaTeX is also the de-facto standard for typing up math. And anyone not fluent in LaTeX will still see the intention and meaning of a \frac{x}{y}. Why not switch to full-blown LaTeX you ask? I tried that and have typed up summaries in LaTeX but it's just too much friction and that's what you gotta keep down when learning a new habit.

Also, the live rendering switches to Markdown on certain parts, like inline code rendering, when you set the cursor to it. And it's quite intelligent, so it doesn't do this on list asterisks. And of course, you can always switch to Source Mode and fix those pesky errors you get when importing weirdly formatted stuff.

Is this the ultimate solution? Probably not. But as last time, it works for now!