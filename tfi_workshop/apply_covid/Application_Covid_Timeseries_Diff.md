---
sort: 4
---

# Exploration of COVID19 dataset: Time-Series daily cases plot

## Recap & Grabbing Time-Series Data

First, customary importing of packages and data if you haven't already done so from the previous sections.


```python
import pandas as pd
import matplotlib.pyplot as plt
ASEAN_countries_list = ['Brunei', 'Cambodia', 'Indonesia', 'Laos', 'Malaysia', 'Burma', 'Philippines', 'Singapore', 'Vietnam']

link = 'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv'
covid19_data = pd.read_csv(link)
asean_df = covid19_data[covid19_data['Country/Region'].isin(ASEAN_countries_list)]
asean_df.set_index('Country/Region', inplace = True)
asean_df_dropped = asean_df.drop(columns = ['Province/State', 'Lat', 'Long'])
asean_t = asean_df_dropped.T
asean_t
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
      <th>Country/Region</th>
      <th>Brunei</th>
      <th>Burma</th>
      <th>Cambodia</th>
      <th>Indonesia</th>
      <th>Laos</th>
      <th>Malaysia</th>
      <th>Philippines</th>
      <th>Singapore</th>
      <th>Vietnam</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1/22/20</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>1/23/20</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <td>1/24/20</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <td>1/25/20</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <td>1/26/20</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>7/30/21</td>
      <td>336</td>
      <td>294460</td>
      <td>76585</td>
      <td>3372374</td>
      <td>5919</td>
      <td>1095486</td>
      <td>1580824</td>
      <td>64861</td>
      <td>141122</td>
    </tr>
    <tr>
      <td>7/31/21</td>
      <td>337</td>
      <td>299185</td>
      <td>77243</td>
      <td>3409658</td>
      <td>6299</td>
      <td>1113272</td>
      <td>1588965</td>
      <td>64981</td>
      <td>150060</td>
    </tr>
    <tr>
      <td>8/1/21</td>
      <td>337</td>
      <td>302665</td>
      <td>77914</td>
      <td>3440396</td>
      <td>6566</td>
      <td>1130422</td>
      <td>1597689</td>
      <td>65102</td>
      <td>157507</td>
    </tr>
    <tr>
      <td>8/2/21</td>
      <td>338</td>
      <td>306354</td>
      <td>78474</td>
      <td>3462800</td>
      <td>6765</td>
      <td>1146186</td>
      <td>1605762</td>
      <td>65213</td>
      <td>157507</td>
    </tr>
    <tr>
      <td>8/3/21</td>
      <td>338</td>
      <td>311067</td>
      <td>79051</td>
      <td>3496700</td>
      <td>7015</td>
      <td>1163291</td>
      <td>1612541</td>
      <td>65315</td>
      <td>174461</td>
    </tr>
  </tbody>
</table>
<p>560 rows × 9 columns</p>
</div>



## Using daily cumulative cases to calculate daily increase

Previously we looked at simple plotting of cumulative cases against dates. What if we would want to look at daily cases instead? We would need to do some maths and manipulation (i promise its nothing too scary).

Imagine our dataframe for 1 country now looks like this:

| Day | Cases  | 
| -- | ------------- | 
| 0  | 0 |
| 1  | 0          | 
| 2  | 1          |
| 3  | 3          | 
| 4  | 3          | 
| 5  | 4          |

How we are going to do this is to make make a new dataframe which brings a row to align with the previous day's data. So we can do some quick maths later!

| Day | Cases_O  | Cases_ShiftF  |  
| -- | ------------- | ------------ |
| 1  | 0          | NaN         | 
| 2  | 1          |    0      | 
| 3  | 3          |     1     | 
| 4  | 3          |      3    | 
| 5  | 4          |       3 | 

Then by adding a new column called "difference" we can calculate the difference / increase in cases for each day!


| Day | Cases_O  | Cases_ShiftF  |difference|
| -- | ------------- | ------------ | ---|
| 1  | 0          | NaN         | NaN|
| 2  | 1          |    0      | 1|
| 3  | 3          |     1     | 2|
| 4  | 3          |      3    |0|
| 5  | 4          |       3 |1 |

We can then plot the `difference`!

We can try do this for `Singapore` first.


```python
import numpy as np

#Make a copy so we don't actually change the previous dataframe
sg_s = asean_t['Singapore'].copy()

#Use this to shift the entire column down by 1
sg_s_F = sg_s.shift(1)

#Merge the two columns by using the same dates
sg_df = pd.concat([sg_s, sg_s_F], axis=1)

#Rename the columns for easier reference later
sg_df.columns = ['Cases_O', 'Cases_ShiftF']

#Creating a new column
sg_df['difference'] = sg_df['Cases_O'] - sg_df['Cases_ShiftF']
sg_df
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
      <th>Cases_O</th>
      <th>Cases_ShiftF</th>
      <th>difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1/22/20</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>1/23/20</td>
      <td>1</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>1/24/20</td>
      <td>3</td>
      <td>1.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>1/25/20</td>
      <td>3</td>
      <td>3.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1/26/20</td>
      <td>4</td>
      <td>3.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>7/30/21</td>
      <td>64861</td>
      <td>64722.0</td>
      <td>139.0</td>
    </tr>
    <tr>
      <td>7/31/21</td>
      <td>64981</td>
      <td>64861.0</td>
      <td>120.0</td>
    </tr>
    <tr>
      <td>8/1/21</td>
      <td>65102</td>
      <td>64981.0</td>
      <td>121.0</td>
    </tr>
    <tr>
      <td>8/2/21</td>
      <td>65213</td>
      <td>65102.0</td>
      <td>111.0</td>
    </tr>
    <tr>
      <td>8/3/21</td>
      <td>65315</td>
      <td>65213.0</td>
      <td>102.0</td>
    </tr>
  </tbody>
</table>
<p>560 rows × 3 columns</p>
</div>



If we just refer to the code snippet above, we can easily make a function that does this for each country! Lets call this function `country_diff()` which takes in the original dataframe (`asean_t`) and the country of choice. In turn, make it return a new modified dataframe!


```python
def country_diff(df, country):

    #Make a copy so we don't actually change the previous dataframe
    df_s = df[country].copy()

    #Use this to shift the entire column down by 1
    df_s_F = df_s.shift(1)

    #Merge the two columns by using the same dates
    country_df = pd.concat([df_s, df_s_F], axis=1)

    #Rename the columns for easier reference later
    country_df.columns = [f'{country}_Cases_O', f'{country}_Cases_ShiftF']

    #Creating a new column
    country_df[f'{country}_difference'] = country_df[f'{country}_Cases_O'] - country_df[f'{country}_Cases_ShiftF']
    return country_df

#Test the function
#brunei_df = country_diff(asean_t, 'Brunei')
```

Notice that our function is generally the same as our Singapore example, except we made some changes in the naming conventions (you'll see why later) to better reference them later!

We can now make use of `ASEAN_countries_list` to grab the daily cases of all our countries!

We can then make use of the `pd.concat` function again to have a dataframe consisting solely of daily cases for each country!


```python
#Create a new dataframe
asean_daily_df = pd.DataFrame()

#Run a for loop across all countries
#Reminder:
#ASEAN_countries_list = ['Brunei', 'Cambodia', 'Indonesia', 'Laos', 
#                        'Malaysia', 'Burma', 'Philippines', 'Singapore', 'Vietnam']

for country in ASEAN_countries_list:
    #Run the function and storing it into a temporary dataframe
    #per country
    temp_df = country_diff(asean_t, country)
    
    #Attach this temporary df to the actual dataframe
    #While selecting for the "Difference" column only!
    asean_daily_df = pd.concat([asean_daily_df, temp_df[f'{country}_difference']],sort = False, axis = 1)

    
#Drop the very first row because it makes no sense to have a change between 0th day and -1th day
asean_daily_df = asean_daily_df.iloc[1:,]
asean_daily_df
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
      <th>Brunei_difference</th>
      <th>Cambodia_difference</th>
      <th>Indonesia_difference</th>
      <th>Laos_difference</th>
      <th>Malaysia_difference</th>
      <th>Burma_difference</th>
      <th>Philippines_difference</th>
      <th>Singapore_difference</th>
      <th>Vietnam_difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1/23/20</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>1/24/20</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1/25/20</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1/26/20</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1/27/20</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>7/30/21</td>
      <td>3.0</td>
      <td>668.0</td>
      <td>41168.0</td>
      <td>244.0</td>
      <td>16840.0</td>
      <td>5127.0</td>
      <td>8537.0</td>
      <td>139.0</td>
      <td>7717.0</td>
    </tr>
    <tr>
      <td>7/31/21</td>
      <td>1.0</td>
      <td>658.0</td>
      <td>37284.0</td>
      <td>380.0</td>
      <td>17786.0</td>
      <td>4725.0</td>
      <td>8141.0</td>
      <td>120.0</td>
      <td>8938.0</td>
    </tr>
    <tr>
      <td>8/1/21</td>
      <td>0.0</td>
      <td>671.0</td>
      <td>30738.0</td>
      <td>267.0</td>
      <td>17150.0</td>
      <td>3480.0</td>
      <td>8724.0</td>
      <td>121.0</td>
      <td>7447.0</td>
    </tr>
    <tr>
      <td>8/2/21</td>
      <td>1.0</td>
      <td>560.0</td>
      <td>22404.0</td>
      <td>199.0</td>
      <td>15764.0</td>
      <td>3689.0</td>
      <td>8073.0</td>
      <td>111.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>8/3/21</td>
      <td>0.0</td>
      <td>577.0</td>
      <td>33900.0</td>
      <td>250.0</td>
      <td>17105.0</td>
      <td>4713.0</td>
      <td>6779.0</td>
      <td>102.0</td>
      <td>16954.0</td>
    </tr>
  </tbody>
</table>
<p>559 rows × 9 columns</p>
</div>

> Edit on 15th August 2021, I found out that there is a function called `pd.diff()` which does this exact thing. I will now demonstrate it

```python
# Yes thats it...
asean_daily_diff = asean_t.diff().iloc[1:,]
asean_daily_diff
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
      <th>Brunei_difference</th>
      <th>Cambodia_difference</th>
      <th>Indonesia_difference</th>
      <th>Laos_difference</th>
      <th>Malaysia_difference</th>
      <th>Burma_difference</th>
      <th>Philippines_difference</th>
      <th>Singapore_difference</th>
      <th>Vietnam_difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1/23/20</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>1/24/20</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1/25/20</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1/26/20</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1/27/20</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>7/30/21</td>
      <td>3.0</td>
      <td>668.0</td>
      <td>41168.0</td>
      <td>244.0</td>
      <td>16840.0</td>
      <td>5127.0</td>
      <td>8537.0</td>
      <td>139.0</td>
      <td>7717.0</td>
    </tr>
    <tr>
      <td>7/31/21</td>
      <td>1.0</td>
      <td>658.0</td>
      <td>37284.0</td>
      <td>380.0</td>
      <td>17786.0</td>
      <td>4725.0</td>
      <td>8141.0</td>
      <td>120.0</td>
      <td>8938.0</td>
    </tr>
    <tr>
      <td>8/1/21</td>
      <td>0.0</td>
      <td>671.0</td>
      <td>30738.0</td>
      <td>267.0</td>
      <td>17150.0</td>
      <td>3480.0</td>
      <td>8724.0</td>
      <td>121.0</td>
      <td>7447.0</td>
    </tr>
    <tr>
      <td>8/2/21</td>
      <td>1.0</td>
      <td>560.0</td>
      <td>22404.0</td>
      <td>199.0</td>
      <td>15764.0</td>
      <td>3689.0</td>
      <td>8073.0</td>
      <td>111.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>8/3/21</td>
      <td>0.0</td>
      <td>577.0</td>
      <td>33900.0</td>
      <td>250.0</td>
      <td>17105.0</td>
      <td>4713.0</td>
      <td>6779.0</td>
      <td>102.0</td>
      <td>16954.0</td>
    </tr>
  </tbody>
</table>
<p>559 rows × 9 columns</p>
</div>


## Plotting Daily Cases for each country

With this new dataframe, we can now make use of the plotting function in the previous section for time-series!

Note the use of `f''` to easily specify the different columns :)


```python
fig, ax = plt.subplots(figsize = (10,10))

#Iterate through our countries so we can plot automatically plot them!
for country in ASEAN_countries_list:
    asean_daily_df[f'{country}_difference'].plot(ax=ax, label = country)

ax.set_ylabel('Confirmed Daily Cases')
ax.set_xlabel('Dates')
ax.legend()
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/apply%20covid/Time/output_11_0.png)
    


From the graph above, you can tell that recently, Indonesia has the highest confirmed daily cases. Followed by Malaysia and Vietnam.

The interesting thing is that over time, we can tell that Indonesia's daily cases are slowly decreasing.
