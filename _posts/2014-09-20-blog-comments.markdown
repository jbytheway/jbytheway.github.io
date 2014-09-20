---
layout: post
title: "Blog comments"
commentIssueId: 2
tags: blog
---

Disclaimer: This post is another self-referential post about creating this
blog.

As discussed [last time](/2014/08/10/metablogging), I was pondering how best to
add comments to this blog.

As I mentioned then, the only option seemed to be externally hosted comments
using e.g. [Disqus](https://disqus.com/).

I also had the idea of somehow redirecting my readers to make a pull request
against a special comments file using GitHub's online file editing feature.  I
thought this was a great idea, but luckily others have thought further than I.

A bit more searching found me [talaria](https://github.com/m2w/talaria), a
system where comments can be attached to git commits and pulled from there into
the post through the GitHub API.

This was pretty awesome already, but there seemed to be some concerning
limitations and gotchas.  I [asked the
author](http://blog.tibidat.com/2013/03/26/writing-a-github-hosted-commenting-system/)
through this very commenting system and he tipped me off to another
alternative: [exploiting GitHub issue
comments](http://ivanzuzak.info/2011/02/18/github-hosted-comments-for-github-hosted-blogs.html).

The downside of this is the need to create an issue and link it somehow to the
blog post, but it seems the better option for now.

I've [implemented
it](https://github.com/jbytheway/jbytheway.github.io/blob/master/_includes/comments.html),
cribbing shamelessly from [izuzak's
implementation](https://github.com/izuzak/izuzak.github.com/blob/master/_layouts/post.html)
and later from
[qwertie's](https://github.com/qwertie/Loyc/blob/gh-pages/_includes/comments.html),
and it worked!

Except not on my primary Firefox.  At first I blamed
[NoScript](http://noscript.net).  But it was odd that it worked when hosted
locally (using [jekyll --serve](http://jekyllrb.com/docs/usage/)) and on
[izuzak's
blog](http://ivanzuzak.info/2011/02/18/github-hosted-comments-for-github-hosted-blogs.html),
or if I used Opera, but not form me on
[github.io](https://jbytheway.github.io/2014/08/10/metablogging/) through
Firefox.  This didn't really fit with NoScript being to blame, and if NoScript
broke AJAX this fundamentally, I'm pretty sure there would be complaints all
over the Internet about it.  There aren't.

I was finally clued in to what was going on when I was poking about in the
Firefox inspection tools.  In the console there were warnings about mixed
content.  they led me to [this
page](https://developer.mozilla.org/en-US/docs/Security/MixedContent)
explaining the problems of loading javascript over http in an https page.
Switching all the content links over to https did the trick.

Learning about the [GitHub API](https://developer.github.com/v3/) was
interesting.  I am somewhat confused, however, about the [OAuth
situation](https://developer.github.com/v3/oauth/).  Both the above commenting
solutions claim that it is required to register a OAuth application, and yet
the documentation of OAuth on GitHub seems unrelated to the straightforward API
calls being used.  And it seems to be working without that, even when served on
localhost.

I also spent some time improving the layout of the site, and wrote my first
ever CSS, including (already!) a browser-specific workaround.

This was my first foray into web programming.  It was fun to get my toes wet,
but I'm not inspired to want to do this as a day job...

With luck, I may now be able to blog about something other than blogging.
