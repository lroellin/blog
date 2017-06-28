+++
title = "You Need HTTPS"
date = 2017-06-29T00:10:25+02:00
+++

I keep hearing people saying that they don't need HTTPS. First of all, there's https://doesmysiteneedhttps.com/, but they're missing or only scratching one point: keeping your users safe.

Let's say you own a big website where users can post all kinds of things. So content on your site can be cooking recipes, how to clean your bike, but also some bad things about some government. This is to say, someone censoring stuff can't just shut the whole site down without potentially calling for trouble.

Now let's say there are people reading the government-critical stuff and they're tracked by some government institution. If every content they're viewing can be seen in plain text when you're just using HTTP, a suspicion can easily turn into evidence. But if you're using HTTPS, any tracker just sees a connection to your servers but can't see what's transferred.

If you're now thinking, I don't serve any content that could be seen as dangerous by any party, think about it. If you're telling people how to use VPN, that could be bad in some places. If you tell people how to encrypt their email, voilà. And with Let's Encrypt, there's no reason NOT to have HTTPS, unless it's some hoster that doesn't support it. In which case, it's time to get another one. If it's that much behind time, it sure isn't gonna be the cheapest one aswell...