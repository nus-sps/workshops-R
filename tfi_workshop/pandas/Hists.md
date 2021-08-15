---
sort: 2
---

# Histograms

## Basic Histogram

First, customary importing of packages and data if you haven't already done so from the previous section.


```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/iris.csv")
```

Using the same syntax as the bar chart from the previous section, we can easily plot histograms in the same way.


```python
df['Petal.Length'].plot(kind='hist')

#Don't forget to label your x-axis
plt.xlabel('Petal.Length')
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/pandas/exploratory/output_3_0.png)
    


## Grouped Histograms

Likewise, like in our previous example, what if we want to check the distribution of `Petal.Length` grouped by each species of _Iris_ ? We can still make use of the `df.groupby()` function.


```python
grouped_species = df.groupby("Species")['Petal.Length']
grouped_species.plot(kind='hist')

#Don't forget to enable the legend so we know which colour refers to which species!
plt.legend()

#Don't forget to label your x-axis
plt.xlabel('Petal.Length')
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/pandas/exploratory/output_6_0.png)
    


Since we know _I. versicolor_ overlaps with _I. virginica_, we can set the transparency of the histogram so we can see exactly how they overlap! This can be done by specifying the `alpha` argument.


```python
grouped_species = df.groupby("Species")['Petal.Length']
grouped_species.plot(kind='hist', alpha = 0.5)

#Don't forget to enable the legend so we know which colour refers to which species!
plt.legend()

#Don't forget to label your x-axis
plt.xlabel('Petal.Length')
plt.show()
```


    
![png](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/pandas/exploratory/output_8_0.png)
    
From the histogram above, we can conclude many things on first glance:

1. _I. setosa_ has the lowest mean Petal Length, followed by _I. versicolor_ then _I. virginica_.

2. The distribution of Petal Length for _I. setosa_ is lower than both _I. versicolor_ and _I. virginica_.
