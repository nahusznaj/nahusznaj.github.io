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

Python starts counting from 0. So the first element of the list

` A = ['a','b','c','d','e']`,

is `A[0] = 'a'`.

The last element of `A` is `A[4] = 'e'`. If I wanted to use `len` to get the last element, I could try  `A[len(A)]`, but `len(A) = 5` and `A[5]` does not exist. If you call `A(len(A))` you will get the error `IndexError: list index out of range`. Instead, the correct way to get `'e'` would be `A[len(A) - 1]`.

Now, to run through the elements of a list, you can use `list[start : end]`. But there's a trick: it will start at `start` and it will stop one place before `end`. So `list[start : end]` will give as output `{list[0], list[1], list[2], ... , list[end-1]}`. That is why if you wanted to print the first 3 elements of `A`, the right code would be to call `print(A[0:3])`. This takes the elements `{0, 1, 2}` from `A`. If you call `A[0:2]` you will get `{A[0], A[1]} = {'a', 'b'}`.
