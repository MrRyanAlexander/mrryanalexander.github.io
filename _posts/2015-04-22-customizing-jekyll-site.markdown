---
title:  "This Jeykll Site"
date:   2015-04-22 19:54:11
---
I created this walkthrough of my [Jekyll][mysite] while I created it. 

To kick things off I gotta create a new project. 

{% highlight bash %}
jekyll new blog
{% endhighlight %}

Now I'm gonna start serving my project locally and preview updates @ http://localhost:4000/.

{% highlight bash %}
jekyll serve
{% endhighlight %}

Now that I have my new project working I'm gonna start updating the layout and then add some new styling effects. I want the layout to have a fixed header at the top to show a title and maybe some links, a floated left sidebar with links to prjojects by language and a right content view to show pages and posts. 

Now I have a sidebar without content. Later I will add some to finish this project. 

{% highlight html %}
<header class="site-header">
  <a class="site-title" href="#">
    Ryan-Alex.com</a>
</header>

<div class="site-sidebar">
  <div class="inner-sidebar">
    <div class="sidebar-media">
      <!-- my rounded selfie -->
      <img src=""img/selfie.jpg"">
      <ul class="social-media-list auto-margin">
        <li class="inline-list">
          <!-- round icon links -->
        </li>
      </ul>
    </div>
    <div class="sidebar-links">
      <ul>
      <!-- project links -->
      </ul>
    </div>
  </div>
</div>

<div class="post">
  <header class="post-header">
    <h1 class="post-title">This Jekyll Site</h1>
    <p class="post-meta">2015-04-22 19:54:11 • Ryan Alex • getting started kickoff</p>
  </header>
  <article class="post-content">
    <!-- content -->
  </article>
</div>
{% endhighlight %}

That is it. Oops wait a minute, I almost forgot to say thanks by adding a footer and linking back to the people who deserve credit for creating the tools I am using to create this project. 

{% highlight html %}
<footer class="site-footer">
  <div class="wrapper">
    <div class="footer-li-wrapper">
      <p class="text">This site was created using Jekyll and it is hosted in a Github Pages page | 2015 Ryan-Alex.com</p>
  </div>
</footer>
{% endhighlight %}


[mysite]:      http://ryan-alex.com/
[jekyll]:      http://jekyllrb.com/
[gh-pages]:    https://pages.github.com/