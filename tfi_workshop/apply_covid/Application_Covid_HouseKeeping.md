---
sort: 1
---

# Housekeeping

First, customary importing of packages and data if you haven't already done so from the previous sections."


```python
import pandas as pd
import matplotlib.pyplot as plt

month_int = '08'
day_int = '03'

df = pd.read_csv(f"https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_daily_reports/{month_int}-{day_int}-2021.csv")
df
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
      <th>FIPS</th>
      <th>Admin2</th>
      <th>Province_State</th>
      <th>Country_Region</th>
      <th>Last_Update</th>
      <th>Lat</th>
      <th>Long_</th>
      <th>Confirmed</th>
      <th>Deaths</th>
      <th>Recovered</th>
      <th>Active</th>
      <th>Combined_Key</th>
      <th>Incident_Rate</th>
      <th>Case_Fatality_Ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Afghanistan</td>
      <td>2021-08-04 04:21:25</td>
      <td>33.939110</td>
      <td>67.709953</td>
      <td>148572</td>
      <td>6804</td>
      <td>82586.0</td>
      <td>59182.0</td>
      <td>Afghanistan</td>
      <td>381.655103</td>
      <td>4.579598</td>
    </tr>
    <tr>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Albania</td>
      <td>2021-08-04 04:21:25</td>
      <td>41.153300</td>
      <td>20.168300</td>
      <td>133211</td>
      <td>2457</td>
      <td>130291.0</td>
      <td>463.0</td>
      <td>Albania</td>
      <td>4628.917923</td>
      <td>1.844442</td>
    </tr>
    <tr>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>2021-08-04 04:21:25</td>
      <td>28.033900</td>
      <td>1.659600</td>
      <td>175229</td>
      <td>4370</td>
      <td>117557.0</td>
      <td>53302.0</td>
      <td>Algeria</td>
      <td>399.600529</td>
      <td>2.493879</td>
    </tr>
    <tr>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Andorra</td>
      <td>2021-08-04 04:21:25</td>
      <td>42.506300</td>
      <td>1.521800</td>
      <td>14766</td>
      <td>128</td>
      <td>14348.0</td>
      <td>290.0</td>
      <td>Andorra</td>
      <td>19110.852262</td>
      <td>0.866856</td>
    </tr>
    <tr>
      <td>4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Angola</td>
      <td>2021-08-04 04:21:25</td>
      <td>-11.202700</td>
      <td>17.873900</td>
      <td>43070</td>
      <td>1022</td>
      <td>39389.0</td>
      <td>2659.0</td>
      <td>Angola</td>
      <td>131.046214</td>
      <td>2.372881</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>3982</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Vietnam</td>
      <td>2021-08-04 04:21:25</td>
      <td>14.058324</td>
      <td>108.277199</td>
      <td>174461</td>
      <td>2071</td>
      <td>50831.0</td>
      <td>121559.0</td>
      <td>Vietnam</td>
      <td>179.231087</td>
      <td>1.187085</td>
    </tr>
    <tr>
      <td>3983</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>West Bank and Gaza</td>
      <td>2021-08-04 04:21:25</td>
      <td>31.952200</td>
      <td>35.233200</td>
      <td>317264</td>
      <td>3609</td>
      <td>312289.0</td>
      <td>1366.0</td>
      <td>West Bank and Gaza</td>
      <td>6219.136020</td>
      <td>1.137538</td>
    </tr>
    <tr>
      <td>3984</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yemen</td>
      <td>2021-08-04 04:21:25</td>
      <td>15.552727</td>
      <td>48.516388</td>
      <td>7086</td>
      <td>1380</td>
      <td>4232.0</td>
      <td>1474.0</td>
      <td>Yemen</td>
      <td>23.757821</td>
      <td>19.475021</td>
    </tr>
    <tr>
      <td>3985</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Zambia</td>
      <td>2021-08-04 04:21:25</td>
      <td>-13.133897</td>
      <td>27.849332</td>
      <td>197123</td>
      <td>3422</td>
      <td>189341.0</td>
      <td>4360.0</td>
      <td>Zambia</td>
      <td>1072.255612</td>
      <td>1.735972</td>
    </tr>
    <tr>
      <td>3986</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Zimbabwe</td>
      <td>2021-08-04 04:21:25</td>
      <td>-19.015438</td>
      <td>29.154857</td>
      <td>112435</td>
      <td>3676</td>
      <td>81570.0</td>
      <td>27189.0</td>
      <td>Zimbabwe</td>
      <td>756.479528</td>
      <td>3.269445</td>
    </tr>
  </tbody>
</table>
<p>3987 rows × 14 columns</p>
</div>



As you can tell, the table is huge with ~4000 rows. Let us subset our data to just ASEAN countries.


```python
ASEAN_countries_list = ['Brunei', 'Cambodia', 'Indonesia', 'Laos', 'Malaysia', 'Burma', 'Philippines', 'Singapore', 'Vietnam']

asean_df = df[df['Country_Region'].isin(ASEAN_countries_list)]
asean_df.set_index('Country_Region', inplace = True)
asean_df
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
      <th>FIPS</th>
      <th>Admin2</th>
      <th>Province_State</th>
      <th>Last_Update</th>
      <th>Lat</th>
      <th>Long_</th>
      <th>Confirmed</th>
      <th>Deaths</th>
      <th>Recovered</th>
      <th>Active</th>
      <th>Combined_Key</th>
      <th>Incident_Rate</th>
      <th>Case_Fatality_Ratio</th>
    </tr>
    <tr>
      <th>Country_Region</th>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-08-04 04:21:25</td>
      <td>4.535300</td>
      <td>114.727700</td>
      <td>338</td>
      <td>3</td>
      <td>280.0</td>
      <td>55.0</td>
      <td>Brunei</td>
      <td>77.260145</td>
      <td>0.887574</td>
    </tr>
    <tr>
      <td>Burma</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-08-04 04:21:25</td>
      <td>21.916200</td>
      <td>95.956000</td>
      <td>311067</td>
      <td>10373</td>
      <td>220887.0</td>
      <td>79807.0</td>
      <td>Burma</td>
      <td>571.711409</td>
      <td>3.334651</td>
    </tr>
    <tr>
      <td>Cambodia</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-08-04 04:21:25</td>
      <td>11.550000</td>
      <td>104.916700</td>
      <td>79051</td>
      <td>1471</td>
      <td>72145.0</td>
      <td>5435.0</td>
      <td>Cambodia</td>
      <td>472.822161</td>
      <td>1.860824</td>
    </tr>
    <tr>
      <td>Indonesia</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-08-04 04:21:25</td>
      <td>-0.789300</td>
      <td>113.921300</td>
      <td>3496700</td>
      <td>98889</td>
      <td>2873669.0</td>
      <td>524142.0</td>
      <td>Indonesia</td>
      <td>1278.390505</td>
      <td>2.828066</td>
    </tr>
    <tr>
      <td>Laos</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-08-04 04:21:25</td>
      <td>19.856270</td>
      <td>102.495496</td>
      <td>7015</td>
      <td>7</td>
      <td>3392.0</td>
      <td>3616.0</td>
      <td>Laos</td>
      <td>96.418748</td>
      <td>0.099786</td>
    </tr>
    <tr>
      <td>Malaysia</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-08-04 04:21:25</td>
      <td>4.210484</td>
      <td>101.975766</td>
      <td>1163291</td>
      <td>9598</td>
      <td>950029.0</td>
      <td>203664.0</td>
      <td>Malaysia</td>
      <td>3594.176209</td>
      <td>0.825073</td>
    </tr>
    <tr>
      <td>Philippines</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-08-04 04:21:25</td>
      <td>12.879721</td>
      <td>121.774017</td>
      <td>1612541</td>
      <td>28141</td>
      <td>1521263.0</td>
      <td>63137.0</td>
      <td>Philippines</td>
      <td>1471.550496</td>
      <td>1.745134</td>
    </tr>
    <tr>
      <td>Singapore</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-08-04 04:21:25</td>
      <td>1.283300</td>
      <td>103.833300</td>
      <td>65315</td>
      <td>38</td>
      <td>63252.0</td>
      <td>2025.0</td>
      <td>Singapore</td>
      <td>1116.430267</td>
      <td>0.058180</td>
    </tr>
    <tr>
      <td>Vietnam</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-08-04 04:21:25</td>
      <td>14.058324</td>
      <td>108.277199</td>
      <td>174461</td>
      <td>2071</td>
      <td>50831.0</td>
      <td>121559.0</td>
      <td>Vietnam</td>
      <td>179.231087</td>
      <td>1.187085</td>
    </tr>
  </tbody>
</table>
</div>



There are many useless columns as you could tell with `NaN`. Most likely, we would not need variables such as `Lat` and `Long_`. We can thus remove these columns.


```python
asean_df_dropped = asean_df.drop(columns = ['FIPS', 'Admin2','Province_State', 'Last_Update', 'Lat', 'Long_', 'Combined_Key'])
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
      <th>Confirmed</th>
      <th>Deaths</th>
      <th>Recovered</th>
      <th>Active</th>
      <th>Incident_Rate</th>
      <th>Case_Fatality_Ratio</th>
    </tr>
    <tr>
      <th>Country_Region</th>
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
      <td>338</td>
      <td>3</td>
      <td>280.0</td>
      <td>55.0</td>
      <td>77.260145</td>
      <td>0.887574</td>
    </tr>
    <tr>
      <td>Burma</td>
      <td>311067</td>
      <td>10373</td>
      <td>220887.0</td>
      <td>79807.0</td>
      <td>571.711409</td>
      <td>3.334651</td>
    </tr>
    <tr>
      <td>Cambodia</td>
      <td>79051</td>
      <td>1471</td>
      <td>72145.0</td>
      <td>5435.0</td>
      <td>472.822161</td>
      <td>1.860824</td>
    </tr>
    <tr>
      <td>Indonesia</td>
      <td>3496700</td>
      <td>98889</td>
      <td>2873669.0</td>
      <td>524142.0</td>
      <td>1278.390505</td>
      <td>2.828066</td>
    </tr>
    <tr>
      <td>Laos</td>
      <td>7015</td>
      <td>7</td>
      <td>3392.0</td>
      <td>3616.0</td>
      <td>96.418748</td>
      <td>0.099786</td>
    </tr>
    <tr>
      <td>Malaysia</td>
      <td>1163291</td>
      <td>9598</td>
      <td>950029.0</td>
      <td>203664.0</td>
      <td>3594.176209</td>
      <td>0.825073</td>
    </tr>
    <tr>
      <td>Philippines</td>
      <td>1612541</td>
      <td>28141</td>
      <td>1521263.0</td>
      <td>63137.0</td>
      <td>1471.550496</td>
      <td>1.745134</td>
    </tr>
    <tr>
      <td>Singapore</td>
      <td>65315</td>
      <td>38</td>
      <td>63252.0</td>
      <td>2025.0</td>
      <td>1116.430267</td>
      <td>0.058180</td>
    </tr>
    <tr>
      <td>Vietnam</td>
      <td>174461</td>
      <td>2071</td>
      <td>50831.0</td>
      <td>121559.0</td>
      <td>179.231087</td>
      <td>1.187085</td>
    </tr>
  </tbody>
</table>
</div>



Description of each field (from the [github](https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data)) 

1. **Country_Region**: Country, region or sovereignty name. The names of locations included on the Website correspond with the official designations used by the U.S. Department of State.


2. **Confirmed**: Total Counts include confirmed and probable (where reported).


3. **Deaths**: Total Counts include confirmed and probable (where reported).


4. **Recovered**: Recovered cases are estimates based on local media reports, and state and local reporting when available, and therefore may be substantially lower than the true number. US state-level recovered cases are from [COVID Tracking Project](https://covidtracking.com/).


5. **Active**: Active cases = total cases - total recovered - total deaths.


6. **Incident_Rate**: Incidence Rate = cases per 100,000 persons.


7. **Case_Fatality_Ratio (%)**: Case-Fatality Ratio (%) = Number recorded deaths / Number cases.



All cases, deaths, and recoveries reported are based on the date of initial report. Exceptions to this are noted in the "Data Modification" and "Retrospective reporting of (probable) cases and deaths" subsections below.
