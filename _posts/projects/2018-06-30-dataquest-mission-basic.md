---
layout: article
title: Dataquest Python mission 1
categories: projects
modified: 2016-06-30T16:28:11-04:00
tags: [python, dataquest]
comments: true
share: true
read_time: true
---

## Exploratory analysis of deaths in the USA 2012 - 2014

This exercise is the last step in the `Python Programming: Intermediate` course at [Dataquest](dataquest.io).

The idea is to practice how to load `csv` files, use list comprehension techniques, and create dictionaries that reflect the content of the data.

In this problem we have `guns.csv`. The dataset came from [FiveThirtyEight](https://www.fivethirtyeight.com/). It contains data about gun deaths occurred in the USA from 2012 to 2014.

Each row has data about a  fatality, while each colum contains information on the victim.

First let us read the file with `csv` and store it in a list called `data`


```python
import csv
f = open("guns.csv", 'r')
csvreader = csv.reader(f)
data = list(csvreader)
data[0:5]
```




    [['',
      'year',
      'month',
      'intent',
      'police',
      'sex',
      'age',
      'race',
      'hispanic',
      'place',
      'education'],
     ['1',
      '2012',
      '01',
      'Suicide',
      '0',
      'M',
      '34',
      'Asian/Pacific Islander',
      '100',
      'Home',
      '4'],
     ['2', '2012', '01', 'Suicide', '0', 'F', '21', 'White', '100', 'Street', '3'],
     ['3',
      '2012',
      '01',
      'Suicide',
      '0',
      'M',
      '60',
      'White',
      '100',
      'Other specified',
      '4'],
     ['4', '2012', '02', 'Suicide', '0', 'M', '64', 'White', '100', 'Home', '4']]



Let us take the headers out of the data:


```python
headers = data[0]
data = data[1:]
```


```python
headers
```




    ['',
     'year',
     'month',
     'intent',
     'police',
     'sex',
     'age',
     'race',
     'hispanic',
     'place',
     'education']



It's always important to familiarise yourself with the dataset. Let's look at the first 5 rows of data:


```python
data[0:5]
```




    [['1',
      '2012',
      '01',
      'Suicide',
      '0',
      'M',
      '34',
      'Asian/Pacific Islander',
      '100',
      'Home',
      '4'],
     ['2', '2012', '01', 'Suicide', '0', 'F', '21', 'White', '100', 'Street', '3'],
     ['3',
      '2012',
      '01',
      'Suicide',
      '0',
      'M',
      '60',
      'White',
      '100',
      'Other specified',
      '4'],
     ['4', '2012', '02', 'Suicide', '0', 'M', '64', 'White', '100', 'Home', '4'],
     ['5',
      '2012',
      '02',
      'Suicide',
      '0',
      'M',
      '31',
      'White',
      '100',
      'Other specified',
      '2']]



A first analysis would be to look at how many deaths occur per year:

Let's extract the column `year`:


```python
years = []
for row in data:
    years.append(row[1])
    
years[0:5]
```




    ['2012', '2012', '2012', '2012', '2012']



Now let's loop through the data and count how many deaths occur in each year:


```python
year_counts = {}
for year in years:
    if year not in year_counts:
        year_counts[year] = 1
    else:
        year_counts[year] +=1
        
```


```python
year_counts
```




    {'2012': 33563, '2013': 33636, '2014': 33599}



We have information about monthly distribution of deaths. So let's look into deaths per month with the help of the [datetime python module](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior)


```python
import datetime

dates = []
for row in data:
    date = datetime.datetime(year = int(row[1]), month = int(row[2]), day = 1)
    dates.append(date)
```


```python
dates[0:5]
```




    [datetime.datetime(2012, 1, 1, 0, 0),
     datetime.datetime(2012, 1, 1, 0, 0),
     datetime.datetime(2012, 1, 1, 0, 0),
     datetime.datetime(2012, 2, 1, 0, 0),
     datetime.datetime(2012, 2, 1, 0, 0)]




```python
date_counts = {}
for item in dates:
    if item not in date_counts:
        date_counts[item] = 1
    else:
        date_counts[item] +=1

```


```python
date_counts
```




    {datetime.datetime(2012, 1, 1, 0, 0): 2758,
     datetime.datetime(2012, 2, 1, 0, 0): 2357,
     datetime.datetime(2012, 3, 1, 0, 0): 2743,
     datetime.datetime(2012, 4, 1, 0, 0): 2795,
     datetime.datetime(2012, 5, 1, 0, 0): 2999,
     datetime.datetime(2012, 6, 1, 0, 0): 2826,
     datetime.datetime(2012, 7, 1, 0, 0): 3026,
     datetime.datetime(2012, 8, 1, 0, 0): 2954,
     datetime.datetime(2012, 9, 1, 0, 0): 2852,
     datetime.datetime(2012, 10, 1, 0, 0): 2733,
     datetime.datetime(2012, 11, 1, 0, 0): 2729,
     datetime.datetime(2012, 12, 1, 0, 0): 2791,
     datetime.datetime(2013, 1, 1, 0, 0): 2864,
     datetime.datetime(2013, 2, 1, 0, 0): 2375,
     datetime.datetime(2013, 3, 1, 0, 0): 2862,
     datetime.datetime(2013, 4, 1, 0, 0): 2798,
     datetime.datetime(2013, 5, 1, 0, 0): 2806,
     datetime.datetime(2013, 6, 1, 0, 0): 2920,
     datetime.datetime(2013, 7, 1, 0, 0): 3079,
     datetime.datetime(2013, 8, 1, 0, 0): 2859,
     datetime.datetime(2013, 9, 1, 0, 0): 2742,
     datetime.datetime(2013, 10, 1, 0, 0): 2808,
     datetime.datetime(2013, 11, 1, 0, 0): 2758,
     datetime.datetime(2013, 12, 1, 0, 0): 2765,
     datetime.datetime(2014, 1, 1, 0, 0): 2651,
     datetime.datetime(2014, 2, 1, 0, 0): 2361,
     datetime.datetime(2014, 3, 1, 0, 0): 2684,
     datetime.datetime(2014, 4, 1, 0, 0): 2862,
     datetime.datetime(2014, 5, 1, 0, 0): 2864,
     datetime.datetime(2014, 6, 1, 0, 0): 2931,
     datetime.datetime(2014, 7, 1, 0, 0): 2884,
     datetime.datetime(2014, 8, 1, 0, 0): 2970,
     datetime.datetime(2014, 9, 1, 0, 0): 2914,
     datetime.datetime(2014, 10, 1, 0, 0): 2865,
     datetime.datetime(2014, 11, 1, 0, 0): 2756,
     datetime.datetime(2014, 12, 1, 0, 0): 2857}



Let's see the distribution of fatalities for gender and race group:


```python
sex = []
for row in data:
    sex.append(row[5])
    
sex[0:5]
```




    ['M', 'F', 'M', 'M', 'M']




```python
sex_counts = {}
for item in sex:
    if item not in sex_counts:
        sex_counts[item] = 1
    else:
        sex_counts[item] +=1
sex_counts
```




    {'F': 14449, 'M': 86349}



This shows that overall there are a lot more male victims than female victims.

Now let's look at race:


```python
race = []
for row in data:
    race.append(row[7])
    
race[0:5]
```




    ['Asian/Pacific Islander', 'White', 'White', 'White', 'White']




```python
race_counts = {}
for item in race:
    if item not in race_counts:
        race_counts[item] = 1
    else:
        race_counts[item] +=1
race_counts
```




    {'Asian/Pacific Islander': 1326,
     'Black': 23296,
     'Hispanic': 9022,
     'Native American/Native Alaskan': 917,
     'White': 66237}



This shows that more hispanic people are victims in gun deaths. 

But this is the thing: the dataset we are using counts absolute values. An din order to have an estimation we should see the numbers relative to the population for each race.

In order to do so, let us load the file `census.csv` which includes information on population per race.

### Deaths relative to race population


```python
f = open("census.csv", 'r')
csvreader = csv.reader(f)
census = list(csvreader)
census
```




    [['Id',
      'Year',
      'Id',
      'Sex',
      'Id',
      'Hispanic Origin',
      'Id',
      'Id2',
      'Geography',
      'Total',
      'Race Alone - White',
      'Race Alone - Hispanic',
      'Race Alone - Black or African American',
      'Race Alone - American Indian and Alaska Native',
      'Race Alone - Asian',
      'Race Alone - Native Hawaiian and Other Pacific Islander',
      'Two or More Races'],
     ['cen42010',
      'April 1, 2010 Census',
      'totsex',
      'Both Sexes',
      'tothisp',
      'Total',
      '0100000US',
      '',
      'United States',
      '308745538',
      '197318956',
      '44618105',
      '40250635',
      '3739506',
      '15159516',
      '674625',
      '6984195']]



The following dictionary will contain the population per race for 2010. This will allow us to have an estimation of deaths by gunshots per race relative to that race's population. This is an estimation because the census gives the population for the year 2010, while gunshut deaths correspond to other years.

Let's create a `mapping` dictionary that contains the population numbers per race based on the information that we have from the census file. We have to manipulate a little bit in order to make the categories match with our `guns` file (`data` list).


```python
mapping = {'Asian/Pacific Islander': 15159516+674625,
 'Black': 40250635,
 'Hispanic': 44618105,
 'Native American/Native Alaskan': 3739506,
 'White': 197318956}

```


```python
mapping
```




    {'Asian/Pacific Islander': 15834141,
     'Black': 40250635,
     'Hispanic': 44618105,
     'Native American/Native Alaskan': 3739506,
     'White': 197318956}



Now we can create a dictionary that stores the number of deaths per race relative to that race's population in terms of number of deaths over a hundred thousand people.


```python
race_per_hundredk = {}
for key in race_counts:
    race_per_hundredk[key] = 100000*race_counts[key]/mapping[key]
```


```python
race_per_hundredk
```




    {'Asian/Pacific Islander': 8.374309664161762,
     'Black': 57.877347773519595,
     'Hispanic': 20.220491210910907,
     'Native American/Native Alaskan': 24.521955573811088,
     'White': 33.56849303419181}



We can now realise that although there are more deaths occuring in hispanic race, the relative values show that actually, black people die a lot more than any other racial group.

### Now we could look at the type of death.

Now let's look at the type of death, that is whether it was {'Accidental', 'Homicide', 'NA', 'Suicide', 'Undetermined'}


```python
intents = []
for row in data:
    intents.append(row[3])
```


```python
races = []
for row in data:
    races.append(row[7])
```


```python
homicide_race_counts = {}
for i, race in enumerate(races):
    if intents[i] == 'Homicide':
        if race not in homicide_race_counts:
            homicide_race_counts[race] = 1
        else:
            homicide_race_counts[race] += 1
        
```


```python
homicide_race_counts
```




    {'Asian/Pacific Islander': 559,
     'Black': 19510,
     'Hispanic': 5634,
     'Native American/Native Alaskan': 326,
     'White': 9147}



We see that if we look at homicides, there are more black victims, than any other racial group. But again, these are absolute values. 

Let us relativise them to the race population.


```python
homicide_race_per_hundredk = {}
for key in race_counts:
    homicide_race_per_hundredk[key] = 100000*homicide_race_counts[key]/mapping[key]
    
homicide_race_per_hundredk
```




    {'Asian/Pacific Islander': 3.5303462309701548,
     'Black': 48.47128498718095,
     'Hispanic': 12.627161104219912,
     'Native American/Native Alaskan': 8.717729026240365,
     'White': 4.6356417981453335}



Comparing the dictionaries `homicide_race_per_hundredk` and `homicide_race_counts` is useful.


There were in the period 2012-2014 across the USA, 19510 black victims, while there were 5634 hispanic victims. That is, around three time more black victims than hispanics. 

However, in relative terms to the number of black and hispanic people, there were 48 deaths in black people per 100k black people, and 12 victims in hispanic people per 100k hispanic people. That is about 1/4, and not 1/3. If we had looked a the absolute values only we would have believed that the difference is smaller. Actually, more black people die out of gun related events than hispanic people.

### Python question

I thought that I could have obtained the number of deaths by homicide for each race group with a different code, as follows:


```python
another_homicide_race_counts = {}
for race in races:
    for row in data:
        if (row[7] == race) & (row[3] == 'Homicide'):
            if race not in another_homicide_race_counts:
                another_homicide_race_counts[race] = 1
            else:
                another_homicide_race_counts[race] += 1
            
```

But this piece of code does not obtain my expected output. Actually, it doesn't give any output. I think there is a time error.

And it made me wonder whether nesting for loops is a bad practice in python. If you know this, I would appreciate your comments!


I could keep working with this dataset, and make some plots with matplotlib, but I will do more exercises later on in my learning course towards data science at [dataquest](dataquest.io)

