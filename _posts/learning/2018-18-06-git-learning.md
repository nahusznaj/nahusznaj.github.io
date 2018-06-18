---
layout: article
title: Using Git and Github
categories: learning
modified: 2018-06-18T16:28:11-04:00
tags: [git]
comments: true
share: true
read_time: true
---

I tend to internalise what I learn when I am able to write it down or explain it to someone else.

I recently learned how to create/clone/download/edit repositories in git/github. I'm no expert. So I want to have this written down for a while.


1. Create a new repository on github, say named `my_new_repo`

2. Create a folder in your local directory.

3. Initialise a git bash in the local directory and run:


`$ git init`

`$ git config --global user.name 'Your Name' `

`$ git config --global user.email 'Your@email.com'`

`$ git remote add origin https://github.com/GITHUB_USERNAME/my_new_repo.git`

At this point, your local directory will be able to push files into the repository just created.

So, open your text editor (I'm using Atom).




