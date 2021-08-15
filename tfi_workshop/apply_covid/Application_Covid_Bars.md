---
sort: 2
---

# Exploration of COVID19 dataset: Bar Chart

## Recap

First, customary importing of packages and data if you haven't already done so from the previous sections.


```python
import pandas as pd
import matplotlib.pyplot as plt

month_int = '08'
day_int = '03'

df = pd.read_csv(f"https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_daily_reports/{month_int}-{day_int}-2021.csv")
ASEAN_countries_list = ['Brunei', 'Cambodia', 'Indonesia', 'Laos', 'Malaysia', 'Burma', 'Philippines', 'Singapore', 'Vietnam']
asean_df = df[df['Country_Region'].isin(ASEAN_countries_list)]
asean_df.set_index('Country_Region', inplace = True)
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



As you can tell, the table is huge with ~4000 rows. Let us subset our data to just ASEAN countries.

Description of each field (from the [github](https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data)) 

1. **Country_Region**: Country, region or sovereignty name. The names of locations included on the Website correspond with the official designations used by the U.S. Department of State.


2. **Confirmed**: Total Counts include confirmed and probable (where reported).


3. **Deaths**: Total Counts include confirmed and probable (where reported).


4. **Recovered**: Recovered cases are estimates based on local media reports, and state and local reporting when available, and therefore may be substantially lower than the true number. US state-level recovered cases are from [COVID Tracking Project](https://covidtracking.com/).


5. **Active**: Active cases = total cases - total recovered - total deaths.


6. **Incident_Rate**: Incidence Rate = cases per 100,000 persons.


7. **Case_Fatality_Ratio (%)**: Case-Fatality Ratio (%) = Number recorded deaths / Number cases.



All cases, deaths, and recoveries reported are based on the date of initial report. Exceptions to this are noted in the "Data Modification" and "Retrospective reporting of (probable) cases and deaths" subsections below.

## Bar Charts

From the table itself, there are many types of barcharts we can plot out. Let us take a look at the `Incident_rate` against each ASEAN country.


```python
asean_df_dropped['Incident_Rate'].plot(kind = 'bar').set_ylabel('Incident Rate')
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/apply%20covid/Bars/output_5_0.png)
    


From this barchart, we can instantly tell that Malaysia has the **highest** incident rate at ~3,500. This means that they have about 3,500 confirmed cases for every 100,000 person in Malaysia. 

Likewise, Brunei and Laos have the **lowest** incident rate at less than a 100 confirmed cases for every 100,000 persons in their respective countries.

Hence, we can see that, assuming Malaysia, Brunei and Laos have the same population, Malaysia would have more of her people infected as compared to the other two countries.

Another interesting statistic we can see is `Case_Fatality_Ratio`.


```python
asean_df_dropped['Case_Fatality_Ratio'].plot(kind = 'bar').set_ylabel('Case Fatality Ratio (%)')
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/apply%20covid/Bars/output_7_0.png)
    


From **this** barchart, we can tell that Burma has the highest case to fatality ratio. and Singapore have the lowest case to fatality ratio.
