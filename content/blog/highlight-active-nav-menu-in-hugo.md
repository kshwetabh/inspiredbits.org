---
title: "Highlight Active Nav Menu in Hugo"
date: 2018-12-18T17:38:45+05:30
summary: "How to highlight the current tab in Hugo theme"
description: TL;DR Here's a snippet to easily enable current tab highlighting in your hugo theme.
tags: [hugo]
---
After applying the <a href="https://html5up.net/editorial" target="_blank">Editorial theme</a> to my website, I found that the menu item for the current page is not being highlighted. With some fiddling I was finally able to implement it with Go logic. 

If you want to implement this for your theme/website, locate the code that actually renders the site menus. In the Editorial theme, it was present in layouts/partials/nav.html file (please note this might vary for different themes, just search for .Site.Menus.main in your theme files and you should be able to easily locate it).

In the below code snippet notice the lines highlighted (5, 9 and 20). In line #5, I am splitting the URL (eg. https://inspiredbits.org/post) to get the page name (eg. post, projects, contactme, etc.). Once I have the page name, I am applying `active` class to the `<li>` element if the current menu (returned by a nice inbuilt `$.IsMenuCurrent` page method provided by hugo) object returns the same current page object. `active` class then highlights the menu for the current page.

There you have it. A simple Go template implementation to solve the current page tab highlighting issue.

<div class="code">
{{< highlight html "linenos=table,hl_lines=8" >}}
  <div class="menu">
      <ul>
          {{ $currentNode := . }}
          <!-- apply active class to the current tab -->
          {{- $firstUrlElement := print "/" (index (split .URL "/") 1) -}}
          {{ range .Site.Menus.main }}              
              <!-- Single level menus -->
              <li><a href="{{.URL}}" class="{{if or ($.IsMenuCurrent "main" .) (eq ($firstUrlElement|lower) (.URL|lower)) }}active{{end}}">{{ .Name }}</a></li>
          {{ end }}
      </ul>
  </div>
  {{< / highlight >}} 
</div> <!--code-->