---
layout: article
title: Some tricks I want to keep in mind II
categories: learning
modified: 2016-06-14T16:28:11-04:00
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
