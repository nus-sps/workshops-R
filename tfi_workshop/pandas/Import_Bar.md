---
sort: 1
---

# Importing Dataset & Bar Charts

## Importing Iris Dataset

We can import the dataset either by downloading the dataset or linking it straight from a source (like what we're going to do)


```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/iris.csv")

#Remember df.head() shows us the first 5 rows of the dataset.
df.head()
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
      <th>Sepal.Length</th>
      <th>Sepal.Width</th>
      <th>Petal.Length</th>
      <th>Petal.Width</th>
      <th>Species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <td>1</td>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <td>2</td>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <td>4</td>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
  </tbody>
</table>
</div>



## Bar Chart
### Species value_counts()

The basic plotting function is `pd.plot` which supports easy substitution of plot styles using the kind keyword argument.

We can first make a bar chart containing the number of each species of _Iris_ flowers found in our dataset.

Remember that `df['Species'].value_counts()` counts the number of unique elements in that column.


```python
df['Species'].value_counts().plot(kind='bar')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x156ffaf0>




    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/pandas/exploratory/output_3_1.png)
    


From this Bar Chart, we can see that in our dataset, there are 50 of each species in our dataset.

### Plotting average of Petal.Length

What if we want to plot a bar chart plotting average `Petal.Length` for each species of _Iris_?


```python
import numpy as np

grouped_species = df.groupby("Species")['Petal.Length']
grouped_species.mean().plot(kind = 'bar')

#Don't forget to add the y-axis label for clarity!
plt.ylabel('Petal.Length')
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/pandas/exploratory/output_5_0.png)
    


However, most barcharts, while counting averages, needs to have standard error. Since there is no function that calculates standard error for us, we would need to make our own function (`se`).

Recall that standard error is the formula:

$$se = \frac{\sigma}{\sqrt{n}}$$

sd = `np.std` and we can get `n` with `.count()`.


```python
def se(data):
    return np.std(data) / np.sqrt(data.count())

grouped_species.agg([np.mean, se])
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
      <th>mean</th>
      <th>se</th>
    </tr>
    <tr>
      <th>Species</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>setosa</td>
      <td>1.462</td>
      <td>0.024313</td>
    </tr>
    <tr>
      <td>versicolor</td>
      <td>4.260</td>
      <td>0.065788</td>
    </tr>
    <tr>
      <td>virginica</td>
      <td>5.552</td>
      <td>0.077265</td>
    </tr>
  </tbody>
</table>
</div>



Now we can plot and specify the error bars with the argument `yerr = 'se'`.


```python
grouped_species.agg([np.mean, se]).plot(kind = 'bar', yerr = 'se')

#Don't forget to add the y-axis label for clarity!
plt.ylabel('Petal.Length')
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/pandas/exploratory/output_9_0.png)
    
From the barchart above, we can conclude many things on first glance:

1. _I setosa_ has the lowest mean Petal Length, followed by _I versicolor_ then _I virginica_.

2. The standard error of Petal Length for each species are extremely low, signifying very little variance within species.
