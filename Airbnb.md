```python
import numpy as np
import pandas as pd
```


```python
df = pd.read_csv("./Airbnb_Open_Data.csv")
```

    /var/folders/9c/9gm285k54tz9ysvymk9gtd400000gn/T/ipykernel_69508/3613748228.py:1: DtypeWarning: Columns (25) have mixed types. Specify dtype option on import or set low_memory=False.
      df = pd.read_csv("./Airbnb_Open_Data.csv")



```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 102599 entries, 0 to 102598
    Data columns (total 26 columns):
     #   Column                          Non-Null Count   Dtype  
    ---  ------                          --------------   -----  
     0   id                              102599 non-null  int64  
     1   NAME                            102349 non-null  object 
     2   host id                         102599 non-null  int64  
     3   host_identity_verified          102310 non-null  object 
     4   host name                       102193 non-null  object 
     5   neighbourhood group             102570 non-null  object 
     6   neighbourhood                   102583 non-null  object 
     7   lat                             102591 non-null  float64
     8   long                            102591 non-null  float64
     9   country                         102067 non-null  object 
     10  country code                    102468 non-null  object 
     11  instant_bookable                102494 non-null  object 
     12  cancellation_policy             102523 non-null  object 
     13  room type                       102599 non-null  object 
     14  Construction year               102385 non-null  float64
     15  price                           102352 non-null  object 
     16  service fee                     102326 non-null  object 
     17  minimum nights                  102190 non-null  float64
     18  number of reviews               102416 non-null  float64
     19  last review                     86706 non-null   object 
     20  reviews per month               86720 non-null   float64
     21  review rate number              102273 non-null  float64
     22  calculated host listings count  102280 non-null  float64
     23  availability 365                102151 non-null  float64
     24  house_rules                     50468 non-null   object 
     25  license                         2 non-null       object 
    dtypes: float64(9), int64(2), object(15)
    memory usage: 20.4+ MB



```python
df.isnull().sum()
```




    id                                     0
    NAME                                 250
    host id                                0
    host_identity_verified               289
    host name                            406
    neighbourhood group                   29
    neighbourhood                         16
    lat                                    8
    long                                   8
    country                              532
    country code                         131
    instant_bookable                     105
    cancellation_policy                   76
    room type                              0
    Construction year                    214
    price                                247
    service fee                          273
    minimum nights                       409
    number of reviews                    183
    last review                        15893
    reviews per month                  15879
    review rate number                   326
    calculated host listings count       319
    availability 365                     448
    house_rules                        52131
    license                           102597
    dtype: int64




```python

pd.set_option('display.max_columns', None)

```


```python
df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>NAME</th>
      <th>host id</th>
      <th>host_identity_verified</th>
      <th>host name</th>
      <th>neighbourhood group</th>
      <th>neighbourhood</th>
      <th>lat</th>
      <th>long</th>
      <th>country</th>
      <th>country code</th>
      <th>instant_bookable</th>
      <th>cancellation_policy</th>
      <th>room type</th>
      <th>Construction year</th>
      <th>price</th>
      <th>service fee</th>
      <th>minimum nights</th>
      <th>number of reviews</th>
      <th>last review</th>
      <th>reviews per month</th>
      <th>review rate number</th>
      <th>calculated host listings count</th>
      <th>availability 365</th>
      <th>house_rules</th>
      <th>license</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1001254</td>
      <td>Clean &amp; quiet apt home by the park</td>
      <td>80014485718</td>
      <td>unconfirmed</td>
      <td>Madaline</td>
      <td>Brooklyn</td>
      <td>Kensington</td>
      <td>40.64749</td>
      <td>-73.97237</td>
      <td>United States</td>
      <td>US</td>
      <td>False</td>
      <td>strict</td>
      <td>Private room</td>
      <td>2020.0</td>
      <td>$966</td>
      <td>$193</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>10/19/2021</td>
      <td>0.21</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>286.0</td>
      <td>Clean up and treat the home the way you'd like...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1002102</td>
      <td>Skylit Midtown Castle</td>
      <td>52335172823</td>
      <td>verified</td>
      <td>Jenna</td>
      <td>Manhattan</td>
      <td>Midtown</td>
      <td>40.75362</td>
      <td>-73.98377</td>
      <td>United States</td>
      <td>US</td>
      <td>False</td>
      <td>moderate</td>
      <td>Entire home/apt</td>
      <td>2007.0</td>
      <td>$142</td>
      <td>$28</td>
      <td>30.0</td>
      <td>45.0</td>
      <td>5/21/2022</td>
      <td>0.38</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>228.0</td>
      <td>Pet friendly but please confirm with me if the...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1002403</td>
      <td>THE VILLAGE OF HARLEM....NEW YORK !</td>
      <td>78829239556</td>
      <td>NaN</td>
      <td>Elise</td>
      <td>Manhattan</td>
      <td>Harlem</td>
      <td>40.80902</td>
      <td>-73.94190</td>
      <td>United States</td>
      <td>US</td>
      <td>True</td>
      <td>flexible</td>
      <td>Private room</td>
      <td>2005.0</td>
      <td>$620</td>
      <td>$124</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>352.0</td>
      <td>I encourage you to use my kitchen, cooking and...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1002755</td>
      <td>NaN</td>
      <td>85098326012</td>
      <td>unconfirmed</td>
      <td>Garry</td>
      <td>Brooklyn</td>
      <td>Clinton Hill</td>
      <td>40.68514</td>
      <td>-73.95976</td>
      <td>United States</td>
      <td>US</td>
      <td>True</td>
      <td>moderate</td>
      <td>Entire home/apt</td>
      <td>2005.0</td>
      <td>$368</td>
      <td>$74</td>
      <td>30.0</td>
      <td>270.0</td>
      <td>7/5/2019</td>
      <td>4.64</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>322.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1003689</td>
      <td>Entire Apt: Spacious Studio/Loft by central park</td>
      <td>92037596077</td>
      <td>verified</td>
      <td>Lyndon</td>
      <td>Manhattan</td>
      <td>East Harlem</td>
      <td>40.79851</td>
      <td>-73.94399</td>
      <td>United States</td>
      <td>US</td>
      <td>False</td>
      <td>moderate</td>
      <td>Entire home/apt</td>
      <td>2009.0</td>
      <td>$204</td>
      <td>$41</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>11/19/2018</td>
      <td>0.10</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>289.0</td>
      <td>Please no smoking in the house, porch or on th...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1004098</td>
      <td>Large Cozy 1 BR Apartment In Midtown East</td>
      <td>45498551794</td>
      <td>verified</td>
      <td>Michelle</td>
      <td>Manhattan</td>
      <td>Murray Hill</td>
      <td>40.74767</td>
      <td>-73.97500</td>
      <td>United States</td>
      <td>US</td>
      <td>True</td>
      <td>flexible</td>
      <td>Entire home/apt</td>
      <td>2013.0</td>
      <td>$577</td>
      <td>$115</td>
      <td>3.0</td>
      <td>74.0</td>
      <td>6/22/2019</td>
      <td>0.59</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>374.0</td>
      <td>No smoking, please, and no drugs.</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1004650</td>
      <td>BlissArtsSpace!</td>
      <td>61300605564</td>
      <td>NaN</td>
      <td>Alberta</td>
      <td>Brooklyn</td>
      <td>Bedford-Stuyvesant</td>
      <td>40.68688</td>
      <td>-73.95596</td>
      <td>United States</td>
      <td>US</td>
      <td>False</td>
      <td>moderate</td>
      <td>Private room</td>
      <td>2015.0</td>
      <td>$71</td>
      <td>$14</td>
      <td>45.0</td>
      <td>49.0</td>
      <td>10/5/2017</td>
      <td>0.40</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>224.0</td>
      <td>Please no shoes in the house so bring slippers...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1005202</td>
      <td>BlissArtsSpace!</td>
      <td>90821839709</td>
      <td>unconfirmed</td>
      <td>Emma</td>
      <td>Brooklyn</td>
      <td>Bedford-Stuyvesant</td>
      <td>40.68688</td>
      <td>-73.95596</td>
      <td>United States</td>
      <td>US</td>
      <td>False</td>
      <td>moderate</td>
      <td>Private room</td>
      <td>2009.0</td>
      <td>$1,060</td>
      <td>$212</td>
      <td>45.0</td>
      <td>49.0</td>
      <td>10/5/2017</td>
      <td>0.40</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>219.0</td>
      <td>House Guidelines for our BnB We are delighted ...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1005754</td>
      <td>Large Furnished Room Near B'way</td>
      <td>79384379533</td>
      <td>verified</td>
      <td>Evelyn</td>
      <td>Manhattan</td>
      <td>Hell's Kitchen</td>
      <td>40.76489</td>
      <td>-73.98493</td>
      <td>United States</td>
      <td>US</td>
      <td>True</td>
      <td>strict</td>
      <td>Private room</td>
      <td>2005.0</td>
      <td>$1,018</td>
      <td>$204</td>
      <td>2.0</td>
      <td>430.0</td>
      <td>6/24/2019</td>
      <td>3.47</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>180.0</td>
      <td>- Please clean up after yourself when using th...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1006307</td>
      <td>Cozy Clean Guest Room - Family Apt</td>
      <td>75527839483</td>
      <td>unconfirmed</td>
      <td>Carl</td>
      <td>Manhattan</td>
      <td>Upper West Side</td>
      <td>40.80178</td>
      <td>-73.96723</td>
      <td>United States</td>
      <td>US</td>
      <td>False</td>
      <td>strict</td>
      <td>Private room</td>
      <td>2015.0</td>
      <td>$291</td>
      <td>$58</td>
      <td>2.0</td>
      <td>118.0</td>
      <td>7/21/2017</td>
      <td>0.99</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>375.0</td>
      <td>NO SMOKING OR PETS ANYWHERE ON THE PROPERTY 1....</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Dropping License Column: 

df.drop(columns=['license'], inplace=True)

```


```python
#Dealing with null value:

# Filing  text-based nulls
df['NAME'] = df['NAME'].fillna('N/A')
df['host_identity_verified'] = df['host_identity_verified'].fillna('unverified')
df['neighbourhood group'] = df['neighbourhood group'].fillna('Unknown')
df['house_rules'] = df['house_rules'].fillna('None')


# Filling boolean or category-based
#df['instant_bookable'] = df['instant_bookable'].fillna('False')
df['cancellation_policy'] = df['cancellation_policy'].fillna('unknown')

# Numeric fixes
df['reviews per month'] = df['reviews per month'].fillna(0)
df['number of reviews'] = df['number of reviews'].fillna(0)



```


```python
df['host name'] = df['host name'].fillna('N/A')
```


```python
df['neighbourhood'] = df['neighbourhood'].fillna('Unknown')
```


```python
df.isnull().sum()
```




    id                                    0
    NAME                                  0
    host id                               0
    host_identity_verified                0
    host name                           406
    neighbourhood group                   0
    neighbourhood                        16
    lat                                   8
    long                                  8
    country                             532
    country code                        131
    instant_bookable                      0
    cancellation_policy                   0
    room type                             0
    Construction year                   214
    price                               247
    service fee                         273
    minimum nights                      409
    number of reviews                     0
    last review                       15893
    reviews per month                     0
    review rate number                  326
    calculated host listings count      319
    availability 365                    448
    house_rules                           0
    dtype: int64




```python
df['instant_bookable'] = df['instant_bookable'].fillna('False')
```


```python
# For price/service fee/minimum nights
df['price'] = pd.to_numeric(df['price'], errors='coerce')

```


```python
df['price'] = df['price'].fillna(df['price'].median())
```

    /Users/saiswethalakkoju/anaconda3/lib/python3.11/site-packages/numpy/lib/_nanfunctions_impl.py:1215: RuntimeWarning: Mean of empty slice
      return np.nanmean(a, axis, out=out, keepdims=keepdims)



```python
df.isnull().sum()
```




    id                                     0
    NAME                                   0
    host id                                0
    host_identity_verified                 0
    host name                            406
    neighbourhood group                    0
    neighbourhood                         16
    lat                                    8
    long                                   8
    country                              532
    country code                         131
    instant_bookable                       0
    cancellation_policy                    0
    room type                              0
    Construction year                    214
    price                             102599
    service fee                          273
    minimum nights                       409
    number of reviews                      0
    last review                        15893
    reviews per month                      0
    review rate number                   326
    calculated host listings count       319
    availability 365                     448
    house_rules                            0
    dtype: int64




```python
# Convert 't'/'f' and any string 'False' to real booleans
df['instant_bookable'] = df['instant_bookable'].replace({'t': True, 'f': False, 'False': False, 'True': True})
df['instant_bookable'] = df['instant_bookable'].astype(bool)

```

    /var/folders/9c/9gm285k54tz9ysvymk9gtd400000gn/T/ipykernel_69508/3329949727.py:2: FutureWarning: Downcasting behavior in `replace` is deprecated and will be removed in a future version. To retain the old behavior, explicitly call `result.infer_objects(copy=False)`. To opt-in to the future behavior, set `pd.set_option('future.no_silent_downcasting', True)`
      df['instant_bookable'] = df['instant_bookable'].replace({'t': True, 'f': False, 'False': False, 'True': True})



```python
df['instant_bookable'].value_counts()
```




    instant_bookable
    False    51579
    True     51020
    Name: count, dtype: int64




```python
df['number of reviews'].value_counts()
```




    number of reviews
    0.0      15917
    1.0      10408
    2.0       7175
    3.0       5375
    4.0       4151
             ...  
    567.0        1
    592.0        1
    797.0        1
    966.0        1
    300.0        1
    Name: count, Length: 476, dtype: int64




```python
df.isnull().sum()
```




    id                                    0
    NAME                                  0
    host id                               0
    host_identity_verified                0
    host name                             0
    neighbourhood group                   0
    neighbourhood                         0
    lat                                   8
    long                                  8
    country                             532
    country code                        131
    instant_bookable                      0
    cancellation_policy                   0
    room type                             0
    Construction year                   214
    price                               247
    service fee                         273
    minimum nights                      409
    number of reviews                     0
    last review                       15893
    reviews per month                     0
    review rate number                  326
    calculated host listings count      319
    availability 365                    448
    house_rules                           0
    dtype: int64




```python
df_ab = df[df['number of reviews'].notnull()]

```


```python
group_a = df_ab[df_ab['instant_bookable'] == False]['number of reviews']
group_b = df_ab[df_ab['instant_bookable'] == True]['number of reviews']

```


```python
mean_a = group_a.mean()
mean_b = group_b.mean()

lift = (mean_b - mean_a) / mean_a
print(f"Mean A (False): {mean_a:.4f}")
print(f"Mean B (True): {mean_b:.4f}")
print(f"Lift: {lift*100:.2f}%")

```

    Mean A (False): 27.3968
    Mean B (True): 27.4730
    Lift: 0.28%



```python
from scipy.stats import ttest_ind

t_stat, p_value = ttest_ind(group_a, group_b, equal_var=False)
print(f"T-statistic: {t_stat:.4f}, P-value: {p_value:.4f}")

```

    T-statistic: -0.2468, P-value: 0.8051



```python

```
