---
sort: 1
---

# Matplotlib: Basic Plotting
## Utilizing arguments in matplotlib
### Using Markers, Linestyle and Color

From the previous section, we showed the basics of plotting two variables against each other. However, changing the aesthetics of the graph is also important in data visualisation / presentation. Some aesthetics include `marker` type, `linestyle` and `color`. These aesthetics are changed in the `plt.plot()` function as additional arguments.

For this example, we chose to have a '*' `marker`, 'dashed' `linestyle` and a 'r' `color` plot.
```python
x = [1,2,3]
y = [4,2,0]

plt.plot(x,y, marker = '*',linestyle = 'dashed',color = 'r')
plt.show()
```
![WorkshopImage2](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/basics%20plt/workshop2.png)

Using the same plot and values, we can also change the size of the points / marker using `markersize`, the width of the line using `linewidth` and changing the colour using the hex colour code.
```python
x = [1,2,3]
y = [4,2,0]

plt.plot(x,y , marker='*', linestyle = 'dashed', color = '#ff0000', markersize = 12, linewidth = 5)
plt.show()
```
![WorkshopImage3](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/basics%20plt/workshop3.png)

Assuming now we have a third variable `z` and we want to plot 'z against x' on the same graph. We can make use of the various aesthetic arguments shown before to differentiate the plots! 
```python
x = [1,2,3]
y = [4,2,0]
z = [6,2,4]


plt.plot(x,y , marker='*', linestyle = 'dashed', color = '#ff0000', markersize = 12, linewidth = 1)
plt.plot(x,z , marker='.', linestyle = '-', color = '#00ff00', markersize = 10, linewidth = 1)
plt.show()
```
![WorkshopImage4](https://raw.githubusercontent.com/darren1998s/darren1998s.github.io/main/assets/images/tfi/basics%20plt/workshop4.png)

