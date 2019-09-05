---
title: "How to Configure Hugo Site With Github Pages for Custom Domain"
date: 2018-12-24T09:59:47+05:30
description: "TL;DR This post walks through the specific configuration required in Hugo's config.toml file to setup custom domain on GitHub.com."
tags: [hugo, github]
---

Hosting a static site on Github is pretty easy but there are some obscure configurations needed to get everything setup properly. This post walks through few of those for setting up hugo generated site with Github.

Hugo's official documentation on how to <a href="https://gohugo.io/hosting-and-deployment/hosting-on-github/" target="_blank">Host on GitHub</a> has almost all the details that is required to configure Hugo and successfully host your static website on GitHub Pages. I got lost in the custom domain step on which the page does not have much details, except setting up the CNAME file. It then defers to the <a href="https://help.github.com/articles/using-a-custom-domain-with-github-pages/" target="_blank">official Github page </a>for any custom domain configuration.

### Let's start with config.toml
I struggled quite a bit with the **baseURL** config. The official Hugo page instructs to use `<USERNAME>.github.io/<PROJECT>/` whereas few online blogs and forums mentions to use `https://<USERNAME>.github.io/<PROJECT>/` or `//<USERNAME>.github.io/<PROJECT>/`. I tried all of these in vain but then with some hit and trial (and realization in hindsight) that using **`https://inspiredbits.org/`**, *the actual domain name*, only makes sense. No need to specify github project URL or anything else.

This might be obvious to others, but I struggled and thought to put it out to the world to save others from going through this.

<div class="code">
{{< highlight toml>}}

baseurl = "https://inspiredbits.org/"	#config for github pages
publishDir = "docs"                     #config for github pages

theme = "hugo-editorial"
# Define the number of posts per page
paginate = 9
date_format1 = "Jan 2, 2006" #this config is not working
DefaultContentLanguage = "en"
{{< / highlight >}}
</div>   

### Entry into CNAME file
This file should have the domain name entry without any **http**, **https** or **www** protocols or prefixes.

<div class="code">
{{< highlight toml>}}
inspiredbits.org
{{< / highlight >}} 

And that's all you need. Make sure to enable HTTPS support as it comes for free with GitHub Pages hosting and Chrome won't flag your site as insecure. You will find it under project Settings &rarr; GitHub Pages sections &rarr; **Enforce HTTPS**.