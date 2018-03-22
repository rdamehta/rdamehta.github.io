---
title:  "African Conflicts"
subtitle: "A Series Exploring Conflicts on the Content"
author: "Ravi"
avatar: "img/authors/the-wire-couch.jpg"
image: "img/africa.jpg"
date:   2018-03-22 12:12:12
---

## African Conflicts
The data is from African Conflict Location and Event Data Project and can be downloaded from Kaggle https://www.kaggle.com/jboysen/african-conflicts

From the Kaggle Description:

"This dataset codes the dates and locations of all reported political violence and protest events in dozens of developing countries in Africa. Political violence and protest includes events that occur within civil wars and periods of instability, public protest and regime breakdown. The project covers all African countries from 1997 to the present."


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
```


```python
pd.options.display.max_columns = 999
df = pd.read_csv('african_conflicts.csv', encoding ='latin1', low_memory = False)
df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ACTOR1</th>
      <th>ACTOR1_ID</th>
      <th>ACTOR2</th>
      <th>ACTOR2_ID</th>
      <th>ACTOR_DYAD_ID</th>
      <th>ADMIN1</th>
      <th>ADMIN2</th>
      <th>ADMIN3</th>
      <th>ALLY_ACTOR_1</th>
      <th>ALLY_ACTOR_2</th>
      <th>COUNTRY</th>
      <th>EVENT_DATE</th>
      <th>EVENT_ID_CNTY</th>
      <th>EVENT_ID_NO_CNTY</th>
      <th>EVENT_TYPE</th>
      <th>FATALITIES</th>
      <th>GEO_PRECISION</th>
      <th>GWNO</th>
      <th>INTER1</th>
      <th>INTER2</th>
      <th>INTERACTION</th>
      <th>LATITUDE</th>
      <th>LOCATION</th>
      <th>LONGITUDE</th>
      <th>NOTES</th>
      <th>SOURCE</th>
      <th>TIME_PRECISION</th>
      <th>YEAR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>Civilians (Algeria)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tizi Ouzou</td>
      <td>Beni-Douala</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>Algeria</td>
      <td>18/04/2001</td>
      <td>1416RTA</td>
      <td>NaN</td>
      <td>Violence against civilians</td>
      <td>1</td>
      <td>1</td>
      <td>615</td>
      <td>1</td>
      <td>7</td>
      <td>17</td>
      <td>36.61954</td>
      <td>Beni Douala</td>
      <td>4.08282</td>
      <td>A Berber student was shot while in police cust...</td>
      <td>Associated Press Online</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Rioters (Algeria)</td>
      <td>NaN</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tizi Ouzou</td>
      <td>Tizi Ouzou</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>19/04/2001</td>
      <td>2229RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>3</td>
      <td>615</td>
      <td>5</td>
      <td>1</td>
      <td>15</td>
      <td>36.71183</td>
      <td>Tizi Ouzou</td>
      <td>4.04591</td>
      <td>Riots were reported in numerous villages in Ka...</td>
      <td>Kabylie report</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bejaia</td>
      <td>Amizour</td>
      <td>NaN</td>
      <td>Students (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>20/04/2001</td>
      <td>2230RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>6</td>
      <td>0</td>
      <td>60</td>
      <td>36.64022</td>
      <td>Amizour</td>
      <td>4.90131</td>
      <td>Students protested in the Amizour area. At lea...</td>
      <td>Crisis Group</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rioters (Algeria)</td>
      <td>NaN</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bejaia</td>
      <td>Amizour</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>21/04/2001</td>
      <td>2231RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>5</td>
      <td>1</td>
      <td>15</td>
      <td>36.64022</td>
      <td>Amizour</td>
      <td>4.90131</td>
      <td>Rioters threw molotov cocktails, rocks and bur...</td>
      <td>Kabylie report</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rioters (Algeria)</td>
      <td>NaN</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tizi Ouzou</td>
      <td>Beni-Douala</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>21/04/2001</td>
      <td>2232RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>5</td>
      <td>1</td>
      <td>15</td>
      <td>36.61954</td>
      <td>Beni Douala</td>
      <td>4.08282</td>
      <td>Rioters threw molotov cocktails, rocks and bur...</td>
      <td>Kabylie report</td>
      <td>1</td>
      <td>2001</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 165808 entries, 0 to 165807
    Data columns (total 28 columns):
    ACTOR1              165808 non-null object
    ACTOR1_ID           140747 non-null float64
    ACTOR2              122255 non-null object
    ACTOR2_ID           140747 non-null float64
    ACTOR_DYAD_ID       140747 non-null object
    ADMIN1              165808 non-null object
    ADMIN2              165676 non-null object
    ADMIN3              86933 non-null object
    ALLY_ACTOR_1        28144 non-null object
    ALLY_ACTOR_2        19651 non-null object
    COUNTRY             165808 non-null object
    EVENT_DATE          165808 non-null object
    EVENT_ID_CNTY       165808 non-null object
    EVENT_ID_NO_CNTY    140747 non-null float64
    EVENT_TYPE          165808 non-null object
    FATALITIES          165808 non-null int64
    GEO_PRECISION       165808 non-null int64
    GWNO                165808 non-null int64
    INTER1              165808 non-null int64
    INTER2              165808 non-null int64
    INTERACTION         165808 non-null int64
    LATITUDE            165808 non-null object
    LOCATION            165805 non-null object
    LONGITUDE           165808 non-null object
    NOTES               155581 non-null object
    SOURCE              165635 non-null object
    TIME_PRECISION      165808 non-null int64
    YEAR                165808 non-null int64
    dtypes: float64(3), int64(8), object(17)
    memory usage: 35.4+ MB
    

There are a lot of columns|variables|features in this data set. I'm particularly interested Country where a conflict occured, which countries or groups of people were involved, when the event took place, How many fatalities, some notes on the conflict, and what type of conflict was it.

So I am going to limit our data set to these columns




```python
df = df.loc[:,['ACTOR1', 'ACTOR2', 'ADMIN1', 'ADMIN2','COUNTRY', 'LOCATION', 'EVENT_DATE', 'EVENT_TYPE', 'INTERACTION', 'FATALITIES', 'NOTES']]
df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ACTOR1</th>
      <th>ACTOR2</th>
      <th>ADMIN1</th>
      <th>ADMIN2</th>
      <th>COUNTRY</th>
      <th>LOCATION</th>
      <th>EVENT_DATE</th>
      <th>EVENT_TYPE</th>
      <th>INTERACTION</th>
      <th>FATALITIES</th>
      <th>NOTES</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Police Forces of Algeria (1999-)</td>
      <td>Civilians (Algeria)</td>
      <td>Tizi Ouzou</td>
      <td>Beni-Douala</td>
      <td>Algeria</td>
      <td>Beni Douala</td>
      <td>18/04/2001</td>
      <td>Violence against civilians</td>
      <td>17</td>
      <td>1</td>
      <td>A Berber student was shot while in police cust...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Rioters (Algeria)</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>Tizi Ouzou</td>
      <td>Tizi Ouzou</td>
      <td>Algeria</td>
      <td>Tizi Ouzou</td>
      <td>19/04/2001</td>
      <td>Riots/Protests</td>
      <td>15</td>
      <td>0</td>
      <td>Riots were reported in numerous villages in Ka...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>Bejaia</td>
      <td>Amizour</td>
      <td>Algeria</td>
      <td>Amizour</td>
      <td>20/04/2001</td>
      <td>Riots/Protests</td>
      <td>60</td>
      <td>0</td>
      <td>Students protested in the Amizour area. At lea...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rioters (Algeria)</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>Bejaia</td>
      <td>Amizour</td>
      <td>Algeria</td>
      <td>Amizour</td>
      <td>21/04/2001</td>
      <td>Riots/Protests</td>
      <td>15</td>
      <td>0</td>
      <td>Rioters threw molotov cocktails, rocks and bur...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rioters (Algeria)</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>Tizi Ouzou</td>
      <td>Beni-Douala</td>
      <td>Algeria</td>
      <td>Beni Douala</td>
      <td>21/04/2001</td>
      <td>Riots/Protests</td>
      <td>15</td>
      <td>0</td>
      <td>Rioters threw molotov cocktails, rocks and bur...</td>
    </tr>
  </tbody>
</table>
</div>



The column Interaction actually tells us quite a bit. The first digit is the type of Actor 1, and the second digit is the type of Actor 2. From the Userguide:

A numeric code indicating the interaction 
between types of ACTOR1 and ACTOR2. 
Coded as an interaction between
actor types, and recorded as
lowest joint number:

- 1 Government/Military/Police
- 2 Rebel group
- 3 Political Militia
- 4 Communal Militia
- 5 Rioters
- 6 Protestors
- 7 Civilians
- 8 Other (e.g. Regional groups
such as AFICOM; or UN


e.g.  When  the  action  is 
between   a 
government   and   a 
rebel  group,  this  will  be  coded  as 
12; when a political militia attacks 
civilians, it is coded as 37.


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 165808 entries, 0 to 165807
    Data columns (total 11 columns):
    ACTOR1         165808 non-null object
    ACTOR2         122255 non-null object
    ADMIN1         165808 non-null object
    ADMIN2         165676 non-null object
    COUNTRY        165808 non-null object
    LOCATION       165805 non-null object
    EVENT_DATE     165808 non-null object
    EVENT_TYPE     165808 non-null object
    INTERACTION    165808 non-null int64
    FATALITIES     165808 non-null int64
    NOTES          155581 non-null object
    dtypes: int64(2), object(9)
    memory usage: 13.9+ MB
    

Suprisingly the above shows that we don't have a lot of Null values. Only in places we might expect such as 'Notes' or 'Actor2'. I know I'm want to explore conflicts as they progress over time so I better enocde Event_Date as a datetime object


```python
df['EVENT_DATE'] = pd.to_datetime(df['EVENT_DATE'])
```

### Exploratory Data Analysis

Off the bat here are some things I'm curious about:

- In the last 5 years which African country had the most conflict events?
- most fatalities?
- what type of events were those?



```python
df[doi].COUNTRY.value_counts().head(10)
```




    Somalia                         16916
    Nigeria                          8933
    South Africa                     8425
    Sudan                            7849
    Egypt                            7829
    Democratic Republic of Congo     6368
    Libya                            5752
    South Sudan                      5083
    Burundi                          4479
    Tunisia                          3740
    Name: COUNTRY, dtype: int64




```python
doi = df['EVENT_DATE'] > '2012'
plt.figure(figsize=(8,6))
sns.countplot(x = 'COUNTRY',data = df[doi], order=df[doi].COUNTRY.value_counts().head(10).index,
             )
plt.xticks(rotation = 90)
```




    (array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]), <a list of 10 Text xticklabel objects>)




![png](img/africa_files/blogpost_13_1.png)


In the last 5 years Somalia by far has had the most events, more that double that most of the other African Countries. The list isnt too suprising if you've been paying attention to the news. We see some North African Countries: Libya, Tunisia, Egypt so this data shows the after effects of Arab Springs. Remember also that in 2011 Gadaffi was overthrown.

Lets see this list by fatalities


```python
plt.figure(figsize=(8,6))
sns.barplot(x='COUNTRY', y='FATALITIES', data = df[doi],
            estimator = sum,
            ci = None,
           order = df[doi].groupby('COUNTRY')['FATALITIES'].sum().sort_values(ascending = False).head(10).index)

plt.xticks(rotation = 90)
plt.ylabel('Total Sum of Fatalities')
```




    <matplotlib.text.Text at 0x1fcdf569668>




![png](img/africa_files/blogpost_15_1.png)


Very very interesting! Although Somalia had the most number of incidents, Nigeria by far had the most fatalities. I wonder what type of conflicts occured there? Lets take a look!


```python
dfdoi = df[doi]

```


```python
nigeria = dfdoi['COUNTRY']=='Nigeria'
plt.figure(figsize = (12,6))
sns.countplot(x = 'INTERACTION', data = dfdoi[nigeria])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1fcdf1b77f0>




![png](img/africa_files/blogpost_18_1.png)


60 refers to Protestors Sole Action, that actually is a decent measure of unrest in a country, and entirely possible there were no fatalities during many of these protests. Lets do a quick pandas query sorting INTERACTION type by number of fatalities


```python
dfdoi[nigeria].groupby('INTERACTION')['FATALITIES'].sum().sort_values(ascending = False)
```




    INTERACTION
    12    9807
    37    8388
    27    7781
    47    5730
    13    3951
    44    1432
    17    1285
    28     681
    34     588
    15     428
    33     390
    14     339
    23     284
    24     238
    55     189
    16      69
    22      46
    50      44
    57      41
    11      32
    20      14
    78      10
    38       8
    56       8
    30       5
    36       5
    35       2
    46       2
    60       2
    18       1
    58       1
    26       0
    66       0
    40       0
    45       0
    48       0
    10       0
    Name: FATALITIES, dtype: int64



AHA! This tells us much more information. Turns out there were 2 fatalities in all of those protests. And almost 10,000 people were killed in MILITARY vs REBEL conflicts. 

Also take a look at the next 3 numbers. Theres a common element, the digit '7'. This unfortunately represents Civilians. As in there was a vast amount of fatal violent conflicts directed towards Civilians by Military, Rebel, and Militia groups. An unfortunate reality that is all too common in places where multiple factions are fighting for a piece of the pie



This was just a brief introduction into the dataset. I am definitly going to make this a series where I'll gather insights, throw in some interactive plots, and definitly maps to help visualize the conflicts that have ravaged one of most beautiful continents on Earth. 


```python

```
