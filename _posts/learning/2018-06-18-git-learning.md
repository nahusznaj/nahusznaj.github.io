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

I learned how to create/clone/download/edit repositories in git/github. I'm no expert so I want to have this written down for my own reference.


1. Create a new repository on github, say named `my_new_repo`

2. Create a folder in your local directory.

3. Initialise a git bash in the local directory and run:

  `$ git init`

  `$ git config --global user.name 'Your Name' `

  `$ git config --global user.email 'Your@email.com'`

  `$ git remote add origin https://github.com/GITHUB_USERNAME/my_new_repo.git`

  At this point, your local directory will be able to push files into the repository just created.

  So, open your text editor (I'm using Atom).

  Let's creat a markdown file file to have something to push into the repo.

  Go back to the git bash. You want to `add`, `commit`, and then `push` the changes (the creation of the file). This process will take the current files in the local directory (where you are editing, your laptop/PC) into the git repository. To do this three steps:

4. Run `$ git add .` This will add all the files in the current directory. (There are commands to select specific files, but I now want this to be simple and quick.)

`$ git commit -m 'a message describing what you are adding/changing'`

`$ git push -u origin master` This command will push the files just commited into the git repository at github that this local folder was instructed, by the git bash, to connect with. This was done when we run `$ git remote add origin https://github.com/GITHUB_USERNAME/my_new_repo.git` a few lines earlier.

So that's it. Then you can go to your browser and check that the files are actually there in the repo `my_new_repo`.

I learned how to do this watching this video on youtube: [Git & GitHub Crash Course For Beginners](https://www.youtube.com/watch?v=SWYqp7iY_Tc).

Another very useful source for learning these instructions is dataquest: https://www.dataquest.io/blog/how-to-share-data-science-portfolio/




