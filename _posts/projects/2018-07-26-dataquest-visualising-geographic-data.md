---
layout: article
title: Visualising geographic data with python
categories: projects
modified: 2018-07-26T16:28:11-04:00
tags: [python, pandas, matplotlib, seaborn, basemap]
comments: true
share: true
read_time: true
---

This project is part of my learning experience with [Dataquest.io]() where I'm practising using basemap.

## 1. Geographic Data ##

Let's load pandas and the datasets provided by [Dataquest.io]:

```python
import pandas as pd
airlines = pd.read_csv("airlines.csv")
airports = pd.read_csv("airports.csv")
routes = pd.read_csv("routes.csv")
```

With this command I can print out the first row of the DataFrame

```python
print(airlines.iloc[0])

print(airports.iloc[0])

print(routes.iloc[0])
```
(I'm not showing the outputs now.)


## 4. Workflow With Basemap

```python
import matplotlib.pyplot as plt
from mpl_toolkits.basemap import Basemap

m = Basemap(projection='merc',
            llcrnrlat= -80,
            urcrnrlat = 80,
            llcrnrlon = -180,
            urcrnrlon = 180)
```

You can check out the parameters for [Basemap](https://matplotlib.org/basemap/api/basemap_api.html#mpl_toolkits.basemap.Basemap):

- `projection`: the map projection.
- `llcrnrlat`: latitude of lower left hand corner of the desired map domain
- `urcrnrlat`: latitude of upper right hand corner of the desired map domain
- `llcrnrlon`: longitude of lower left hand corner of the desired map domain
- `urcrnrlon`: longitude of upper right hand corner of the desired map domain

## 5. Converting From Spherical to Cartesian Coordinates ##
```python
m = Basemap(projection='merc', llcrnrlat=-80, urcrnrlat=80, llcrnrlon=-180, urcrnrlon=180)
```
The constructor (now `m`) takes only  list values, and I have Series objects, so I need to convert `Series.tolist()` to convert the longitude and latitude columns from the airports dataframe to lists.

```python
long = airports['longitude'].tolist()
lat = airports['latitude'].tolist()
```
Now, the following will covert the spherical coordinates to Cartesian coordinates.

```python
x, y = m(long, lat)
```

```python
m.scatter(x, y, s = 1)
plt.show()
```

![png](/images/2018-07-26-image_1.png)


## 7. Customizing The Plot Using Basemap ##

We can add costal lines to the map:
```python
m = Basemap(projection='merc', llcrnrlat=-80, urcrnrlat=80, llcrnrlon=-180, urcrnrlon=180)
longitudes = airports["longitude"].tolist()
latitudes = airports["latitude"].tolist()
x, y = m(longitudes, latitudes)
m.scatter(x, y, s=1)
m.drawcoastlines()
plt.show()
```

## 8. Customizing The Plot Using Matplotlib ##

We can add a title and change the size of the figure

```python
m = Basemap(projection='merc', llcrnrlat=-80, urcrnrlat=80, llcrnrlon=-180, urcrnrlon=180)
longitudes = airports["longitude"].tolist()
latitudes = airports["latitude"].tolist()
x, y = m(longitudes, latitudes)
fig, ax = plt.subplots(figsize = (15, 20))
ax.set_title('Scaled Up Earth With Coastlines')
m.scatter(x, y, s=1)
m.drawcoastlines()
plt.show()
```


## 9. Introduction to Great Circles ##

Let's use the routes dataset prepared by [dataquest.io]

```python
geo_routes = pd.read_csv('geo_routes.csv')
geo_routes.info()
print(geo_routes.head(5))
```


## 10. Displaying Great Circles ##
```python
fig, ax = plt.subplots(figsize=(15,20))
m = Basemap(projection='merc', llcrnrlat=-80, urcrnrlat=80, llcrnrlon=-180, urcrnrlon=180)
m.drawcoastlines()
```

Now the idea is to write a function, named create_great_circles() that draws a great circle for each route that has an absolute difference in the latitude and longitude

And apply it for a specific airport.


```pyton
def create_great_circles(dataframe):
    for row in dataframe.iterrows():
        if (row[1][7] - row[1][6] < 180) & (abs(row[1][5] - row[1][4]) < 180):
            m.drawgreatcircle(row[1][4], row[1][6], row[1][5], row[1][7])
```

The iterator iterrows gives a series, so taking row[1] selects the actual list of things that I want, since `row[0]` is the dataframe index. Once I have row[0] I can select the column that I want -- not by its name such as end_latitude, but as the column number because now it's an array and not a series.

```python
dfw = geo_routes[geo_routes['source']=='DFW']
dfw_copy = dfw[0:1]
dfw.head()
#create_great_circles(dfw)
#next(dfw_copy.iterrows())[1][4]
#create_great_circles(dfw_copy)[1][6]- create_great_circles(dfw_copy)[1][4]
create_great_circles(dfw)
```
