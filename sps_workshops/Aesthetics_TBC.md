# Data Visualisation: When to use what graph?

**Authors:** [Darren Teo](https://www.linkedin.com/in/darren-teo-3125871a1/), [Hillson Hung](https://www.linkedin.com/in/hillson-hung/)

**About the Authors:** Year 3 student in NUS in Special Programme in Science, Darren and Hillson are currently majoring in Life Sciences and Physics respectively.

**About this tutorial:** Data visualisation is all about presenting your data accurately and succinctly so that your audience can see what it means. In this section we provide some quick and easy guidelines to decide what to use to represent your data. Keep in mind that what we cover are not rigid rules that you must always follow, it is just a general guideline. The most important thing is not to get caught up in all the fancy graphs and charts and to present your data such that it tells a clear story.

## Different kinds of data

There are three main kinds of data, exclusively numerical, exclusively categorical and a mix of the two. There are many ways to represent numerical data, depending on the number of variables and whether it is ordered in some way or other. On the other hand, exclusively categorical data is usually harder to visualise, especially when there are multiple independent categorical variables. Below is a quick flowchart for which methods of data visualisation to use for the different kinds of data.

### Exclusively Numerical/Categorical Data Flowchart

```mermaid
graph LR
a{Type of data}-->b1 & b2
subgraph two[Dataset contains only categorical data]
b2(How many variables?)--> c2a(Single variable) & c2b(Multiple variables)
c2a--->c2a_plot[Bar Plot, Pie Chart]
c2b--->|Independent|c2b1_plot[Typical graphs are not very useful]
c2b--->|Subcategories or<br>hierachies exist|c2b2_plot[Bar Plot, Grouped Scatter Plot, Stacked Bar Plot]
end
subgraph one[Dataset contains only numerical data]
b1(How many variables?)-->c1a(Single variable) & c1b(Two variables) & c1c(Multiple variables)
c1c-->c1c_order(Ordered?)
c1c_order-->|No| c1c_order_no[Box Plot, Correlogram, Heatmap, Violin Plot]
c1c_order-->|Yes| c1b_order_yes
c1b-->c1b_order(Ordered?)
c1b_order-->|Yes| c1b_order_yes[Area Plot, Connected Scatter Plot, Line Plot]
c1b_order-->|No| c1b_order_no[Box Plot, Histogram, Scatter Plot, Violin Plot]
c1a-->c1a1(Time series?)
c1a1-->|Yes| c1b_order_yes
c1a1-->|No| c1a2_plot[Density Plot, Histogram]
end
```

### Mixed Numerical and Categorical Data Flowchart

```mermaid
    graph LR
    start{Mixed data types}-->a1(Single num<br>Single cat) & a2(Single cat<br>Multiple num) & a3(Multiple num<br>Multiple cat)
    subgraph mixed["Dataset contains both numerical (num) and categorical (cat) data"]
    a1-->a1a(Single data point per cat)
    a1a-->a1a_plot[Box Plot, Pie Chart]
    a1-->a1b(Multiple data points per cat)
    a1b-->a1b_plot[Box Plot, Density Plot, Histogram, Violin Plot]
    a2-->a2a(Not ordered)
    a2a-->a2a_plot[Box Plot, Correlogram, Grouped Scatter Plot, Violin Plot]
    a2-->a2b(A single num variable is ordered<br>or Time series)
    a2b-->a2b_plot[Area Plot, Connected Scatter Plot, Line Plot, Stacked Area Plot]
    a2-->a2c(Single num value per cat)
    a2c-->a2c_plot[Grouped Scatter Plot, Heatmap, Stacked Bar Plot]
    a3-->|Subcategories or<br>hierachies exist|a3b(How many num per subcat?)
    a3b-->|Single num per subcat|a2c_plot
    a3b-->|Multiple num per subcat|a3b2_plot[Box Plot, Violin Plot]
    a3--->|Independent|a3a[Typical graphs are not very useful]
    end
```

