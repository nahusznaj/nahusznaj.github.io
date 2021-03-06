---
layout: article
title: Some tricks I want to keep in mind (Pandas)
categories: learning
modified: 2018-06-14T16:28:11-04:00
tags: [python, pandas]
comments: true
share: true
read_time: true
---

Lots of people say that you should code thinking that you will forget reasons why you wrote things the way you did. You should write comments explaining to your future self.

In this post I will upload things that I want to remember how to use. Most of it I learned from `pandas` tagged questions in
[StakOverflow](https://stackoverflow.com/questions/tagged/pandas).


### How to define a dataframe from a dictionary:

```python
import pandas as pd

d = {
    'A' : [1, 2, 3, 4, 5, 6, 7, 7, 7, 7],     
    'B' : ['a','b','c','d','e','f','g','h','h','h'],
    }

df = pd.DataFrame(data=d)
```

### How to read a `csv` file and create a dataframe:

```python
df = pd.read_csv("your_csv_file.csv")
```

### How to import an Excel file and create a data-frame:

```python
xl = pd.ExcelFile("file_name.xls")
df = xl.parse("Sheet1") # Or the sheet that is appropriate
```


### How to select all the rows that match the condition that a specific `Column` takes a specific `value`

This returns a dataframe object, that we call `new_dataframe`
```python
new_dataframe = df[df["Column"] == 'Value']
```
`new_dataframe` is a Pandas dataframe and conserves the indexes from its parent dataframe.

### How to delete a `Column` from a dataframe

```python
df.drop('Column', axis = 1, inplace = True)
```

### How to locate rows that have a `null` value for a specific `Column`

```python
np.where(pd.isnull(df['Column']))
```

### How to update the cell at a specific `row_number` in a specific  `Column` to a `new value` 

```python
df.iloc[row_number][Column] = 'new value'
```

### How to update the name of a `Column` to `New_Column`

```python
df.rename(columns={'Column':'New_Column'}, inplace=True)
```

### `Groupby` and `count`

```python
grouped = df.groupby(['Column_1', 'Column_2']).count()
grouped.reset_index(inplace=True)
```

