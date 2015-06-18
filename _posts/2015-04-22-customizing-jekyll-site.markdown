---
title:  "Creating this Jeykll Site"
date:   2015-04-22 19:54:11
level: "Entry Level"
tags: "Web"
---
I created this walkthrough of my [Jekyll powered site][mysite] while I created it. 

To kick this off I need to install the Jekyll gem. 

{% highlight bash %}
gem install jekyll
{% endhighlight %}

I plan to deploy this project as my [github][ra_page].io page, so I'll go ahead and create a Gemfile as [recommended][recommended].

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
title: "Customizing this Jekyll Site"
date:   2015-04-22 20:54:11
level: "Mid Level"
tags: "Html"
---
{% endhighlight %}

Now that is kinda cool. Jekyl can see the pages I created for each language. When I click on one of the sidebar links, a page is loaded containing a list of page links with tags that match the page title. 

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