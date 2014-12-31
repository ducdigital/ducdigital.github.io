---
title: Is HTML5 helps with SEO?
description: HTML5 helps SEO or not and how to improve your blog with it's new syntax? I will give comparisons and guides.
tags: [html,seo,html5, github, jekyll]
category : seo
---

HTML5 is powerful, as we can make almost everything with the support of javascript. Still HTML5 is still a XML-base document no different than HTML4, but with the new specifications and new tags. This will helps SEO a lot.


## Jekyll + Github

It has been 2 years since I stop wring my previous blog on tech, or more precise, programming because a hosting company delete my host before. So now, the end of the year 2014, I decided to restart my blog from scratch on [Github Pages](http://pages.github.com/) with [Jekyll](http://jekyllrb.com/).

Seriously, this Jekyll is really useful. Just after 2 hours of work, I already have my base structure of the blog ready. If you guys want to pull the site, just go ahead and go to [Github](https://github.com/ducdigital/ducdigital.github.io). Just remember to not include my posts on your websites.

I will soon write a blog post about this jekyll and how it is useful.

HTML5
----

With the new version of HTML, now introduce lots of new tags like `<audio>`, `<video>`, `<section>`, `<header>`..., we are having a much more clear XML representation of website data than ever. I would like to focus on the following tags in this post on SEO:

- `<section>`
- `<article>`
- `<header>`
- `<footer>`
- `<nav>`
- `<main>`
- `<time>`
- `<link>`
- `<h1>`


{% highlight html %}
<article>
	<header>
		<h1> My post </h1>
		<time>01-01-1997</time>
	</header>
	<section>
		<h1> Chapter 1</h1>
		<p>My beautiful text</p>
	</section>
	<footer></footer>
</article>
{% endhighlight %}


{% highlight html %}
<section>
	<h1> Category </h1>
	<article>
		<h1>Article 1</h1>
	</article>
	<article>
		<h1>Article 2</h1>
	</article>
	<article>
		<h1>Article 3</h1>
	</article>
</section>
{% endhighlight %}

### `<section>` & `<article>`
This tag by definition from w3 is a **grouping of content**. You can group different `section` in an `article` or multiple `article` in a `section` like category.

### `<header>` & `<footer>`
`header` and `footer` is a block, refer to the heading of a section or body, you can use multiple times but once per level.
We can use it to differentiate the heading or footer of a post and it's body. Refer to the first example above for the usage of header and footer.

You can use this tag for the page header and footer too just like I did (view source)

### `<main>`
Main is the main content of the `<body>`, it can only be use one, so pick carefully which part of data on your website you want to be the main. *For example:* a blogpost page main should contain it's articles.

### `<nav>`
Nav is anything that helps user navigate to different page on the website. Let it be the navbar of your page, the sidebar navigation, or pagination, wrap this tag around it.

I also recommend use a list inside nav. IMO, it's better for the robot to crawl than bunch of divs stack together.

### `<time>`
Use the time on your article. Straight forward so the crawler don't need to guess.

### `<link>`
Give the permalink on your post for consistency purpose.

### `<h1>`
Why H1?
As of HTML5 we can have multiple H1 per document. H1 by default is the biggest heading for all sections, articles, footers, headers...

Schema.org
----
Schema.org is a markup volcabulary that helps search engines index easier the content of your website.

Let's improve the first example we have done above with schema.org included:

{% highlight html %}
<article itemprop="blogPost" itemscope itemtype="http://schema.org/BlogPosting">
	<header>
		<h1 itemprop="headline"> My post </h1>
		<time itemprop="datePublished" datetime="01-01-1997">01-01-1997</time>
		<link itemprop="url" href="/myblog/mypost/">
	</header>
	<section itemprop="articleBody">
		<h1> Chapter 1</h1>
		<p>My beautiful text</p>
	</section>
	<footer></footer>
</article>
{% endhighlight %}

So an article is now identify as a `blogPost`. Inside this `blogPost` we have `headline`, `datePublished`, `url`, and the `articleBody`. Pretty straight forward, right? By structure your html like this. Google can easily find which part of your document is the article and which is the heading. And the benefit? **SEO**

Backward compatible? Internet Explorer?
----
**IE8:** Not Support
**IE9:** Basic Support

My advice: **Screw IE**. Just kidding. You can use [this script (html5shiv)](https://github.com/aFarkas/html5shiv) for backward support on IE or browser not supporting these kind of tags

