---
layout: post
title: "Metablogging: Poole and Pingbacks"
---

I have spent the last few months without ready access to my desktop PC.  I'm
one of those dinosaurs who still prefers, where possible, to use my desktop for
everything from listening to music to writing software.  In particular, without
access to my desktop I can't use Thunderbird and I lost access to all my
RSS feeds.

While thus stranded I was educated by a friend of mine on how to get
[YouTube](https://youtube.com) working reliably on my laptop without Flash
(short version: use [YouTube
Center](https://addons.mozilla.org/en-US/firefox/addon/youtube-center/)).  Thus
I was doomed to spend more time than is probably healthy distracted by largely
pointless video-watching.  Once I was over that, I decided to take this
opportunity to find some new feeds to follow.

That's how I finally found myself reading the [blog of an old
friend](http://www.drmaciver.com/blog/) and in particular a [post advocating
more blogging](http://www.drmaciver.com/2014/07/you-should-write-more/).
Finding myself with more free time than I am accustomed to, I have little
excuse not to heed this call.

I was faced with two problems: what to talk about, and how to talk about it.
Naturally I decided to turn one of these problems into a solution, and talk
about constructing a blogging platform.

Unsurprisingly, this seems to be a very popular blogging topic, so I won't
blame anyone for reading no more of this post.

My goals were:

* Write posts in gVim.
* Manage and publish posts through git.
* Not deal with hosting.

I first saw a hint that [one can publish to WordPress through
git](http://people.mbi.ucla.edu/leec/docs/gitpublish/tutorials/intro.html),
which is awesome, but soon I recalled the existence of [GitHub
Pages](https://pages.github.com/), and indeed there are a number of offerings
to host a blog there, all based on [Jekyll](http://jekyllrb.com/).

Jekyll is a static site generator specifically designed to support
&ldquo;blogging like a hacker&rdquo; with git and text editors in mind.

I encountered (in this order)

* [Jekyll Bootstrap](http://jekyllbootstrap.com/)
* [Jekyll Now](http://www.github.com/barryclark/jekyll-now)
* [Poole](https://github.com/poole/poole)
* [Octopress](http://octopress.org/)
* Even the [original announcement of
Jekyll](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)!

and eventually settled on Poole, for a few reasons:

* I found several mentions of it.
* It seems to strike a nice balance between providing the features I want and
  not providing those I don't.
* It appears to be actively (or at least recently) maintained.

I cloned the Poole repo and started playing from there.  I could tell you the
rest, but by the time you can read this my commit history ought to tell the
story better than I can, so you might as well look there (all being well, there
should be a link to the repository in the sidebar).

One serious concern remains.  There is some debate as to solution for
commenting and feedback on a static blogging platform.  In some places it is
even [considered
harmful](http://dumbmatter.com/2011/08/jekyll-and-other-static-site-generators-are-currently-harmful-to-the-free-open-source-software-movement/).

The most common solution appears to be [Disqus](https://disqus.com/), a
proprietary service which keeps all of your comment data in their database.
This is the sort of thing I'm generally leery of, but what other option is
there?  The whole point of the simple static Jekyll website would be undermined
by trying to accept user commentary.  I don't want to manage a database, so
there is nowhere to put it (In fact I think there *is* somewhere to put it, and
I hope to discuss that in a future post).

Disqus provides for comments and I saw
some evidence of it catching mentions on Twitter, but I see hints that
[pingbacks and tracebacks are not
supported](http://theitbros.com/display-pingbacks-on-wordpress-posts-with-disqus-comment-system/).
This is a shame.  Especially since I don't even have a Twitter account.
Personally I think pingbacks are even more useful than regular comments.  I've
linked to four other blogs already in this post alone, and I would like to give
them due credit with a pingback.  I would also like to allow others to offer me
the same in the future.  Right now I'm not sure either of these is possible.  I
did find a [manual
pingback](http://software.hixie.ch/utilities/cgi/pingback-proxy/client-proxy.html)
page, which might solve one direction, but all my googling is for naught when
searching for a means to support pingbacks in a Jekyll blog.  Still, the
evidence is confusing and further research is required. Maybe if I actually get
the Disqus homepage to load (right now it seems rendered unrenderable by
[NoScript](http://noscript.net/)) I will discover that it does do what I want.
Or perhaps one of the [various
alternatives](https://news.ycombinator.com/item?id=6818416) will prove a better
fit.  For now I just want to see if this blog thing works at all...

As for the future of this blog?  My two past blogs have lasted for about 4 and
20 posts (neither are currently on the Internet).  Perhaps with an easier
publication channel I'll fare better.  Perhaps I'll abandon it as soon as I
have my desktop back in hand.  Perhaps I'll be inspired to [start using
beeminder](http://www.drmaciver.com/2014/07/playing-beeminder-on-hard-mode-by-adding-backpressure/)
to incentivise posting.  Only time will tell.

<!--
- **To bold text**, use `<strong>`.
- *To italicize text*, use `<em>`.
- Abbreviations, like <abbr title="HyperText Markup Langage">HTML</abbr> should use `<abbr>`, with an optional `title` attribute for the full phrase.
- Citations, like <cite>&mdash; Mark otto</cite>, should use `<cite>`.
- <del>Deleted</del> text should use `<del>` and <ins>inserted</ins> text should use `<ins>`.
- Superscript <sup>text</sup> uses `<sup>` and subscript <sub>text</sub> uses `<sub>`.

Most of these elements are styled by browsers with few modifications on our part.

## Heading

Vivamus sagittis lacus vel augue rutrum faucibus dolor auctor. Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.

### Code

Cum sociis natoque penatibus et magnis dis `code element` montes, nascetur ridiculus mus.

{% highlight js %}
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
{% endhighlight %}

Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa.

### Gists via GitHub Pages

Vestibulum id ligula porta felis euismod semper. Nullam quis risus eget urna mollis ornare vel eu leo. Donec sed odio dui.

{% gist 5555251 gist.md %}

Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum. Nullam quis risus eget urna mollis ornare vel eu leo. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sed odio dui. Vestibulum id ligula porta felis euismod semper.

### Lists

Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.

* Praesent commodo cursus magna, vel scelerisque nisl consectetur et.
* Donec id elit non mi porta gravida at eget metus.
* Nulla vitae elit libero, a pharetra augue.

Donec ullamcorper nulla non metus auctor fringilla. Nulla vitae elit libero, a pharetra augue.

1. Vestibulum id ligula porta felis euismod semper.
2. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
3. Maecenas sed diam eget risus varius blandit sit amet non magna.

Cras mattis consectetur purus sit amet fermentum. Sed posuere consectetur est at lobortis.

<dl>
  <dt>HyperText Markup Language (HTML)</dt>
  <dd>The language used to describe and define the content of a Web page</dd>

  <dt>Cascading Style Sheets (CSS)</dt>
  <dd>Used to describe the appearance of Web content</dd>

  <dt>JavaScript (JS)</dt>
  <dd>The programming language used to build advanced Web sites and applications</dd>
</dl>

Integer posuere erat a ante venenatis dapibus posuere velit aliquet. Morbi leo risus, porta ac consectetur ac, vestibulum at eros. Nullam quis risus eget urna mollis ornare vel eu leo.

### Images

Quisque consequat sapien eget quam rhoncus, sit amet laoreet diam tempus. Aliquam aliquam metus erat, a pulvinar turpis suscipit at.

![placeholder](http://placehold.it/800x400 "Large example image")
![placeholder](http://placehold.it/400x200 "Medium example image")
![placeholder](http://placehold.it/200x200 "Small example image")

### Tables

Aenean lacinia bibendum nulla sed consectetur. Lorem ipsum dolor sit amet, consectetur adipiscing elit.

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Upvotes</th>
      <th>Downvotes</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Totals</td>
      <td>21</td>
      <td>23</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Charlie</td>
      <td>7</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

Nullam id dolor id nibh ultricies vehicula ut id elit. Sed posuere consectetur est at lobortis. Nullam quis risus eget urna mollis ornare vel eu leo.

-----
-->
