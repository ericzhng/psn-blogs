---
layout: post
title: "Setup Hexo in Windows or WSL"
modified:
categories: blog
excerpt:
tags: [Windows,Hexo,GitHub]
image:
  feature: web/github-hexo.png
date: 2018-10-13
comments: true
share: true
---

This post talks about how to setup Hexo in Windows and host a site in GitHub.

<!--more-->

## Install tools for Hexo

* Download and install lastest version of [Node.js](https://nodejs.org/dist/v10.16.0/node-v10.16.0-x64.msi).

* Install [git](https://git-scm.com/download/linux) if you haven't done so.

* Install Hexo:
`npm install hexo-cli -g`
`hexo init blog`
`cd blog`
`npm install`
`hexo g` # or `hexo generate`
`hexo s` # or `hexo server`
`hexo d` # or `hexo deploy`

* Create a new post
`hexo new "My New Post"`
