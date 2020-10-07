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

ngrok is awesome. If you download it from https://ngrok.com/download and follow the instructions, you'll still need to run in your terminal:

```
$ ./ngrok http {portNumber}
```

from the folder that you have the file unzipped in. I unzipped it in ~/Downlaods folder (for no specific reason).

Here's the trick to make this more efficient. You can use `alias` in your terminal.

Example: 
```
~$ alias ddd='cd ~/Downloads'
```

Then, when you run `ddd` anywhere in your terminal, it'll run `cd ~/Downloads` and you'll navigate to the Downloads folder.

The trick is to chain commands so that, whenever you type `ngrok command` in your terminal, it'll go to /Downloads and run `./ngrok command`.

And we want this permanently. For this, you can write it in your `.bash_profile` file.

Navigate to this file in your home directory:

```
~$ nano .bash_profile
```

add this line to your bash profile:


```
## ngrok alias
alias ngrok='cd ~/Downloads/ && ./ngrok'
```

and save it (if you are using nano, hit `control+X` and then `Y`).

Then source the file:
```
~$ source .bash_profile
```
Then you're good to go.

Type `ngrok http 3000` to open a tunnel on port 3000 from your localhost. Or any other ngrok command. See https://ngrok.com/docs.