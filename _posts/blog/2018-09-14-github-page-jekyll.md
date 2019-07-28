---
layout: post
title: "Setup Jekyll for GitHub Page in Windows WSL"
categories: blog
excerpt:
tags: [Jekyll, WSL, Website]
image:
  feature: web/github-jekyll.jpg
date: 2018-09-14
comments: true
share: true
---

In this blog, I want to talk about how to set up Jekyll in Windows 10 and generate static web pages to host on GitHub page. There are three major steps you should follow in order to successfully use Jekyll.

<!--more-->


## 1. Set up Linux subsystem in Windows 10
* Please refer to my post titled "Setup Linux environment (WSL) in Windows" to setup WSL in Windows 10.

## 2. Install all necessary files for Jekyll in WSL
* Open WSL Bash in Windows 10, and update our repo lists and packages
	`sudo apt-get update -y`
	`sudo apt-get upgrade -y`

* (Optional) Add the repository from BrightBox, which has an optimized Ruby version in Ubuntu.
   `sudo apt-add-repository ppa:brightbox/ruby-ng`

* Before we install Jekyll, we need to make sure we have all the required dependencies.
  `sudo apt-get update`
  `sudo apt-get install build-essential patch ruby ruby-dev zlib1g-dev liblzma-dev dh-autoreconf`

* Update Ruby gems
  `sudo gem update`

* Install Jekyll
  `sudo gem install jekyll bundler`

* Test whether Jekyll is installed successfully
  `jekyll -v`

* Install all of the required gems
  `bundle install`

## 3. Build your local Jekyll site forked from GitHub

* Open cmd, and type `bash` to get in Bash environment.

* In Bash, navigate to the root directory of your local Jekyll site repository.

* Run following command to run the Jekyll site:
  `bundle exec jekyll serve`

* Preview the changes in your web browser at "localhost:4000".

## (optional): install Ruby w/ Devikit:

* Download Ruby w/ Devikit from https://rubyinstaller.org/downloads/

* Run the 'ridk install' step on the last stage of the installation wizard. This is needed for installing gems with native extensions. You can find addtional information regarding this in the RubyInstaller Documentation

* Open a new command prompt window from the start menu, so that changes to the PATH environment variable becomes effective. Install Jekyll and Bundler via: `gem install jekyll bundler`


## Some common issues:

### Eror when running `jekyll -v`:
* "You have already activated public_suffix 3.1.0, but your Gemfile requires public_suffix 2.0.5. Prepending `bundle exec` to your command may solve this. (Gem::LoadError)"


* You should add bundle exec before every jekyll command.

### Error when running `bundle exec jekyll serve`:
* "Could not find minitest-5.11.3 in any of the sources. Run `bundle install` to install missing gems."

* This is most probably you forget to execute last command in Step 2. Type `bundle install` in Bash and execute. You may be required to input your password.

### Error when running `bundle install`:
* "Gem::Ext::BuildError: ERROR: Failed to build gem native extension. An error occurred while installing nokogiri (1.8.4), and Bundler cannot continue. Make sure that `gem install nokogiri -v '1.8.4' --source 'https://rubygems.org/'` succeeds before bundling."

* First install nokogiri by itself in Linux subsystem ('sudo gem install nokogiri'), then try "bundle install" again!

Reference:
------

1. [How to Enable the Linux Bash Shell in Windows 10](https://www.laptopmag.com/articles/use-bash-shell-windows-10)
2. [Setting up your GitHub Pages site locally with Jekyll](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)
3. [Jekyll on Windows](https://jekyllrb.com/docs/installation/windows/)
