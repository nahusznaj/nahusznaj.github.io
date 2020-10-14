---
layout: article
title: Setting up an alias for ngrok
categories: learning
modified: 2020-10-07T16:28:11-04:00
tags: [git]
comments: true
share: true
read_time: true
---

ngrok is awesome. If you download it from <https://ngrok.com/download> and follow the instructions, you'll still need to run in your terminal:

```
$ ./ngrok http {portNumber}
```

from the folder that you have the file unzipped in. I unzipped it in ~/Downlaods folder (for no specific reason).

Here's the trick to make this more efficient. You can use `alias` in your terminal.

Example: 
```
~$ alias ddd='cd ~/Downloads'
```

Then, when you run `ddd` anywhere in your terminal, the alias means that bash will actually run `cd ~/Downloads`, changing directory to the Downloads folder.

The trick is to chain commands so that, whenever you type `ngrok command` in your terminal, it'll go to /Downloads and run `./ngrok command`.

And we want this permanently. So, we'll need to write the alias in the `.bash_profile` file.


Let's do this.

Open a terminal and in your home folder open the `.bash_profile` file, you can use `nano`:

```
~$ nano .bash_profile
```

Add the following line to your bash profile:


```
## ngrok alias
alias ngrok='cd ~/Downloads/ && ./ngrok'
```

and save it (if you are using nano, hit `control+X` and then `Y`).

Then, source the file:
```
~$ source .bash_profile
```
You're good to go! To test, go adhead and type `ngrok http 3000` to open a tunnel on port 3000 from your localhost. Or any other ngrok command. See (ngrok docs)[https://ngrok.com/docs].