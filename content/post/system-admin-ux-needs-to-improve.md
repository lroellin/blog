+++
title = "System Administration UX needs to improve"
date = 2017-07-01T16:46:24+02:00
tags = ["UX"]
+++

So as you may know, I'm working as an IT security guy. Part of my job is installing systems and maintaining them. So I get to see a lot of different products.

My main problem is that system administration is not easy or intuitive. There's far too much bullshit I have to go through for simple tasks. Sometimes it even leads you the wrong way. I'm not calling names here because I don't want to shame, I want to help. People who know the struggle will recognize it. I'll also  add an enhancement for each problem so that it's not just telling how bad everything is.

Also note that I'm aware of the phrase "With great power comes great responsibility". I know that it's my fault when I'm screwing up without having properly read documentation. I just want to say that all that should be easier to avoid.

# UI is ancient

System vendors often think that people don't care about the UI. It's made by techies and will be used by techies. But I'll tell you something: it hurts.

One example is the local system management of a firewall product. It's a great product and very powerful but it just looks too complicated. Important things like clustering are hidden in submenus and you have to think about which cluster type you're using. If you view the status of the wrong type, it gives you the impression that this is a single machine.

It also does not follow recent interaction techniques known to users. To upload a file, you have to choose your file and then click Apply on the bottom (there's always Apply and Cancel on every page. Also there's save?!). My problem is that this is not intuitive. Of course, Apply is like a commit button for what you configured on each page, but this generalization goes too far in that case.

My proposal: follow recent usability techniques and don't let your programmers do the design. If you have no idea of visual design (like me), use Bootstrap at least.

# UI is misleading

Another thing I always fall for is the status window of a well-known firewall product. You can see the connection status of the management to its firewalls on the GUI. When you click on it, it just says "Communicating"

To me, this sounds like it's still trying to figure out the status. After a while and with some external guidance you realize that this is the success message.

My proposal: use proper non-ambiguous wording and maybe some icons instead of just text.

# User Guidance is non-existing

Recently I had to install a firewall product on an older appliance. The installation process is not that easy since you first have to install an OS and then one or more applications on top of it, in the correct order.

After installing the OS we wanted to install the application. It did not install via the web interface because something was missing. On an error like this you think the file is corrupted. Wrong! You just can't install it on the web interface, you have to go via CLI.

Why can't you tell me about this issue? Don't say "Oh this is missing". Say "This package does not support web interface installation".

We then installed it via CLI (or tried to) but after running the script it told me that a wrapper was not found. This sounds like a serious issue, like a problem with the OS maybe.

Wrong! The problem was that it needs an older version first, this is just an upgrade package. Again, why don't you tell me this? This would not have been that much of a change since all the error messages were in that script.

Another weird thing was when you had to install the base package via web interface and the upgrade package via CLI but you see where I'm going...

My proposal: fix these misleading messages and provide useful help. The error messages provided sound like "this guy can't walk" instead of "get him an ambulance, he's got a broken leg".

 
# Partial UIs

One thing I hate about certain products is that they're only partly configurable by some kind of UI (like a GUI, or some nurses text-based ones). They also rely on plain text files. 

The product in question uses a lot of configuration files but displays them via the UI. If your product relies on these text files so much, I guess it's crucial to have them formatted correctly. So yeah, let me just mangle around in these files hoping I don't break anything. A UI can help the user by giving tips and guide him through the process. You can also validate user input before committing, like when configuring a network address. Do I have to enter the full `255.255.255.0` or just a simple `/24`, or can I do both? Do you need a slash before the `24` or not? These are all things you have a UI for, so why don't you use it?

Note that I'm perfectly happy with an approach where you have a basic GUI and a more powerful CLI behind it. You're my hero if you do all the things of the GUI via CLI in the background. If you show the commands your GUI made on the CLI to achieve that, you're my king. That way, I can easily replicate it on other machines. 