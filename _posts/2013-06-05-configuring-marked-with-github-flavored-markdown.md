---
layout: post
title: Configuring Marked With GitHub Flavored Markdown(ish)
date: 2013-06-05 03:15
comments: true
external-url:
categories: [osx, markdown, apps]
---
I prefer to write things almost exclusively using the Markdown format. It's
pretty great and if you're reading this, chances are you think so too.

There are a plethora of tools out there to help you visualize what the output of
your fancy Markdown document will turn into once a parser runs over it and spits
out HTML, but the two I've used the most are [Marked](http://markedapp.com) and
[Mou](http://mouapp.com/); both for OS X.

Mou is a stand-up candidate for a primary Markdown visualizer, but I ran into
more than a few odd little bugs here and there when I was using it. Namely,
poor support or glitchy behavior for extended Markdown formatting (tables and
junk). When the extended features were supported, I found that I didn't quite like the
way Mou was implementing them, so I switched to a recommendation of my
co-worker, [Jeff Eaton](http://lbt.me/eaton), called Marked. Don't let that
dissuade you from using Mou though, it's fantastic in a lot of other ways.

Marked too had some funky issues, but happily, provides a way to configure the
parser it runs on. In fact, you can configure your own entirely, which is what
this article is really about. One thing I think most people who switch from Mou
to Marked miss is the ability to edit and preview in the same application. For
me, the enhanced configuration abilities outweigh the annoyance of
getting used to writing exclusively in Vim again.

You may have noticed in the title the acronym **GHFM**. I use that to stand for
[GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown)
which is a fancy Markdown variant which GitHub uses. Since a lot of what I write
ends up on GitHub, it makes sense to try and emulate GHFM locally.

In addition to GHFM, I'm also becoming increasingly attached to some of the
Markdown features from the [PHP Markdown Extra](http://michelf.ca/projects/php-markdown/extra/) project.
Support for things like tables and footnotes are fantastic additions to the
Markdown toolset.

So, with all this hodgepodge of extra Markdown stuff, what exactly can we
replicate locally? Here's a summary:


Feature                                | Working with Marked? | Source
-------------------------------------- | -------------------- | ----------------
Abbreviations                          | no                   | Markdown Extra
Definition lists                       | no                   | Markdown Extra
Fenced code blocks                     | yes                  | -
Footnotes                              | no                   | Markdown Extra
Inline HTML                            | yes                  | Markdown Extra
Markdown inside HTML blocks            | no                   | Markdown Extra
Multiple underscores in words          | yes                  | GHFM
Newlines (via 2x space at end of line) | yes                  | GHFM
URL autolinking                        | yes                  | GHFM
Special attributes (ids, classes)      | no                   | Markdown Extra
Syntax highlighting                    | yes                  | -
Tables                                 | yes                  | Markdown Extra
Task Lists                             | no                   | GHFM

Obviously the list isn't complete, but we have the majority of the GHFM
extensions and 1/2 of the most important contributions from Markdown Extra
(Tables and Footnotes).

Even missing a few, that's a ton of extensions. With GHFM and Markdown Extra
syntaxes in the mix, there are 5+ ways to write a header!

Da-yum!

To help keep things
consistent, I wrote myself a [Markdown Style
Guide](https://github.com/carwin/markdown-styleguide) which you should
definitely fork for your own uses or flatter me and just use as-is.

So, now that we know what our capabilities are, let's get down to business:

## 1. Install the `pygments` library for syntax highlighting.

[Pygments](http://pygments.org) is a generic syntax highlighter written in
Python and supports a wide variety of languages, including
[Brainfuck](http://www.muppetlabs.com/~breadbox/bf/) which is pretty hardcore.
We'll have our redcarpet settings use this for syntax highlighting later on.

`sudo easy_install pygments`

### Check if `pygmentize` bin is in your user $PATH:
Type `pygmentize`. If you get an error, update your $PATH in one of two ways:

### _Update your shell $PATH_

I use ZSH, so these instructions use `~/.zshrc` as a generic example. You
should use whatever is appropriate for your setup: `~/.bashrc`,
`~/.zshenv`, etc...

To explicitly add `pygmentize` to your $PATH via `.zshrc`, first locate
`pygmentize` via  `which pygmentize` or `locate pygmentize`.

If the `pygments` library is actually installed, one of the above commands
should have returned a POSIX path to the bin, which probably looks
something like this:

{% highlight bash %}
/usr/bin/pygmentize
/usr/local/bin/pygmentize
/wherever/you/installed/pygmentize
{% endhighlight %}

Once you have the path, crack open your `~/.zshrc` and append:

{% highlight bash %}
export PATH="$PATH:/wherever/you/installed/pygmentize"
{% endhighlight %}

### Symlink `pygmentize` to somewhere that _IS_ in your $PATH:

There's a good chance that the directory `/usr/bin/` is in your user's
$PATH. So following the steps from above to locate where `pygmentize`
actually got installed, create a symlink from there to `/usr/bin`
or `/usr/local/bin`:


{% highlight bash %}
ln -s /wherever/you/installed/pygmentize /usr/bin
{% endhighlight %}

or

{% highlight bash %}
ln -s /wherever/you/installed/pygmentize /usr/local/bin
{% endhighlight %}

## 2. Install Some Shiny Gems

OS X comes pre-packaged with Ruby and `rubygems` so you shouldn't run into any
trouble here. There's a chance you may have to prepend `sudo` to these commands
depending on how you have your environment configured, but that's not the end of
the world by any stretch.

We need 2 gems for GitHub flavored goodness:

  * The [Redcarpet 2](https://github.com/vmg/redcarpet) Ruby gem - A Ruby
    library for Markdown processing.

{% highlight bash %}
gem install redcarpet
{% endhighlight %}

  * The [Albino](https://github.com/github/albino) Ruby gem - _A Ruby
    parser for `pygments`._

{% highlight bash %}
gem install albino
{% endhighlight %}

## 3. Grab A Processing Script
Now that you've got all the fancy parts, you'll need to give Marked a way to
actually put them to good use.

To do that, you'll need a processing script to parse your Markdown since Marked
won't be handling it for you any longer.

Feel free to stretch your Google-fu muscles or enjoy a round of DucKDuckGo, but
to save you some time, nab the Ruby script I use and put it somewhere safe (I
keep mine in my [dotfiles](https://github.com/carwin/dotfiles)).

You can either copy paste it from the embedded gist below, or use `wget`/`curl`
if you're feeling fancy.

### Grab the Ruby parser

<details>
  <summary>Copy/Paste the embedded [gist](https://gist.github.com/carwin/5253509#file-ghfm-rb)</summary>
  <script src="https://gist.github.com/carwin/5253509.js"></script>
</details>

or

{% highlight bash %}
wget https://gist.github.com/carwin/5253509/raw/b5379abca8ae20ab6ea5e9415531f2e763fcb0e1/ghfm.rb
{% endhighlight %}

Take a good look at the gist and read the comments to understand what is being
configured with each directive.

### Make the script executable:

{% highlight bash %}
chmod +x /path/to/the/script/ghfm.rb
{% endhighlight %}

**Disclaimer**: _I'm not the original author of this script, and I can't
remember it's original source, so if you're the author and you're pissed off
that I'm not giving you the Nerd Cred you deserve, feel free to write an angry
email about it._

## 4. Actually start configuring Marked

Now that all that preparation is out of the way, we can finally configure the
application. If you're thinking, "Good gravy Carwin, we're _still_ not
finished?!?" you're probably not alone. Hang in there, it's almost over.

Crack open Marked.app's settings and soak in the massive amount of config
options presented to you.

That's right.

_4. Panes._

After the initial shock of how complicated this application's config options are
wears off you can just clone my settings to get you up and running. I figure
you'll be tweaking these to your liking anyway so I'll avoid explaining each and
every parameter in the GUI and just show you what I'm using.

### Window
  * &#9744; Translucent in background
  * &#9744; Keep new windows on top
  * &#9744; Show word count for selection
  * &#9744; Show welcome panel on launch
  * Status bar: &#9745; Style picker &#9745; Word count
  * Edit With: whatever.app

![Marked.app Window Config]({{ site.url }}/images/marked--window--config.jpg)

### Behavior

#### MultiMarkdown

  * ~~&#9744; Disable "smart" typography~~
  * ~~&#9744; Markdown Compatibility mode~~
  * ~~&#9744; Disable header ID creation~~
  * ~~&#9744; Retain line breaks in paragraphs~~
  * ~~&#9744; Convert fenced code blocks~~
  * ~~&#9744; Process HTML files as Markdown~~
  * &#9744; Scroll to first edit
  * &#9744; Disable link popovers
  * Strip: &#9744; YAML Front Matter &#9745; MMD3 Metadata

#### Custom Processor _(hooray, time for that script!)_

  * &#9745; Custom Markdown Processor
  * Path: `/Wherever/You/Saved/That/Ruby/Script/From/Step/3`
  * Args: `<empty>`

![Marked.app Behavior Config]({{ site.url }}/images/marked--behavior--config.jpg)

### Style

Rather than list these settings out, I'll just say there's nothing to change in
the **Additional Features** since our script from Step 3 will take care of our
cool settings and options. You can configure your own custom CSS for previewing
your Markdown output here, but I just use the GitHub default style.

![Marked.app Style Config]({{ site.url }}/images/marked--style--config.jpg)

### Printing
I have yet to find myself wanting to print out a document I wrote in Markdown,
although surely that day will come now that I've mentioned it.

That said, I imagine these settings are sensible so I'll include them here for
the sake of completeness:

  * &#9744; Print table of contents
  * &#9745; Hide link highlights when printing
  * &#9744; Replace horizontal rules (`<hr>`) with page breaks
  * &#9745; Page break before footnotes
  * Add page breaks before: &#9744; H1 &#9744; H2

![Marked.app Style Config]({{ site.url }}/images/marked--printing--config.jpg)

## 5. Decide you don't like it after all and go watch T.V. or something

After you've finished 1-4 you should have a pretty primo Marked.app setup. I'll
wager that many of you will make it all the way to the end and decide it's not
_quite_ what you need and go looking for something else. I understand. Nerds are
picky.

You should take a break before you go a-hunting again though.

Seriously, rest up - this was a huge pain in the ass.
