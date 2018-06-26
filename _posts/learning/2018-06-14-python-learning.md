---
layout: article
title: Some tricks I want to keep in mind II
categories: learning
modified: 2018-06-26T16:28:11-04:00
tags: [python]
comments: true
share: true
read_time: true
---


I'm doing online courses to train myself to become a data scientist.

Here I want to post some general python commands that I usually use and often forget.

### How to load a file:

Say that you have a database `file.csv` with comma and line separated values. For example

`A,1`

`B,2`

`C,3`

in a csv file.

To import/load this into python you can do:

```python
f = open("file.csv", 'r')
data = f.read()
rows = data.split("\n") #first separate by \n new lines.
new_list = []
for row in rows:
    new_list.append(row.split(',')) #then separate each line by comma and append it to the new_list
```

There's more information in [Python's doc site](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)


### Slicing lists in Python

Python starts counting from 0. So the first element of the list

` A = ['a','b','c','d','e']`,

is `A[0] = 'a'`.

Now, the last element of `A` is `A[4] = 'e'`. If I wanted to use `len` to get the last element, I could try  `A[len(A)]`, but `len(A) = 5` and `A[5]` does not exist. If you call `A[len(A)]` you will get a `IndexError: list index out of range` error. Instead, the correct way to obtain `'e'` would be `A[len(A) - 1]`.

Now, to run through the elements of a list (or to slice a list), you can use `list[start : end]`. But there's a trick: Python does not include the last element so it will start at `start` but it will stop one element before `end`. 

Hence, `list[start : end]` will give as output the set `{list[start], list[start + 1], list[start + 2], ... , list[end-1]}`. For example, if you wanted to print out the first three elements of `A`, that is, `{0, 1, 2}`,  you should call `print(A[0:3])`. `A[0:3]` means `A[0], A[1], A[2]` and it does not include `A[3]` because Python does not take the last element of the range used in the slicing. So, if you call `print(A[0:2])` you will get `'a', 'b'`, which is `{A[0], A[1]}`.

For more syntax on slicing lists, check out this [Stackoverflow question](https://stackoverflow.com/a/509295/7746941). There you'll find this reference:

`a[start:end] # items start through end-1`

`a[start:]    # items start through the rest of the array`

`a[:end]      # items from the beginning through end-1`

`a[:]         # a copy of the whole array`



