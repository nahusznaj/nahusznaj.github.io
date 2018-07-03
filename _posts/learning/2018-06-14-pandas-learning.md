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
    'A' : ['1','2','3','4','5','6','7','7','7','7'],     
    'B' : ['a','b','c','d','e','f','g','h','h','h'],
    }

df = pd.DataFrame(data=d)
```


### How to import an Excel file and create a data-frame:

```python
xl = pd.ExcelFile("file_name.xls")
df = xl.parse("Sheet1") # Or the sheet that is appropriate
```

### How to delete a `Column` from a dataframe

```python
df.drop('Column', axis = 1, inplace = True)
```

### How to locate rows that have a `null` value for a specific `Column`

```python
np.where(pd.isnull(df['Column']))
```

### How to set a `new value` of a `Column` cell in a specific `row_number`

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


## Plotting

### Set the title to a specific `ax`

```python
ax.set_title('Title', fontsize=19)
```
### Modify the font-size of the ticks

```python
plt.setp(ax.get_xticklabels(), fontsize=14)
plt.setp(ax.get_yticklabels(), fontsize=14)
```

### Modify the limits of the axis `x` and `y` in `ax`
```python
plt.setp(ax, yticks=np.arange(lower_limit, upper_limit, step= steps))
plt.setp(ax, xticks=np.arange(lower_limit, upper_limit, step= steps))
```

### Add a space between subplots
```python
fig.subplots_adjust(hspace=0.35)
```


### Colours!


### Tableau20 colors

```python
tableau20 = [(23, 190, 207), (31, 119, 180),  (255, 187, 120), (148, 103, 189),
             (44, 160, 44), (152, 223, 138), (174, 199, 232),
             (255, 127, 14),(214, 39, 40), (255, 152, 150),    
             (197, 176, 213), (140, 86, 75), (196, 156, 148),  
             (227, 119, 194), (127, 127, 127), (199, 199, 199),    
             (188, 189, 34), (219, 219, 141),  (158, 218, 229)]    



# Scale the RGB values to the [0, 1] range, which is the format matplotlib accepts.    
for i in range(len(tableau20)):    
    r, g, b = tableau20[i]    
    tableau20[i] = (r / 255., g / 255., b / 255.)    
```
