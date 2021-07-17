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
This dataset contains Sepal and Petal length / width of different Specieis of flowers _Iris setosa_, _versicolor_, and _virginica_

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

But first, let us plot this graph to see whats going on in more detail!
![SLvsPL](https://raw.githubusercontent.com/nus-sps/workshops-R/main/assets/images/irisSepalLvsPetalL.jpg)

It seems to me that Petal Length and Sepal Length have a linear positive correlation with each other!

## Beautifying the graphs

If you were Ronald Fisher and wanted to present about the positive correlation of Sepal Length with Petal Length by using the graph presented above, you will probably be shot.

Luckily, since most of the R community have agreed that base R plotting is terrible for presentations. A very handy package called `ggplot2`

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
