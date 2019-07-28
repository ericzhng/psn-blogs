---
layout: post
title: "Use tensorflow model API in Google Colaboratory"
modified:
categories: blog
excerpt:
tags: [PyCharm, Windows, Tensorflow, Google Colab]
image:
  feature: google/colab-tensorflow.jpg
date: 2018-10-13
comments: true
share: true
---

## Introduction

This posts shows an alternative to run tensorflow, which is using the free google Colaboratory platform. You can run both the CPU and GPU versions there.

<!--more-->

I've had a hard time to make tensorflow run on my Windows PC. I was able to install it successfully, but whenever I execute `import tensorflow as tf` in my python, I got errors saying "DLL file not found". I was able to use tensorflow 1.1.0 successfully before, but new versions seem to have this issue all the time. There is a fix now, please refer to my new post titled "Install Tensorflow (CPU) in PyCharm in Windows".

I gave up on installing tensorflow on my Windows PC, and tried to seek some alternatives. I figured out google Colaboratory could faciliate my learning, so I gave it a try, and it works pretty well.

Two things of interest to me are:

* How do I import other third party and custom packages in google colab?

* How do I read large numbers of data files from google drive?

Please feel free to contribute if you want.
