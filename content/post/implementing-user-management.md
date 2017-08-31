+++
title = "Implementing User Management"
date = 2013-12-23T00:50:47+02:00
+++

Note: this post is about an older version of my [main website](www.dreami.ch) that I implemented in PHP. I still chose to import this post, because the thinking behind it is still valid.

I finally managed to finish my User Management part of my web site. This post will summarize a few things about how I did it. You might learn something from that, and maybe find an inspiration for your own problems.

# Why do you want users?
For the type of my site, user management is not something you see often, because it's mostly not necessary. As I wrote in the registration section, you gain nothing by registration, you only see a few more pages (see Features).

I implemented this because I wanted to develop some management pages, e.g. maintain my gallery, without using PHPMyAdmin every time. Since only me (and possibly other people later) should be able to do that, I needed a way to distinguish users.

First I thought about just restricting access via .htaccess and letting me authenticate by HTTP Basic Authentication. This would be technically fine, but I wanted something better, something more fine-grained. I then came to the conclusion that implementing full-blown user management would be the best.

That way, I can implement access level (see below), that I can assign to pages. If the user does not meet this access level, he is not able to see this page. Additionally, I can show content in pages to only a limited user group. If I would go for the .htaccess-solution, I'd had to put this on a separate page.

Why did I reinvent the wheel? Because this site is mostly developing experience for me, I did not want to use a fit-to-use solution.
# Features
Think about that for a moment: what features does a page with user management usually have?

I did the same and came to the following set of features:
## Registration
![](/post/registration.png)

Let the user register himself in your system. Check if his inputs match your policies (see below), if he does not exist already, and if it seems sane. If all is ok, write that to your database.
## Login
![](/post/login.png)

Check the user's credentials, and assign him all the features the system needs

## Show profile
![](/post/profile.png)

Let the user see what's stored in his database file (only "viewable" data, not passwords (even hashed ones)  or foreign keys and stuff)

I had a look at some other Profie pages. It seems like this is one of the pages that is really specific to your site, it should fit the site's other design.
## Edit profile
![](/post/edit-profile.png)

Let him edit his personal information
## Edit credentials (password and/or e-mail)
![](/post/change-credentials.png)

Let him edit his password or his e-mail address. This information is part of the credentials, since:
 * He can log in with his password
* He may reset his password by his e-mail address (not implemented yet)

Because of that, he has to enter his existing password first.
## Logoff
Let the user log off your system

# Not implemented
## Delete own user
implementing this is a political thing. Do you allow users to delete them selves, or does this need to be confirmed/done by the administrator?
## E-Mail confirmation
I don't have a clever plan to do that yet. I currently want to send an e-mail containing a hash of the current time and some stuff that you can't guess, and store that in the user's entity. Then, send an e-mail containing that hash. If he clicks on it, I delete that hash and mark his e-mail as confirmed.

This should be done every time the address changes.
# Technical stuff
In cases of two pages (one to read information, one to work on that information) like changing a profile. I went for the following naming convention

* change-credentials (read)
* changing-credentials (process)

You can observe that on the addresses in your address bar (oh, really?).

As you see, I made this list in a sort of subsequent order. To tell the truth, I implemented this piece by piece in the following order:
1. Add my user manually
2. Login
3. Logoff
4. Show profile
5. Change credentials
6. Change profile
7. Registration

# Access Levels
As said, I wanted to separate people. I do that based on access levels. On the web, someone suggested implementing a full ACL and then putting them together to predefined roles. I didn't want to take it *that* far (yet?), so I went for the following solution:

I currently have 5 access levels. To be fair, I only distinguish between Unregistered, Registered and Administrator for now.
## Unregistered
I called them "Everyone" in another markup, but went for this term. If you're not logged in, you're actually assigned the ID of the user "Unregistered"
## Registered
People that went through the registration process. I already know their nickname and their e-mail
## *Verified (by myself)*
These are people who I know they are. This will be a manual process, and basically means that this is someone who doesn't have multiple accounts and doesn't spam, if he could write posts or something. I don't have plans for this group yet though.
## *Trusted (people who don't abuse their permissions)*
People that I trust and know, that they don't mess up my site. These may be granted access to beta apps, where I have concerns that they may break my site if abused (like file upload). Again, this is a manual process.
## *Administrator*
Currently, this is only me (I don't want to sound selfish). These may be people who I really trust and know that they have the technical level to do this job too.

### Technical stuff
I assign these levels one of 5 access levels. At the top of my pages, I set a needed access level for this site, then check if the user meets this.

# Security
This is one of the most important things when implementing user management. There are various examples of big companies failing just as big, when their user databases were compromised.

Let me take you back to language class. Listen and repeat:

> I will always only store hashed and salted passwords. If I need to verify it, I verify the user's current input with the stored hashed and salted password.

With PHP 5.5, this got a LOT easier. For more information, read [this great blog post about `password_hash()` and `password_verify()`](http://www.sitepoint.com/hashing-passwords-php-5-5-password-hashing-api/"). Yep, these are the only two functions you need when dealing with passwords.

No "where do I store the salt" or "what exactly do I hash" or anything else. Supplement the clear text password to password_hash, store that. Read the user's password and verify it with the stored password_verify. Nothing more, plain simple, needs 1 password column.

Salted password hashing is no rocket science anymore, so please USE it.
## Never trust input
I see a lot of pages using JavaScript validation of forms. I hope they validate that data too when it is worked on, on the server too. Because, do you trust the client to always do your validation and NOT sending invalidated data?

That. is. adorable.

There may be people with JS turned off, so they may send you whatever they want. They are even part of the good guys, who send you garbage.
You have to think that a real attacker will send you garbage, even though his browser may not. He can even just construct a HTTP-POST statement himself, without any browser. So even if you made sure that he does not enter
    
    ; DROP TABLE `user`;

as a nickname in your JavaScript, does not mean he CANNOT send this.
## Technical stuff
To overcome this, I use JavaScript only as a lazy validation. It checks if all required fields are filled out, and if the passwords match. The real filtering is server-side, where I can access my user database to check if this nickname is not already taken, or if it fits to my nickname policy (which does not allow statements like that)

I use a sort of pattern. I define `$return` as "false", then go into a lot of checks. If every single one of them is correct, `$return` is "true". At the end of the function, it returns $return.

As you can see, it's best to define only the positive cases, because there are so many negative ones you might not think of.

# CAPTCHA
I simply do not want automated bots registering at my page. I know that there are real people you can pay to solve CAPTCHAs, but those are in minority.

Instead of letting you enter scrambled text, I went for the easiest solution, that is both accessible and easy to use, while not already being automatically solved.

All you need to enter is a simple multiplication of two factors, 1-10.
## Technical stuff
I did this by letting PHP generate these two products. I then define a CAPTCHA input field, where the user should enter the product. I then send the factors along, in a hidden field.

Why am I telling you this? I know that someone may be reading this, and he may adopt his spam software to my CAPTCHA.

* He will never adapt his software to this really small site
* If he does, he just spent some time solving 1 site, while leaving bigger sites protected. Win-win for everybody, isn't it?


# SQL Injection
Sorry, I can't explain you what an SQL injection is, in a nutshell. To really understand this, you have to search yourself. It basically is about escaping from your SQL query strings.
To overcome this problem, I use prepared PDO statements. According to my own experience [and StackOverflow expertise](http://stackoverflow.com/questions/134099/are-pdo-prepared-statements-sufficient-to-prevent-sql-injection), these are far more secure than your usual `mysql_real_escape`. Additionally, they are applicable to multiple SQL providers.

# Policies
This is different from security, since security says what's clearly not allowed, policy says what's not allowed in our case.

You have to think about what you allow on your site. For me, these are currently two things:

* Nicknames contain A-Z and numbers
* Passwords must be at least 8 characters long

These are really not the best, especially my nickname policy, but it is a starting point.
# External services
Why re-invent the wheel in every case? I used one external service that does what I need perfectly, without implementing this myself,  because I don't really care for this part.
## Gravatar
I get the avatar you see on the profile page from Gravatar. If a user (identified by his e-mail address) does ot exist there, you get a little identicon (an image based on the hash of your e-mail address).

That way, I always have an avatar ready, when there should be one, instead of a question mark :)

I hope my post helped you along the path of implementing this yourself. As always, these are my opinions, based on what suit me best. Your mileage may vary, you may even find flaws in my model. I hope that it helped you somehow!