---
sort: 3
---

# Exploration of COVID19 dataset: Time-Series plots

## Recap & Grabbing Time-Series Data

First, customary importing of packages and data if you haven't already done so from the previous sections.


```python
import pandas as pd
import matplotlib.pyplot as plt
ASEAN_countries_list = ['Brunei', 'Cambodia', 'Indonesia', 'Laos', 'Malaysia', 'Burma', 'Philippines', 'Singapore', 'Vietnam']
```

In order for us to do time-series plots of COVID19, it would be very inefficient of us to use datasets where a single file is data for 1 day. Luckily for us, from the same source, there is a collated dataset that has a column for each day. Let's load it in the same way first.

We can also use the same code from previous sections to select for ASEAN countries only!


```python
link = 'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv'
covid19_data = pd.read_csv(link)
asean_df = covid19_data[covid19_data['Country/Region'].isin(ASEAN_countries_list)]
asean_df.set_index('Country/Region', inplace = True)
asean_df_dropped = asean_df.drop(columns = ['Province/State', 'Lat', 'Long'])
asean_df_dropped
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
      <th>1/22/20</th>
      <th>1/23/20</th>
      <th>1/24/20</th>
      <th>1/25/20</th>
      <th>1/26/20</th>
      <th>1/27/20</th>
      <th>1/28/20</th>
      <th>1/29/20</th>
      <th>1/30/20</th>
      <th>1/31/20</th>
      <th>...</th>
      <th>7/25/21</th>
      <th>7/26/21</th>
      <th>7/27/21</th>
      <th>7/28/21</th>
      <th>7/29/21</th>
      <th>7/30/21</th>
      <th>7/31/21</th>
      <th>8/1/21</th>
      <th>8/2/21</th>
      <th>8/3/21</th>
    </tr>
    <tr>
      <th>Country/Region</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Brunei</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>321</td>
      <td>333</td>
      <td>333</td>
      <td>333</td>
      <td>333</td>
      <td>336</td>
      <td>337</td>
      <td>337</td>
      <td>338</td>
      <td>338</td>
    </tr>
    <tr>
      <td>Burma</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>269525</td>
      <td>274155</td>
      <td>279119</td>
      <td>284099</td>
      <td>289333</td>
      <td>294460</td>
      <td>299185</td>
      <td>302665</td>
      <td>306354</td>
      <td>311067</td>
    </tr>
    <tr>
      <td>Cambodia</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>72923</td>
      <td>73701</td>
      <td>74386</td>
      <td>75152</td>
      <td>75917</td>
      <td>76585</td>
      <td>77243</td>
      <td>77914</td>
      <td>78474</td>
      <td>79051</td>
    </tr>
    <tr>
      <td>Indonesia</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>3166505</td>
      <td>3194733</td>
      <td>3239936</td>
      <td>3287727</td>
      <td>3331206</td>
      <td>3372374</td>
      <td>3409658</td>
      <td>3440396</td>
      <td>3462800</td>
      <td>3496700</td>
    </tr>
    <tr>
      <td>Laos</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>4762</td>
      <td>4985</td>
      <td>5154</td>
      <td>5434</td>
      <td>5675</td>
      <td>5919</td>
      <td>6299</td>
      <td>6566</td>
      <td>6765</td>
      <td>7015</td>
    </tr>
    <tr>
      <td>Malaysia</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>7</td>
      <td>8</td>
      <td>8</td>
      <td>...</td>
      <td>1013438</td>
      <td>1027954</td>
      <td>1044071</td>
      <td>1061476</td>
      <td>1078646</td>
      <td>1095486</td>
      <td>1113272</td>
      <td>1130422</td>
      <td>1146186</td>
      <td>1163291</td>
    </tr>
    <tr>
      <td>Philippines</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>1548755</td>
      <td>1555396</td>
      <td>1562420</td>
      <td>1566667</td>
      <td>1572287</td>
      <td>1580824</td>
      <td>1588965</td>
      <td>1597689</td>
      <td>1605762</td>
      <td>1612541</td>
    </tr>
    <tr>
      <td>Singapore</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>7</td>
      <td>7</td>
      <td>10</td>
      <td>13</td>
      <td>...</td>
      <td>64179</td>
      <td>64314</td>
      <td>64453</td>
      <td>64589</td>
      <td>64722</td>
      <td>64861</td>
      <td>64981</td>
      <td>65102</td>
      <td>65213</td>
      <td>65315</td>
    </tr>
    <tr>
      <td>Vietnam</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>101173</td>
      <td>106347</td>
      <td>117121</td>
      <td>123640</td>
      <td>133405</td>
      <td>141122</td>
      <td>150060</td>
      <td>157507</td>
      <td>157507</td>
      <td>174461</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 560 columns</p>
</div>



## Transposing

From the table, the columns are the dates, and the countries were set as the index. This would be very difficult for us to plot a time-series graph with the dates as the x-axis.

To solve this problem, we would need to transpose the dataframe so that the columns are rows.


```python
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



## Time-Series Plotting

To plot a time-series chart, it is really easy with pandas!


```python
ax = asean_t['Singapore'].plot()
ax.set_ylabel('Confirmed Cases')
ax.set_xlabel('Dates')
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/apply%20covid/Time/output_8_0.png)
    


In order to plot more countries onto the same plot, we would need to make use of the `plt.subplots()` function call as shown in the `matplotlib` section previously!


```python
fig, ax = plt.subplots()

#Iterate through our countries so we can plot automatically plot them!
for country in ASEAN_countries_list:
    asean_t[country].plot(ax=ax)

ax.set_ylabel('Confirmed Cases')
ax.set_xlabel('Dates')
ax.legend()
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/apply%20covid/Time/output_10_0.png)
    


From the time-series plots, we can tell that currently, Indonesia has the highest cumulative confirmed cases amongst all the ASEAN countries!
