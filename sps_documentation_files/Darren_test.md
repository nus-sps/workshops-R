---
sort: 4
---

# Visualisation of Data using R

# Loading in iris dataset

For the purposes of this tutorial, we are going to be using the _Iris_ flower dataset introduced by Ronald Fisher in his 1936 paper _The use of multiple measurementsi n taxonomic problems_.

We can try loading in this built-in dataset in R. Like so:

```R
data("iris")
```

## Inspecting the dataset
This dataset contains Sepal and Petal length / width of different Species of flowers _Iris setosa_, _versicolor_, and _virginica_

We can thus inspect the dataset like this:

```R
head(iris)
```

|  | Sepal.Length  | Sepal.Width  | Petal.Length  | Petal.Width  | Species  |
| -- | ------------- | ------------ | ------------- | ------------ | -------- |
| 1  | 5.1           | 3.5          | 1.4           | 0.2          | setosa   |
| 2  | 4.9           | 3.0          | 1.4           | 0.2          | setosa   |
| 3  | 4.7           | 3.2          | 1.3           | 0.2          | setosa   |
| 4  | 4.6           | 3.1          | 1.5           | 0.2          | setosa   |
| 5  | 5.0           | 3.6          | 1.4           | 0.2          | setosa   |
| 6  | 5.4           | 3.9          | 1.7           | 0.4          | setosa   |


The next step in exploring datasets is to know and understand what the different variables are referring to, such as Sepal Length, Sepal Width, Petal Lengths and Petal Width!

### Optional Information
The dataset numbers are all in centimeters (cm), and the different variables should look foreign to people not well versed in plant morphology. Luckily for us, since this is a well-known dataset, the internet should have figures explaining what each variables mean.

![iris_variable_explain](https://static.packt-cdn.com/products/9781789539462/graphics/9cede6e3-0932-430a-a17e-d30025eb2b02.png)

How handy! [This website](https://subscription.packtpub.com/book/big_data_and_business_intelligence/9781789539462/3/ch03lvl1sec17/text-classification) contains an image on what Sepal / Petal length and widths mean for each row!

## Testing some variable
Perhaps you have this dataset, you think `Sepal.Length` and `Petal.Width` are related in someway, we can visualise this quickly by using the `plot()` function:

```R
plot(iris$Sepal.Length, iris$Petal.Width)
```
![SLvsPw](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/irisSepalvsPetal.jpg)

Awesome! There seems to be some sort of association. What if we want to explore other combinations of our variables, such as `Sepal.Length` vs `Petal.Length` and so on and so forth? Luckily for us R has a function called `pairs()` to help us! By adding `panel = panel.smooth`, R would help us generate a "smooth" curve to help us better visualise correlations!

```R
pairs(iris, panel = panel.smooth)
``` 
![irisPairsPlot](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/pairsiris.jpg)

It seems that `Petal.Length` and `Petal.Width` has the strongest positive association from each other. This is to be expected as we would expect a flower with a longer petal length to have a longer petal width as well.

It also seems that `Sepal.Length` and `Petal.Length` have some sort of correlation as well. Lets use these two variables for our examples later!

## Solidifying our research question
Before we proceed any further, it is important in any experiment that we have a solid research question in mind. This is because the type of data presented will help answer your research question. 

Lets say we had a basic research question "Are the lengths of the petals associated with the lengths of sepal in _I. setosa_, _I. versicolor_, and _ I. virginica_?" So while we're doing data collection, we collected other variables as well (see table above).

After data collection, we can casually plot `Sepal.Length` against `Petal.Length`.
![SLvsPL](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/irisSepalLvsPetalL.jpg)

It seems to me that Petal Length and Sepal Length have a linear positive correlation with each other!

## Beautifying the graphs

If you were Ronald Fisher and wanted to present about the positive correlation of Sepal Length with Petal Length by using the graph presented above, you will probably be shot.

Luckily, since most of the R community have agreed that base R plotting is terrible for presentations. A very handy package called `ggplot2` was created.

If you have not installed `ggplot2` in R, you can install it using the following command then load it in.

```R
install.packages("ggplot2") #This is only if you have not installed it before
library(ggplot2)
```

The cool thing about `ggplot2` is that it allows for a very "modular" way of adding to the graph. We first specify the dataframe in which ggplot should look in, in our case `iris`, followed by the "global" aesthetics layer using `aes()`.

We want our x-axis to be `Sepal.Length` and y-axis to be `Petal.Length`

So our base syntax for our example would look like this:

```R
iris_PetalLengthvsSepalLength = ggplot(iris, aes(x=Sepal.Length, y = Petal.Length))

#To view the graph you can just run
iris_PetalLengthvsSepalLength
```

![blankggplot](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/Blankggplot2.jpg)

As you can tell, the plot is blank! This is because we only told `ggplot` to initialise a blank canvas, the next thing we want `ggplot` to do is to add our points! We can do this by using this `geom_point()`:

```R
#There are two ways to do this. The first way is 
iris_PetalLengthvsSepalLength = ggplot(iris, aes(x=Sepal.Length, y = Petal.Length)) +
                                geom_point()

#The second way is, assuming you already defined the variable of iris_PetalLengthvsSepalLength before,
iris_PetalLengthvsSepalLength = iris_PetalLengthvsSepalLength + geom_point()

#Like always lets view iris_PetalLengthvsSepalLength
iris_PetalLengthvsSepalLength
```
![geompointExample](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/iris_PetalLengthvsSepalLength.jpg)


Great, this is the exact same graph as above. Except this has **COLOUR**. There are a few things we can do to make this graph look more presentable. For your information, `geom_point()` can take an additional argument to change the shape and size of your dots if they ever look too small! You can experiment with it yourself, it'll look something like this `geom_point(size = 5, shape = 21)`

- [ ] Label size for the numbers
- [ ] Naming of X- and Y-axis
- [ ] Title / subtitle


### Changing the label size
The first issue that is very obvious is that the labels on the x- and y-axis are very small and may not be readable by people. So let us change that using `theme()`:

```R
#Once again, there are two ways of doing this, you can either build the graph in 1 go 
iris_PetalLengthvsSepalLength = ggplot(iris, aes(x=Sepal.Length, y = Petal.Length)) +
                                geom_point() + theme() +
                                theme(axis.text=element_text(size=20)) + 
                                theme(axis.title=element_text(size=25))



#Or make it modular
iris_PetalLengthvsSepalLength = iris_PetalLengthvsSepalLength + theme() +  theme(axis.text=element_text(size=20))
iris_PetalLengthvsSepalLength = iris_PetalLengthvsSepalLength + theme(axis.title=element_text(size=25))

#Like always lets view iris_PetalLengthvsSepalLength
iris_PetalLengthvsSepalLength
```
![Change_Label_Size](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/PLvsSLChangeSize.jpg)


`theme(axis.text=element_text(size=20))` changes the numbers on the x- and y-axis whereas `theme(axis.title=element_text(size=25))` changes the size of the x- and y-axis labels!

So to look at our checklist real quick
- [x] Label size for the numbers
- [ ] Naming of X- and Y-axis
- [ ] Title / subtitle


### Naming of X- and Y-axis & Title / subtitle
Luckily for us, since the dataframe is named appropriately, most readers would know the x- and y-axis are representing Sepal and Petal length. **BUT**, readers would not know the units. It is often good practice to rename your axis to be readable by everyone.

Lets rename the axis so that they portray the right information from the get go.
```R
#You can either do this
iris_PetalLengthvsSepalLength = ggplot(iris, aes(x=Sepal.Length, y = Petal.Length)) +
                                geom_point() + theme() +
                                theme(axis.text=element_text(size=20)) + 
                                theme(axis.title=element_text(size=25)) +
                                xlab('Length of Sepal (cm)') + ylab('Length of Petal (cm)')

#or do this if you already have iris_PetalLengthvsSepalLength defined earlier.
iris_PetalLengthvsSepalLength = iris_PetalLengthvsSepalLength + xlab('Length of Sepal (cm)') + ylab('Length of Petal (cm)')

#Like always lets view iris_PetalLengthvsSepalLength
iris_PetalLengthvsSepalLength
```
![Renamed_Axis_include_units](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/iris_PetalLengthvsSepalLengthAxisLabels.jpg)

Awesome, now with one look, readers can guess what the graph is about. But to make it even clearer, we will need to add a title or a subtitle to the graph:

```R
#Because Iris is the genus, when typing it, they need to be italicised this code snippet below will give you an example.
subtitle_iris = expression(paste("of various ",italic("Iris "), 'flower species'))

#Once again, you can do this 
iris_PetalLengthvsSepalLength = ggplot(iris, aes(x=Sepal.Length, y = Petal.Length)) +
                                geom_point() + theme() +
                                theme(axis.text=element_text(size=20)) + 
                                theme(axis.title=element_text(size=25)) +
                                xlab('Length of Sepal (cm)') + ylab('Length of Petal (cm)') + 
                                labs(title = "Length of Petals (cm) vs Length of Sepals (cm)", subtitle = subtitle_iris) +
                                theme(plot.title  = element_text(size=30)) +
                                theme(plot.subtitle  = element_text(size=20))


#Or do this to add on
iris_PetalLengthvsSepalLength = iris_PetalLengthvsSepalLength + labs(title = "Length of Petals (cm) vs Length of Sepals (cm)", subtitle = subtitle_iris)
iris_PetalLengthvsSepalLength = iris_PetalLengthvsSepalLength + theme(plot.title  = element_text(size=30))
iris_PetalLengthvsSepalLength = iris_PetalLengthvsSepalLength + theme(plot.subtitle  = element_text(size=20))

#Like always lets view iris_PetalLengthvsSepalLength
iris_PetalLengthvsSepalLength
```
![Added_TitlenSubtitle](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/iris_PLvsSLTitle.jpg)


> Editor note: I had to increase the size of the graph here while saving so I changed the size of the points by using the command `geom_point(size = 4)`


Cool, our checklist is done!
- [x] Label size for the numbers
- [x] Naming of X- and Y-axis
- [x] Title / subtitle

### Giving meaning to the graph

Ok we have a decent graph generated, but it does not really tell the reader anything. Linking back to our research question, we want to show that there is a linear association between length of petal and length of sepal of various _Iris_ flower species. The easiest way we can do this is by adding a best-fit linear regression line!

```R
#Once again, you can do this 
iris_PetalLengthvsSepalLength = ggplot(iris, aes(x=Sepal.Length, y = Petal.Length)) +
                                geom_point() + theme() +
                                theme(axis.text=element_text(size=20)) + 
                                theme(axis.title=element_text(size=25)) +
                                xlab('Length of Sepal (cm)') + ylab('Length of Petal (cm)') + 
                                labs(title = "Length of Petals (cm) vs Length of Sepals (cm)", subtitle = subtitle_iris) +
                                theme(plot.title  = element_text(size=30)) +
                                theme(plot.subtitle  = element_text(size=20)) +
                                stat_smooth(method='lm')

#Or do this to add on
iris_PetalLengthvsSepalLength = iris_PetalLengthvsSepalLength + stat_smooth(method='lm')


#Like always lets view iris_PetalLengthvsSepalLength
iris_PetalLengthvsSepalLength

#The dark grey borders around the blue linear line indicates the confidence interval for each point on that line.
#If you would like to remove, you can use this function call
#stat_smooth(method='lm', se = FALSE) instead of stat_smooth(method='lm')
#the method = 'lm' here specifies which model to fit the data with!
```
![Added_stat_smooth_line](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/iris_PLvsSLLMline.jpg)

Let us compare with our base graph from earlier to the one we have now!

![comparison_base_ggplot](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/comparisonggplotbase.png)

Awesome! With one look, readers can tell exactly what they are looking at and what message you would want them to takeaway! In this case, as `Sepal Length` increases, `Petal Length` increases. 

#### Additional info

In the event that you have other ways you would like to fit your data (since not all data are linearly associated), you can still fit your data after generating a model. In this example, I have generated a linear regression model, but it can be any type of model and it'll still work!

```R
#Generating the simplest linear regression model
iris_lm = lm(Petal.Length ~ Sepal.Length, data = iris)
summary(iris_lm)

#Generating datapoints and putting them in the same dataframe as iris for accessibility
iris.predict = cbind(iris, predict(iris_lm, interval = 'confidence'))
iris_withlm = ggplot(iris.predict, aes(x=Sepal.Length, y = Petal.Length))+
              geom_point(size = 4) + 
              geom_line(aes(Sepal.Length, fit),color="blue", size = 1.5) + theme() +
              theme(axis.text=element_text(size=20)) + 
              theme(axis.title=element_text(size=25)) +
              xlab('Length of Sepal (cm)') + ylab('Length of Petal (cm)') + 
              labs(title = "Length of Petals (cm) vs Length of Sepals (cm)", subtitle = subtitle_iris) +
              theme(plot.title  = element_text(size=30)) +
              theme(plot.subtitle  = element_text(size=20)) 

iris_withlm
```

## Visualising Categorical Variables
In the previous section, both variables shown are continuous variables. Meaning they could take any number. What if one of the variables is categorical, like `Species`?

In the `pairs()` plot that is provided all the way to the top, you would notice that the `Species` of _Iris_ has some form of correlation with both `Sepal.Length` and `Petal.Length`.

So, if our research question was to investigate the `Sepal.Length` and `Petal.Length` (continuous variable) between `Species` (categorical variables), we can modify some of our code from the previous section to work!

One of the ways to visualise continous variables against categorical variables, is to use a boxplot.

For the sake of simplicity of the tutorial, I would not be adding `theme()`.
```R
#This was the previous code showing continous variable against another continuous variable
iris_PetalLengthvsSepalLength = ggplot(iris, aes(x=Sepal.Length, y = Petal.Length)) +
                                geom_point() +
                                stat_smooth(method='lm')

iris_PetalvsSpecies = ggplot(iris, aes(x = Species, y = Petal.Length)) +
                      geom_boxplot()

iris_SepalvsSpecies = ggplot(iris, aes(x = Species, y = Sepal.Length)) +
                      geom_boxplot()

#Call these two graphs to view them... right?
iris_PetalvsSpecies
iris_SepalvsSpecies                      
```

### Plotting 2 ggplot graphs in the same window

Oh no problem, we cannot visualise these two graphs at the same time! Your first instinct might be to use `par(mfrow=c(1,2))` but that will not work for `ggplot2` graphs. What we need is `gridExtra`

Install `gridExtra` and load it if you have not:

```R
install.packages('gridExtra')
library(gridExtra)
```

Then displaying the graphs is as simple as 1 line of code:
```R
grid.arrange(iris_PetalvsSpecies,iris_SepalvsSpecies,ncol=2)
#There are fancier ways of arranging your graphs using grid.arrange() using matrices
#But I will not be covering it here as it will take very long
```
![grid_arrange_boxplots](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/iris_PetalvsSpeciesvsSepal.jpg)


Wow! It seems like all three species of _Iris_ are positively associated. With red being _I. Setosa_, green being _I. Versicolor_ and blue being _I. virginica_. There is one thing left! Thats right, the legend size. Lets fix that real quick

```R
iris_PLSL_col = iris_PLSL_col + theme(legend.text = element_text(size = 20)) + theme( legend.title = element_text(size = 25))
#There are other aspects you can tweak for the legend, such as background colour and location!


iris_PLSL_col
```
![Rescaled_Legend](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/iris_PLSL_col_legend.jpg)

Amazing! With this graph, this looks beautiful. At first glance, anyone can immediately understand the following points:

- Each species of _Iris_ flower, the `Petal Length` and `Sepal Length` are positively associated
- Weak association for _I. setosa_ 
- Strong association for _I. versicolor_ and _I. virginica_
- _I. virginica_ have the longest Petal and Sepal on average as compared to the other three species

Text can be **bold**, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

There should be whitespace between paragraphs. There should be whitespace between paragraphs. There should be whitespace between paragraphs. There should be whitespace between paragraphs.

There should be whitespace between paragraphs. There should be whitespace between paragraphs. There should be whitespace between paragraphs. There should be whitespace between paragraphs.

> There should be no margin above this first sentence.
>
> Blockquotes should be a lighter gray with a gray border along the left side.
>
> There should be no margin below this final sentence.

# Header 1

This is a normal paragraph following a header. Bacon ipsum dolor sit amet t-bone doner shank drumstick, pork belly porchetta chuck sausage brisket ham hock rump pig. Chuck kielbasa leberkas, pork bresaola ham hock filet mignon cow shoulder short ribs biltong.

## Header 2

> This is a blockquote following a header. Bacon ipsum dolor sit amet t-bone doner shank drumstick, pork belly porchetta chuck sausage brisket ham hock rump pig. Chuck kielbasa leberkas, pork bresaola ham hock filet mignon cow shoulder short ribs biltong.

### Header 3

```
This is a code block following a header.
```

#### Header 4

- This is an unordered list following a header.
- This is an unordered list following a header.
- This is an unordered list following a header.

##### Header 5

1. This is an ordered list following a header.
2. This is an ordered list following a header.
3. This is an ordered list following a header.

###### Header 6

| What    | Follows  |
| ------- | -------- |
| A table | A header |
| A table | A header |
| A table | A header |

---

There's a horizontal rule above and below this.

---

Here is an unordered list:

- Salt-n-Pepa
- Bel Biv DeVoe
- Kid 'N Play

And an ordered list:

1. Michael Jackson
2. Michael Bolton
3. Michael Bublé

And an unordered task list:

- [x] Create a sample markdown document
- [x] Add task lists to it
- [ ] Take a vacation

And a "mixed" task list:

- [ ] Steal underpants
- ?
- [ ] Profit!

And a nested list:

- Jackson 5
  - Michael
  - Tito
  - Jackie
  - Marlon
  - Jermaine
- TMNT
  - Leonardo
  - Michelangelo
  - Donatello
  - Raphael

Definition lists can be used with HTML syntax. Definition terms are bold and italic.

<dl>
    <dt>Name</dt>
    <dd>Godzilla</dd>
    <dt>Born</dt>
    <dd>1952</dd>
    <dt>Birthplace</dt>
    <dd>Japan</dd>
    <dt>Color</dt>
    <dd>Green</dd>
</dl>

---

Tables should have bold headings and alternating shaded rows.

| Artist          | Album          | Year |
| --------------- | -------------- | ---- |
| Michael Jackson | Thriller       | 1982 |
| Prince          | Purple Rain    | 1984 |
| Beastie Boys    | License to Ill | 1986 |

If a table is too wide, it should condense down and/or scroll horizontally.

<!-- prettier-ignore-start -->

| Artist            | Album           | Year | Label       | Awards   | Songs     |
|-------------------|-----------------|------|-------------|----------|-----------|
| Michael Jackson   | Thriller        | 1982 | Epic Records | Grammy Award for Album of the Year, American Music Award for Favorite Pop/Rock Album, American Music Award for Favorite Soul/R&B Album, Brit Award for Best Selling Album, Grammy Award for Best Engineered Album, Non-Classical | Wanna Be Startin' Somethin', Baby Be Mine, The Girl Is Mine, Thriller, Beat It, Billie Jean, Human Nature, P.Y.T. (Pretty Young Thing), The Lady in My Life |
| Prince            | Purple Rain     | 1984 | Warner Brothers Records | Grammy Award for Best Score Soundtrack for Visual Media, American Music Award for Favorite Pop/Rock Album, American Music Award for Favorite Soul/R&B Album, Brit Award for Best Soundtrack/Cast Recording, Grammy Award for Best Rock Performance by a Duo or Group with Vocal | Let's Go Crazy, Take Me With U, The Beautiful Ones, Computer Blue, Darling Nikki, When Doves Cry, I Would Die 4 U, Baby I'm a Star, Purple Rain |
| Beastie Boys      | License to Ill  | 1986 | Mercury Records | noawardsbutthistablecelliswide | Rhymin & Stealin, The New Style, She's Crafty, Posse in Effect, Slow Ride, Girls, (You Gotta) Fight for Your Right, No Sleep Till Brooklyn, Paul Revere, Hold It Now, Hit It, Brass Monkey, Slow and Low, Time to Get Ill |

<!-- prettier-ignore-end -->

---

Code snippets like `var foo = "bar";` can be shown inline.

Also, `this should vertically align` ~~`with this`~~ ~~and this~~.

Code can also be shown in a block element.

```
var foo = "bar";
```

Code can also use syntax highlighting.

```javascript
var foo = "bar";
```

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```javascript
var foo =
  "The same thing is true for code with syntax highlighting. A single line of code should horizontally scroll if it is really long.";
```

Inline code inside table cells should still be distinguishable.

| Language   | Code               |
| ---------- | ------------------ |
| Javascript | `var foo = "bar";` |
| Ruby       | `foo = "bar"`      |

---

Small images should be shown at their actual size.

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

Large images should always scale down and fit in the content container.

![Branching](https://guides.github.com/activities/hello-world/branching.png)

```
This is the final element on the page and there should be no margin below this.
```
