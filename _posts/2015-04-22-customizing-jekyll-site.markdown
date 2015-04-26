---
title:  "Creating this Jeykll Site"
date:   2015-04-22 19:54:11
level: "Entry Level"
tags: "Ruby, Bash, Html, CSS3"
---
I created this walkthrough of my [Jekyll powered site][mysite] while I created it. 

To kick this off I need to install the Jekyll gem. 

{% highlight bash %}
gem install jekyll
{% endhighlight %}

I plan to deploy this project to my [ra_page][ra_page] git repo, so I'll go ahead and create a Gemfile as [recommended][recommended].

{% highlight ruby %}
source 'https://rubygems.org'

require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'github-pages', versions['github-pages']
gem 'github-markdown'
{% endhighlight %}

I saved the Gemfile inside my project directory and from there I can tell Bundler to download and install dependencies. Nice!

{% highlight bash %}
bundler install 
{% endhighlight %}

Well that was simple. Now I just need to create a new project. 

{% highlight bash %}
bundler exec jekyll new .
{% endhighlight %}

It's all working like I wanted now and with the next command my page will keep updating @ [http://localhost:4000/][local] each time I make changes to any files.

{% highlight bash %}
bundler exec jekyll serve
{% endhighlight %}

Cool! My page is showing and now I'm gonna start updating the layout and then add some new styling effects. I want the layout to have a fixed header at the top to show a title and maybe some links, a floated left sidebar with links to prjojects by language and a right content view to show pages and posts. 

I created a header.html template, a sidebar.html teplate, and edited the rest of the files that were created with this new project. Namely the [_layout.scss][layout]

{% highlight html %}
header.html
<header class="site-header">
  <a class="site-title" href="#">
    Ryan-Alex.com |
  </a>
  <a class="site-title" href="#">
     Resume
  </a>
</header>

sidebar.html
<div class="site-sidebar">
  <div class="inner-sidebar">
    <div class="sidebar-media">
      <!-- my rounded selfie -->
      <img src="/img/selfie.jpg">
      <ul class="social-media-list auto-margin">
        <li class="inline-list">
          <!-- round icon links -->
        </li>
      </ul>
    </div>
    <div class="sidebar-links">
      <ul><!-- project links --></ul>
    </div>
  </div>
</div>
{% endhighlight %}

What is a layout without content? First, I want a list of links to pages for each language I have posted about to automatically appear in the sidebar. To do that I need a way of telling Jekyll about my posts. Jekyll provides TAGS and CATEGORIES. Both of them are lists and both of them are global variables by default. What if I create a reference page for each language I have written about and use that page to link to related posts? I know that is a bit hacky, but it will save some overhead by not forcing a query on each reload. Ill try it out. 

{% highlight html %}
Created cloud.md
---
layout: project
title: Obj-C
type: subject
---

Added a category to 2015-04-22-creating-storyboard-contrains.markdown
---
title:  "Creating UIStoryboard constraints"
date:   2015-04-22 20:54:11
category: Obj-C
---

Finally I updated the sidebar.html
<div class="sidebar-links">
      <div class="trigger">
        <ul class="left-margin-10">
          <!-- for page in site.pages -->
            <!-- if page.type == "subject" --> 
              <li class="top-border-2 pad-10 border-light-blue"><a class="page-link white-link" href="">Cloud</a></li>
              <li class="top-border-2 pad-10 border-light-blue"><a class="page-link white-link" href="">Go</a></li>
              <li class="top-border-2 pad-10 border-light-blue"><a class="page-link white-link" href="">Javascript</a></li>
              <li class="top-border-2 pad-10 border-light-blue"><a class="page-link white-link" href="">Obj-C</a></li>
              <li class="top-border-2 pad-10 border-light-blue"><a class="page-link white-link" href="">Python</a></li>
            <!-- endif -->
          <!-- endfor -->
        </ul>
      </div>
    </div>
  </div>
{% endhighlight %}

Now that is kinda cool. When I click on one of the sidebar links, a page is loaded containing a list of page links matching the page.type

That about wraps it up. I can now just create a post and push the changes to my git repo and like magic, my page is updated. 

The last thing todo is to make sure credit is given where it is deserved, so I will go ahead and add this to the footer. Thank you all! 

{% highlight html %}
<footer class="site-footer">
  <div class="wrapper">
    <div class="footer-li-wrapper">
      <p class="text">This site was created using Jekyll and it is hosted in a Github Pages page | 2015 Ryan-Alex.com</p>
  </div>
</footer>
{% endhighlight %}

[local]:       http://localhost:4000/
[mysite]:      http://ryan-alex.com/
[jekyll]:      http://jekyllrb.com/
[gh-pages]:    https://pages.github.com/
[ra_page]:     https://github.com/MrRyanAlexander/mrryanalexander.github.io/
[recommended]: http://jekyllrb.com/docs/github-pages/
[layout]:      https://github.com/MrRyanAlexander/mrryanalexander.github.io/blob/master/_sass/_layout.scss