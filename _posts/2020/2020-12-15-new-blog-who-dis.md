---
title: "New Blog Who Dis??"
author: Shawn
date: "2020-12-15"
categories: ["Blog"]
tags: ["Blog"]
---

You may notice I've completely overhauled the blog lately. Over the years this blog has been hosted 4 different places, and I'm hopeful this will be my last migration.

This time it's being hosted (for free!) on [Github Pages](https://pages.github.com/), which is a really neat little service by Github. Essentially they will allow you to serve HTML, CSS and JS files from one of your repository as a static website. And they support Jekyll compilation of Markdown and HTML templates into HTML pages as well. So you simply maintain your blog as a series of Markdown files. Easy!

Let's talk about some of the tech in the stack!

## Jekyll

[Jekyll](https://github.com/jekyll/jekyll) is an open-source blog-creation toolchain written in Ruby. It's designed by some of the developers of Github with Github Pages in mind, and has first-class support for concepts like tags, categories, pagination, table of contents, related articles, and templating.

## Markdown

Jekyll supports compiling markdown into HTML using markdown engines. There are a few markdown flavors supported, but the default is [Kramdown](https://kramdown.gettalong.org/).

Markdown is a very simple shorthand syntax for styling text on a webpage. You essentially write your text as you would in a word processor, but have the ability to use symbols to change the text style. Wrapping a word in asterisks (*) makes it *italic* - if you use two it becomes **bold**. Headers are denoted by beginning a line with pound (#) symbols. You can wrap a link in  and then follow it with a link in parenthesis [square brackets\]\(https://google.com\) to turn it into a hyperlink [like so](https://google.com).

Images can be embedded using the same symtax as a link, simply adding an exclamation mark to the beginning \!\[Like So\]\(/path/to/your/image.jpg\)

![Sunrise](/content/2020/12/sunrise.png)

It's also possible to embed HTML inline in Markdown, to embed things like Youtube videos or even links to other websites:

<iframe src="https://www.w3schools.com" style="height: 300px; width:400px;" title="W3Schools">
</iframe>

Most content you would want to embed in any blog is supported in a very simple syntax using Markdown.

## Frontmatter

Jekyll also supports [YAML](https://en.wikipedia.org/wiki/YAML) frontmatter, which is YAML-formatted metadata embedded at the head of a markdown file. This allows you to specify things like the date, author name, tags, etc. for a blog post.

![Frontmatter](/content/2020/12/frontmatter.png)

## Syntax Highlighting

Jekyll supports syntax highlighting for code blocks in your Markdown. The default syntax highlighter is [Rouge](https://github.com/rouge-ruby/rouge), which supports styling various languages using the [Pygments](https://pygments.org/) highlighting standard, which supports hundreds of languages and allows you a lot of customization to make your code look the way you want.

## Configuration

Configuration is done using YAML formatted config files. By convention the default config file is named `_config.yml` but it is also possible to include additional config files.

![Config File](/content/2020/12/config.png)

## Templating 

Templating allows you to define an HTML layout, and include various types of content inline. This allows you to have the same HTMl layout on all of your blog posts and pages, while allowing you to easily change it in the future if you like.

The templating engine used is [Liquid](https://shopify.github.io/liquid/) - a simple and powerful Ruby templating engine with support for embedding content, iterators, variable substitution, etc.

## Theme

And last but not least, you don't have to build your entire Jekyll site from scratch. There are a number of great [themes](http://jekyllthemes.org/) out there. But the one I settled on was [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/) - I really like its dark code editor-style theme and minimal, responsive layout. Kudos to its author for doing a really great job on it!

## Comments

Chirpy has built-in support for embedded comments using [Disqus](https://disqus.com/) - a comments-as-a-service company that has a really nice minimal UI and provides a lot of features like spam prevention, sharing, notifications, etc. that would be a lot of work to achieve in a home-rolled solution, and work great on a static website like this!

![Disqus](/content/2020/12/disqus.png)

## Conclusion

All told, Github has done a great job bringing all of these open source technologies together and combining them with a simple, but free service in Github Pages to make it really easy for someone familiar with markdown and Git to host a blog online for free!

This has worked out great for me since I was never truly happy with my old Wordpress site and hated having to pay a monthly fee for something I didn't love and rarely used.

I hope you enjoy the new and improved blog!