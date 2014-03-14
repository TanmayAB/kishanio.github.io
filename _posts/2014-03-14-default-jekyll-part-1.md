---
layout: post
title: Getting started with Jekyll (Part 1)
---

##Motivation
I needed a blog. Turns out for me blogging platform is very important.  

##Research
With that i narrowed myself down to following list, with reasons combined to reject it.


1. [Ghost](http://ghost.org) - Written in [Node.js](http://nodejs.org) but too mainstream. 
2. [Scriptogr.am](http://scriptogr.am) - You can have your blog files inside [Dropbox](www.dropbox.com). Well that sounds good but i am not that of a Dropbox user too. Just didn't turn me on. 
3. [Jekyll](http://jekyllrb.com) - [Chosen one](http://swfanon.wikia.com/wiki/Prophecy_of_the_Chosen_One). Of-course one line reason won't be enough to describe it. 


**Reasons** for choosing Jekyll,

+ Dead Simple.
+ Developer friendly. 
+ [Ruby](https://www.ruby-lang.org). - If in-case i ever wrote any scripts to do fancy things. 
+ [Markdown](http://daringfireball.net/projects/markdown/). - Giving up old WSIWYG editors and moving on to good formating tools.
+ GIT. - Recently my life is revolving around Write. Commit. Push. For those who don't know, git is a system that allows you to keep versions of code. [Read here](http://git-scm.com).
+ Github Pages. - We can deploy markdown directly to a free hosted platform provided by github. Was sold. [All hail Github](http://pages.github.com).
+ [Plugins](http://jekyllrb.com/docs/plugins/). - Drop in extensions that could enhance functionality without changing the internal structure of an application. You can almost have all the function that you would expect from a blog. 
+ Syntax Highlighting - It has a built in syntax highlighting for almost every language/code i use. [Demo](http://pygments.org/demo/290833/) 


**What is Jekyll?**

[Jekyll](http://jekyllrb.com) is a [Ruby](https://www.ruby-lang.org) parser bundled in form of a [gem](http://rubylearning.com/blog/2010/12/14/ruby-gems-—-what-why-and-how/). It is used to built static websites.


**Usage**

I will be setting this up for Mac OS X 10.9. Though its intended for any [Unix](http://www.bell-labs.com/history/unix) based system. 

Pre-requistes: 

1. [Ruby](https://www.ruby-lang.org/en/downloads/) (Most of the system has it pre-installed)
2. [GIT](http://git-scm.com/book/en/Getting-Started-Installing-Git). Since we will be hosting it on [Github](github).

Navigate to your project folder. And fire up the following command. This will install jeykll and all its dependencies.  

```bash
	$ gem install jekyll
```
	
Thereafter we will create a new Jekyll project using.

```bash
	$ jekyll new myblog && cd myblog
```
    
Naviagate to myblog directory and hit the following command to start a webserver. 

```bash
	$ jekyll serve 
```

Serve command has lots of useful flag. One the most important one is `jekyll serve -w`. This keeps watch on the directory and updates everytime any file is changed.

Jeykll has the following directory structure which is self explaintory. 

	
```bash
myblog
├── _config.yml
├── _layouts
│   ├── default.html
│   └── post.html
├── _posts
│   └── 2014-03-14-welcome-to-jekyll.markdown
├── css
│   ├── main.css
│   └── syntax.css
└── index.html
```
	

Everytime we run `jeykll serve` a `_site` folder is created that has our parsed blog.


Thats pretty much it. You can create a new post by creating a file in the `_posts` folder in following format.

```bash
<year>-<month>-<day>-name-of-article.md
```

**Deploy**

We will use [Github pages](http://pages.github.com) to deploy our blog. Its a free service provided by Github under .io domain. 

To get started create an empty github directory with name same as your username.

Github has an auto-generator that keeps account of the repositiers under your username and deploys them to <username>.github.io/

Note this username repository needs to have Jekyll source because Github is constrained to same. 

Thereafter just initialize git in your local directory. 

```bash
$ git init
```

Copy the clone url from the newly created git repository and add it to remote 

```bash
$ git add remote origin <clone-url>
````

Thats it commit the changes and push it.

```bash
$ git commit -m "Initial Commit" && git push
```



