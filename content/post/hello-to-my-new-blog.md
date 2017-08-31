+++
title = "Hello to my new blog"
date = 2017-06-29T16:15:27+02:00
+++

Hello there! If you've made it to this page, you're on my new blog.

The first thing you'll notice is the new domain. The old one was based on my nickname from years ago and I don't like it that much anymore. 

I chose to move away from Wordpress, mostly because it seems like legacy software to me and it can't decide on how to render my posts. Especially code listings break every other edit. And I also like Markdown and Wordpress seems to support it. But again, it can't decide on if it needs to render it as HTML or if that's already done.

This blog is now based on Hugo, a static site generator. All posts are on [GitHub](https://github.com/lroellin/blog) which gives us version control - so you can check the history of my blog posts. I added a little link to its history on each post. Also, since I can now write Markdown or chose to deliberately use HTML, I'm now in much better control on how things look on this blog. 

I manually imported almost every post from my old blog. I skipped a few, maybe 2-3 that just weren't worth it, or I just didn't think the same anymore.

By the way: Hugo is *very* fast compared to Jekyll, the other static site generator I use for my other website (that may not be running in the future), www.dreami.ch. Generating that site takes at least 2 or 3 seconds each time you hit save - that is too long for the few pages it has. Hugo now does this in 42ms:

    Built site for language en:
    0 draft content
    0 future content
    0 expired content
    67 regular pages created
    12 other pages created
    2 non-page files copied
    15 paginator pages created
    1 series created
    0 tags created
    total in 42 ms

which is very impressive.