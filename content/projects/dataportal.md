---
title: "Dataportal"
date: 2018-10-06T13:47:45+05:30
draft: false
banner: ["projects/dataportal.png"]
description: "P.S: For obvious reasons, all the data shown in the above screenshot is mock data."
---

### What is Dataportal ?

A blazing fast search enabled content and artifact repository. The original target users were software development teams, the application can however be used by any team that needs storing contents and a way to access them fast. Users can store rich-text content, code snippets and different attachments without limitations. The application features full-text-search capability with search ranking (meaning more frequently accessed contents are ranked higher in the subsequent searches). It utilizes Go's builtin http server pacakage and hence is standalone and cross-platform.

### What's the stack used ?

Frontend is built in <a href="https://vuejs.org/" target="_blank">VueJS</a> and backend is implemented in <a href="https://golang.org/" target="_blank">Go</a> language. Frontend utilizes the single-page app design with multiple views, user access control and isolation by team.

Specifically below frameworks and libraries have been used:

- <a href="https://vuejs.org/" target="_blank">VueJs</a> with Vuex and Vue-router
- <a href="https://github.com/axios/axios" target="_blank">Axios</a> for handling ajax calls
- <a href="https://golang.org/" target="_blank">Go</a> programming language
- <a href="https://github.com/blevesearch/bleve" target="_blank">BleveSearch</a> for indexing and full-text-search
- Databases supported
    - Postgres SQL
    - SQLite3
    - MS Sql