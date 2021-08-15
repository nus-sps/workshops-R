---
sort: 6
---

# Misrepresentations of COVID19 Data (and how to fix them)

## Kansas 7-Day Rolling Average of Daily Cases

On August 6, 2020, the following image ![pic](https://www.tandfonline.com/na101/home/literatum/publisher/tandf/journals/content/ujse21/0/ujse21.ahead-of-print/26939169.2021.1915215/20210519/images/large/ujse_a_1915215_f0001_c.jpeg) created by Kansas Department of Health and Environment to show daily cases of COVID19 in Kansas (Engledowl & Weiland, 2021).

At first glance, there _seems_ to be nothing wrong with this graph / plot. It is just a regular plot showing wearing masks will result in a significant decline in COVID19 cases over three weeks as compared to states with no mandatory mask mandates.

However, on closer inspection, the y-axis for both graphs are not the same! The minimum cases for states with mask mandates is "15" while the highest number of cases for states with no mask mandate is around "10". This tells us that states with mask mandates actually has higher cases of COVID19!

Even though there is nothing **technically** wrong with showing this graph, it is extremely misleading as the message this graph was trying to show is that wearing masks would result in a lower number of cases, rather than mask wearing causing a _decline_ of COVID19 cases!

Before we go about fixing the graph, we can recreate this "bad graph" in `python`! We are not going to go through what each line means, so feel free to skip to the next cell


```python
# import relevant packages
import pandas as pd
import matplotlib.pyplot as plt

# init the numbers by hardcoding, (it is not publicly available so...)
No_mask = [9.75, 9.2, 9.4, 9.75, 9.9, 9.5, 9.5, 9, 8.5, 8.5, 8.75, 8.5, 9.9, 9.9, 10.1, 9.5, 9.55, 9.6, 10, 8.8, 9, 8.8, 9.2]
mask = [25.25, 19.75, 19.7, 20.5, 19.75,19.75, 20.5, 19.9,20.6,21.5,19.75,19.75, 20.5, 19,19.6,17,16.2, 16.4, 16.5, 16,16.1,15.75,15.9]

# Generate the same dates using pandas
date = pd.date_range(start="2020-07-12",end="2020-08-03")

# Initiate a subplot because we know we want two axis
fig, ax1 = plt.subplots(figsize = (9,5))

# This converter is here to allow for matplotlib to convert the date properly
pd.plotting.register_matplotlib_converters()

# Plotting the Mask Mandates first
color = 'red'
ax1.plot(date, mask, color=color)
ax1.set_xlabel('date')
ax1.set_ylabel('Mask', color=color)
ax1.tick_params(axis='y', labelcolor=color) # This colours the axis too!

ax2 = ax1.twinx()  # Create a new Axes object which uses the same x-axis as ax1

color = 'blue'
ax2.plot(date, No_mask, color=color)
ax2.set_ylabel('No Mask', color=color)  # x-label is already defined above so we just do y-label here
ax2.tick_params(axis='y', labelcolor=color) # This colours the axis too!


ax1.set_ylim(15,25.5) # setting individual ylims
ax2.set_ylim(4,14.5) # for both axis so we get the "misrepresentation"

plt.suptitle('Kansas COVID-19 7-Day Rolling Average of Daily Cases/Per 100K Population', fontsize = 18)
plt.title('\nMask Counties Vs. No-Mask Mandate Counties')
fig.tight_layout()  # makes everything nice and uncropped
plt.grid()
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/apply%20covid/Misrepp/output_1_0.png)
    


We have now generated "misrepresented graph". Now lets fix this. This is a very simple fix! Just plot the same numbers on the same `Axes` object like we have been doing previously!


```python
import pandas as pd
import matplotlib.pyplot as plt

# init the numbers by hardcoding, (it is not publicly available so...)
No_mask = [9.75, 9.2, 9.4, 9.75, 9.9, 9.5, 9.5, 9, 8.5, 8.5, 8.75, 8.5, 9.9, 9.9, 10.1, 9.5, 9.55, 9.6, 10, 8.8, 9, 8.8, 9.2]
mask = [25.25, 19.75, 19.7, 20.5, 19.75,19.75, 20.5, 19.9,20.6,21.5,19.75,19.75, 20.5, 19,19.6,17,16.2, 16.4, 16.5, 16,16.1,15.75,15.9]

# Generate the same dates using pandas
date = pd.date_range(start="2020-07-12",end="2020-08-03")

# There is actually no need to create an Axes object, but I want to show what changed
# hence I did it.
fig, ax1 = plt.subplots(figsize = (9,5))

# This converter is here to allow for matplotlib to convert the date properly
pd.plotting.register_matplotlib_converters()

##################################################################
# This is start of the part that changed when you refer to above #
##################################################################
# Plotting the numbers using ax1 object
ax1.plot(date, mask, label = 'With mask', color = 'red')
ax1.plot(date, No_mask, label = 'Without mask', color = 'blue')

# Setting the labels
ax1.set_xlabel('date')
ax1.set_ylabel('Number of Cases')
ax1.tick_params(axis='y')
################################################################
# This is end of the part that changed when you refer to above #
################################################################

plt.suptitle('Kansas COVID-19 7-Day Rolling Average of Daily Cases/Per 100K Population', fontsize = 18)
plt.title('\nMask Counties Vs. No-Mask Mandate Counties')
fig.tight_layout()  # makes everything nice and uncropped
plt.grid()
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/apply%20covid/Misrepp/output_3_0.png)
    


## Georgia Department of Public Health

Georgia Department of Public Health posted this graph sometime in May 2020. ![pic](https://pbs.twimg.com/media/EYMC7PBU8AAn0yA?format=jpg&name=medium) (image taken from Bullshit, 2020)

This plot was criticised on the basis that it was borderline data manipulation. At first glance, this bar chart shows that COVID19 cases in the top five counties in the state were dropping over time.

**BUT** on closer inspection of the x-axis shows that the dates were not in chronological order?! 28th April was shown first before 27th April?

> This example of a misleading use of statistics is perhaps one of the more clear cases of intent to mislead, despite attempts of the administration to make it appear accidental **- Engledowl & Weiland, 2021**

For reasons that it is **way** too much work for everyone to recreate this misleading barchart in Python, we are going to jump straight into "fixing" this graph.

1. First we are going to grab a separate dataset from our favorite github link
2. Then we are going to subset it to just in Georgia


```python
US_link = 'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_US.csv'
covid19_US_data = pd.read_csv(US_link)
georgia_df = covid19_US_data.loc[covid19_US_data['Province_State'] == 'Georgia']
georgia_df.head()
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
      <th>UID</th>
      <th>iso2</th>
      <th>iso3</th>
      <th>code3</th>
      <th>FIPS</th>
      <th>Admin2</th>
      <th>Province_State</th>
      <th>Country_Region</th>
      <th>Lat</th>
      <th>Long_</th>
      <th>...</th>
      <th>7/28/21</th>
      <th>7/29/21</th>
      <th>7/30/21</th>
      <th>7/31/21</th>
      <th>8/1/21</th>
      <th>8/2/21</th>
      <th>8/3/21</th>
      <th>8/4/21</th>
      <th>8/5/21</th>
      <th>8/6/21</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>411</td>
      <td>84013001</td>
      <td>US</td>
      <td>USA</td>
      <td>840</td>
      <td>13001.0</td>
      <td>Appling</td>
      <td>Georgia</td>
      <td>US</td>
      <td>31.748472</td>
      <td>-82.289091</td>
      <td>...</td>
      <td>2417</td>
      <td>2428</td>
      <td>2435</td>
      <td>2435</td>
      <td>2435</td>
      <td>2449</td>
      <td>2464</td>
      <td>2480</td>
      <td>2489</td>
      <td>2500</td>
    </tr>
    <tr>
      <td>412</td>
      <td>84013003</td>
      <td>US</td>
      <td>USA</td>
      <td>840</td>
      <td>13003.0</td>
      <td>Atkinson</td>
      <td>Georgia</td>
      <td>US</td>
      <td>31.296335</td>
      <td>-82.875459</td>
      <td>...</td>
      <td>1101</td>
      <td>1105</td>
      <td>1114</td>
      <td>1114</td>
      <td>1114</td>
      <td>1121</td>
      <td>1127</td>
      <td>1131</td>
      <td>1139</td>
      <td>1146</td>
    </tr>
    <tr>
      <td>413</td>
      <td>84013005</td>
      <td>US</td>
      <td>USA</td>
      <td>840</td>
      <td>13005.0</td>
      <td>Bacon</td>
      <td>Georgia</td>
      <td>US</td>
      <td>31.554565</td>
      <td>-82.459365</td>
      <td>...</td>
      <td>1738</td>
      <td>1745</td>
      <td>1756</td>
      <td>1756</td>
      <td>1756</td>
      <td>1764</td>
      <td>1777</td>
      <td>1785</td>
      <td>1799</td>
      <td>1810</td>
    </tr>
    <tr>
      <td>414</td>
      <td>84013007</td>
      <td>US</td>
      <td>USA</td>
      <td>840</td>
      <td>13007.0</td>
      <td>Baker</td>
      <td>Georgia</td>
      <td>US</td>
      <td>31.326699</td>
      <td>-84.442188</td>
      <td>...</td>
      <td>268</td>
      <td>267</td>
      <td>267</td>
      <td>267</td>
      <td>267</td>
      <td>272</td>
      <td>274</td>
      <td>277</td>
      <td>279</td>
      <td>280</td>
    </tr>
    <tr>
      <td>415</td>
      <td>84013009</td>
      <td>US</td>
      <td>USA</td>
      <td>840</td>
      <td>13009.0</td>
      <td>Baldwin</td>
      <td>Georgia</td>
      <td>US</td>
      <td>33.068823</td>
      <td>-83.247017</td>
      <td>...</td>
      <td>4644</td>
      <td>4652</td>
      <td>4662</td>
      <td>4662</td>
      <td>4662</td>
      <td>4680</td>
      <td>4696</td>
      <td>4712</td>
      <td>4729</td>
      <td>4742</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 574 columns</p>
</div>



3. We would then need to subset the `georgia_df` to contain only the counties `Hall, Cobb, Fulton, Gwinnett, DeKalb`. This can be done using the `.isin` command we used in the previous sections!

4. Since we know how to plot with dates as our rows, we would need to transpose the dataframe using `.T` (like we did in the previous sections)!


```python
# Subsetting our dataset further to include the counties we want using .isin
georgia_df_filter = georgia_df[georgia_df['Admin2'].isin(['Hall', 'Cobb', 'Fulton','Gwinnett','DeKalb'])]

df_t = georgia_df_filter.T
df_t.head(6)
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
      <th>443</th>
      <th>453</th>
      <th>470</th>
      <th>477</th>
      <th>479</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>UID</td>
      <td>84013067</td>
      <td>84013089</td>
      <td>84013121</td>
      <td>84013135</td>
      <td>84013139</td>
    </tr>
    <tr>
      <td>iso2</td>
      <td>US</td>
      <td>US</td>
      <td>US</td>
      <td>US</td>
      <td>US</td>
    </tr>
    <tr>
      <td>iso3</td>
      <td>USA</td>
      <td>USA</td>
      <td>USA</td>
      <td>USA</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>code3</td>
      <td>840</td>
      <td>840</td>
      <td>840</td>
      <td>840</td>
      <td>840</td>
    </tr>
    <tr>
      <td>FIPS</td>
      <td>13067</td>
      <td>13089</td>
      <td>13121</td>
      <td>13135</td>
      <td>13139</td>
    </tr>
    <tr>
      <td>Admin2</td>
      <td>Cobb</td>
      <td>DeKalb</td>
      <td>Fulton</td>
      <td>Gwinnett</td>
      <td>Hall</td>
    </tr>
  </tbody>
</table>
</div>



Since we want our column names to be something more recognisable like the county names, we would need to do the following:

1. We need to set the row `Admin2` as the column name. This can be done using `.loc`.

2. We then need to subset our dates to the ones shown in the graph. This can also be done using `.loc`.


```python
#Changing the column name
df_t.columns = [df_t.loc['Admin2']]

df_t_date = df_t.loc['4/26/20':'5/9/20']

# 26 April to 9 May 2020


df_t_date.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Admin2</th>
      <th>Cobb</th>
      <th>DeKalb</th>
      <th>Fulton</th>
      <th>Gwinnett</th>
      <th>Hall</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>4/26/20</td>
      <td>1428</td>
      <td>1800</td>
      <td>2545</td>
      <td>1504</td>
      <td>1033</td>
    </tr>
    <tr>
      <td>4/27/20</td>
      <td>1483</td>
      <td>1855</td>
      <td>2680</td>
      <td>1545</td>
      <td>1098</td>
    </tr>
    <tr>
      <td>4/28/20</td>
      <td>1515</td>
      <td>1887</td>
      <td>2727</td>
      <td>1603</td>
      <td>1183</td>
    </tr>
    <tr>
      <td>4/29/20</td>
      <td>1571</td>
      <td>1970</td>
      <td>2770</td>
      <td>1720</td>
      <td>1242</td>
    </tr>
    <tr>
      <td>4/30/20</td>
      <td>1614</td>
      <td>2026</td>
      <td>2811</td>
      <td>1787</td>
      <td>1332</td>
    </tr>
  </tbody>
</table>
</div>



Then we can just plot this like a regular dataframe!


```python
# You can specify the colour using the color argument, alpha is the transparency of the graph
ax = df_t_date.plot.bar(figsize=(15, 6), color=['#5553B1', '#23878E', '#988739','#95572C', '#236CA9'], alpha = 0.9)

# This sets the background colour of the graph
ax.set_facecolor('#0D2E4F')

# Redo the legend so it looks nicer
ax.legend(["Cobb", "DeKalb", "Fulton", "Gwinnett", "Hall"], title = 'Georgia Counties')
ax.set_ylabel('Confirmed Cases', fontsize = 20)
ax.set_xlabel('Dates', fontsize = 20)
ax.set_title('Top 5 Counties with the Greatest Number of Confirmed COVID-19 Cases', fontsize = 25)
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/apply%20covid/Misrepp/output_11_0.png)
    


### References:

Bullshit, C. (2020, May 17). _One of the most misleading graphs we have ever Seen. The Georgia Department of public health has ordered the dates on the x axis not chronologically, but rather to create the impression of a decreasing number of cases over time._ Twitter. https://twitter.com/callin_bull/status/1261855753846927360?lang=en. 

Engledowl, C., &amp; Weiland, T. (2021). Data (mis)representation and COVID-19: Leveraging misleading data visualizations for Developing statistical Literacy Across Grades 6–16. _Journal of Statistics and Data Science Education_, 1–5. https://doi.org/10.1080/26939169.2021.1915215 
