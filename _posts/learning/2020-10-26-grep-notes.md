---
layout: article
title: Using grep to search for a string pattern in files in a folder
categories: learning
modified: 2020-10-21T16:28:11-04:00
tags: [bash]
comments: false
share: true
---

I needed to review a large number of text files and pick those that included a string pattern. `grep` is awesome for this. 

I opened a terminal and navigated to the main directory folder where I had several subfolders and susbsequent sub-folders. There, I run a grep command and wrote the output in a `.txt` file.

```bash
~/mainFolder$ grep -H -r 'stringPattern' ~/mainFolder/ > ~/myTextFile.txt
```

The basic structure of the command is:

`grep [options] [regexp] [filename]`


From <https://en.wikipedia.org/wiki/Grep>, `grep` stands for "g/re/p (globally search for a regular expression and print matching lines)" and it's a command-line programme.

The options I used are:

- `-H`, which commands to print out the filename for each match. This is key as this will allow me to locate those files! And 
- `-r`, which sets the grep to be recursive, searching within sub-folders.

The regexp can be any regex, in my case, I used the literal string that I wanted to search, say `' 5'`, the number five.

The filename in this case is every file in the folder and sub-folders.

Finally, `>` is an extra that I added in order to write the output in a file, instead of returning it as standard output. For reference <https://askubuntu.com/a/420983>.


I used this as reference:  "A Beginner’s Guide To Grep: Basics And Regular Expressions" in <https://www.opensourceforu.com/2012/06/beginners-guide-gnu-grep-basics/>. Also, see <https://www.howtoforge.com/tutorial/linux-grep-command/>.