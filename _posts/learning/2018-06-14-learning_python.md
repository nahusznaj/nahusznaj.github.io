---
layout: article
title: Some tricks I want to keep in mind II
categories: learning
modified: 2016-06-15T16:28:11-04:00
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


### Lists and indexing in Python

Python counts from 0 on. So a list

` A = ['a','b','c','d','e']`,

has 5 elements. The first element of `A` is `A[0] = 'a'`.

The last element of `A` is `A[4] = 'e'`. If I wanted to use `len` to get the last element, the correct way to get `'e'` would be `A[len(A) - 1]`. This is because `len(A) = 5` and `A[5]` does not exist.
