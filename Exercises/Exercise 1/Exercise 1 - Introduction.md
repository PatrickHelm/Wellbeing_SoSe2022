
# Exercise Number 1: Introduction to R

## Christopher Diebel & Jan-Hendrik Schmidt - ISE Darmstadt

## Helpful Links

-   :house_with_garden:
    [Home](https://github.com/tud-ise/Wellbeing_SoSe2022/blob/main/README.md)
-   :open_book: [Information about R](https://www.r-project.org/)
-   :open_book: [`dplyr`
    documentation](https://dplyr.tidyverse.org/reference/index.html)
-   :open_book: Further Reading [R for Data
    Science](https://r4ds.had.co.nz/), [R für
    Einsteiger](http://aproxy.ulb.tu-darmstadt.de:2058/book/index.cfm?bok_id=1993358)
    or [Einführung in
    R](https://methodenlehre.github.io/einfuehrung-in-R/die-r-sprache.html)
    (This is what this first exercise is largely based on)

## Preparation

Please work through the [Prerequisites
section](https://github.com/tud-ise/Wellbeing_SoSe2022/blob/main/README.md#0-prerequisites)
to be prepared for the first exercise.

## What is R?

R is a free software environment for statistical analysis.

### Graphical User Interface

Your opened RStudio should look something like the following:

<img src="./MD_IMG/RStudio_GUI.png" width="960" height="525/"/>

The RStudio GUI consists of several areas. In the console area, R code
can be entered, which is then interpreted (executed) by R. The `>`
character is the R prompt (prompt character). This means that you can
work with R interactively, using it as a calculator, for example:

``` r
2+3
```

    ## [1] 5

``` r
exp(1)
```

    ## [1] 2.718282

``` r
3/4
```

    ## [1] 0.75

In the upper right corner, besides the History, which lists all the
commands you have executed so far, we find the Environment section.
There you will find all the variables, data sets and functions that have
been defined.

### Packages

Before we start working with RStudio, we need to install some packages.
Packages provide additional functions that are not included in the base
R package. We first install a collection of packages for data
manipulation (`tidyr`, `dplyr`, `forcats`), for importing data files
(`readr`) and for graphics (`ggplot2`). These can all be installed
together with this command, which we enter in the console:

``` r
install.packages("tidyverse")
```

**This installation needs to run only once!**

After that we can load the packages like this:

``` r
library(tidyverse)
```

**You need to run this every time you open RStudio again!**

## Operators

### Arithmetic Operators

| Command   | Meaning                                   | Example (if appropriate) |
|-----------|-------------------------------------------|--------------------------|
| \+        | Addition                                  |                          |
| \-        | Subtraction                               |                          |
| \*        | Multiplication                            |                          |
| /         | Division                                  |                          |
| ^ or \*\* | Exponentiation                            |                          |
| x %\*% y  | Matrix Multiplication                     | c(1,4) %\*% c(3,5) == 23 |
| %/%       | Whole Number Division                     | 6 %/% 4 == 1             |
| %%        | Modulo (Remainder of a Division; x mod y) | 6 %% 4 == 2              |

### Logic Operators

| Command   | Meaning            | Example (if appropriate)   |
|-----------|--------------------|----------------------------|
| ==        | Equal              |                            |
| !=        | Unequal            |                            |
| \<        | Smaller than       |                            |
| \>        | Greater than       |                            |
| \<=       | Smaller equal      |                            |
| \>=       | Greater equal      |                            |
| &         | Logical AND        | (x & y)                    |
| \|        | Logical OR         | (x \| y)                   |
| !         | Logical NOT        | !x                         |
| xor(x, y) | Exclusive OR       | Either in x or y, not both |
| isTRUE(x) | Tests if x is true |                            |

The following graphic shows the use of the logical operators by means of
Venn diagrams. `x` always refers to the left circle, `y` to the right.
The selected area is always shown in dark. Source: [R for Data
Science](https://r4ds.had.co.nz/)

![Illustration of the Logical Operators](./MD_IMG/transform-logical.png)

## R Functions

In the following we will look at some of the standard R functions that
can be used and that make up the language in the first place. Each
function can be called in the documentation (even if it was inserted via
a library - more to that later). Just call the command `help(fct-name)`
(just type it into the console). There you get a first overview about
the function and its parameters.

``` r
help(seq)
```

### Numerical Functions

| Command              | Meaning              | Example (if appropriate)         |
|----------------------|----------------------|----------------------------------|
| abs(x)               | Absolute Value       |                                  |
| sqrt(x)              | Square root          |                                  |
| ceiling(x)           | Round Up             | ceiling(4.687) is 5              |
| floor(x)             | Round Off            | floor(4.687) is 4                |
| round(x, digits = n) | Rounding             | round(4.687, digits = 2) is 4.69 |
| log(x)               | Natural Logarithm    |                                  |
| log2(x)              | Logarithm to base 2  |                                  |
| log10(x)             | Logarithm to base 10 |                                  |
| exp(x)               | Exponential Function | e^x                              |

### Statistical Functions

These functions all have the argument `na.rm`, which by default takes
the value `FALSE`. This allows missing values to be taken into account,
i.e. missing values (na = not available) are not removed in this case
(rm = remove). These functions can all be applied to a vector (see
below).

| Command                | Meaning                                           |
|------------------------|---------------------------------------------------|
| mean(x, na.rm = FALSE) | Mean Value                                        |
| sd(x)                  | Standard Deviation                                |
| var(x)                 | Variance                                          |
| median(x)              | Median                                            |
| quantile(x, probs)     | Quantiles of X (probs: Vector with Probabilities) |
| sum(x)                 | Sum                                               |
| min(x)                 | Minimum Value (x_min)                             |
| max(x)                 | Maximum Value (x_max)                             |
| range(x)               | x_min and x_max                                   |

### Further Useful Functions

**Generation of a Vector**

`c(2,5,7,2,6)`

Vectors can be called as you like: `vector = c(2,5,7,2,6)`

Generation of a Sequence: `seq(from, to, by)`

``` r
seq(1, 5, 0.5)
```

    ## [1] 1.0 1.5 2.0 2.5 3.0 3.5 4.0 4.5 5.0

**Colon Operator**

`:` generates a regular sequence (i.e., sequence in steps of one)

``` r
1:6
```

    ## [1] 1 2 3 4 5 6

**Repetition of X**

`rep(x, times, each)`

-   times: the sequence is repeated n times

-   each: each element is repeated n times

``` r
rep(1:6, times=2)
```

    ##  [1] 1 2 3 4 5 6 1 2 3 4 5 6

``` r
rep(1:6, each=2)
```

    ##  [1] 1 1 2 2 3 3 4 4 5 5 6 6

**Display of the n first elements of x**

`head(x, n = 6)`

``` r
head(x, n = 6)
```

    ## [1] 1 1 2 3 5 8

**Display of the n last elements of x**

`tail(x, n = 6)`

``` r
tail(x, n = 6)
```

    ## [1]  13  21  34  55  89 144

#### Examples

``` r
c(1, 2, 3, 4, 5, 6)

mean(c(1, 2, 3, 4, 5, 6))

mean(c(1, NA, 3, 4, 5, 6), na.rm = TRUE)

mean(c(1, NA, 3, 4, 5, 6), na.rm = FALSE)

sd(c(1, 2, 3, 4, 5, 6))

sum(c(1, 2, 3, 4, 5, 6))

min(c(1, 2, 3, 4, 5, 6))

range(c(1, 2, 3, 4, 5, 6))

seq(from = 1, to = 6, by = 1)

1:6

rep(1:6, times = 2)

rep(1:6, each = 2)

rep(1:6, times = 2, each = 2)
```

In R, functions are often nested, i.e. the output of a function is
passed directly to another function as input.

For example, imagine that you define a vector from which you want to
calculate the mean value and round it to two decimal places:

``` r
# Definition of a vector:
c(34.444, 45.853, 21.912, 29.261, 31.558)
```

    ## [1] 34.444 45.853 21.912 29.261 31.558

``` r
# Calculation of the mean value:
mean(c(34.444, 45.853, 21.912, 29.261, 31.558))
```

    ## [1] 32.6056

``` r
# Round to 2 decimal places:
round(mean(c(34.444, 45.853, 21.912, 29.261, 31.558)), digits = 2)
```

    ## [1] 32.61

The functions are always executed in the order from inside to outside,
i.e., first `mean()`, and then `round()`.

## R Variables

So far, we have not saved the results of our calculations. Of course, we
can define variables in R, and assign a value to them.

Variables are defined in R like this: `my_var <- 4`. `<-` here is a
special assignment arrow, and consists of a `<` character and a `-`.
There is a key combination `ALT` + `-` in RStudio for this. So here we
assign the value 4 to the new variable `my_var`.

However, it is also possible to assign a variable with `=` instead of
`<-` However, since `=` is also the symbol for the assignment of
arguments (for functions), misunderstandings can potentially arise here.
R purists therefore prefer to use `<-`.

**Variable Names**

A variable must have a name - this consists of `letters`, `numbers` and
the characters `_` and/or `.` A variable name must start with a letter
and must not contain spaces.

There are a few conventions to follow to make R code readable and
understandable - especially when sharing it with others. We recommend
using `snake_case` for naming, i.e., we separate words within a name
with an underscore: `my_var`.

If we have defined a variable:

``` r
my_var <- 9
```

we can display their value in the console:

``` r
print(my_var)
```

    ## [1] 9

``` r
# or simply

my_var
```

    ## [1] 9

Variables exist in the Global Environment, but only as long as the
current R session remains. If you restart R, these variables are no
longer present. Therefore you should always record what you have done in
an R script/notebook.

## Data Types

So far we have worked with vectors. These represent the fundamental data
type. All further data types build on this. Vectors themselves can be
divided into the following types:

-   **numeric vectors**: These are what we have been dealing with so
    far. Numeric vectors are further divided into `integer` (whole
    numbers) and `double` (real numbers).

-   **character vectors**: The elements of this type consist of
    characters surrounded by quotation marks (either `'` or `"` ),
    e.g. `'word'` or `"word"`.

-   **logical vectors**: The elements of this type can take only 3
    values: `TRUE`, `FALSE` or `NA`.

Vectors must consist of the same elements, i.e., we cannot mix `logical`
and `character` vectors. Vectors have 3 properties:

-   Type: `typeof()`: What is it?

-   Length: `length()`: How many elements?

-   Attributes: `attributes()`: Additional information (metadata)

Vectors are created either with the `c()` (abbreviation for combine)
function, or with special functions like `seq()` or `rep()`.

### **Numeric Vectors**

Numeric vectors consist of numbers. These are either natural numbers
(`integer`) or real numbers (`double`).

``` r
numbers <- c(1, 2.5, 4.5)
typeof(numbers)
```

    ## [1] "double"

``` r
length(numbers)
```

    ## [1] 3

We can select the individual elements of a vector with `[]` (this is
called `subsetting` in technical jargon):

``` r
# First Element:
numbers[1]
```

    ## [1] 1

``` r
# Second Element:
numbers[2]
```

    ## [1] 2.5

``` r
#Third Element:
numbers[3]
```

    ## [1] 4.5

``` r
# Alternatively, the last element - here the third - can be identified by the length of the vector:
numbers[length(numbers)]
```

    ## [1] 4.5

``` r
# With - (minus) we can omit an element, e.g., all elements except the first one:
numbers[-1]
```

    ## [1] 2.5 4.5

``` r
# We can use a sequence, for example, the first two elements:
numbers[1:2]
```

    ## [1] 1.0 2.5

``` r
# We can omit the first and third elements:
numbers[-c(1, 3)]
```

    ## [1] 2.5

``` r
# Or let us output only the elements that are greater than a threshold:
numbers[numbers>2]
```

    ## [1] 2.5 4.5

#### Matrices

As mentioned before, actually everything in R is a vector. A scalar is a
vector of length 1. A matrix is in principle also a vector, but one with
a `dim` (dimension) attribute:

``` r
# x is a vector consisting of the numbers from 1 to 8
x <- 1:8

# We now assign a dim attribute to x, i.e. we make x a matrix (here with 2 rows and 4 columns)
dim(x) <- c(2, 4)
x
```

    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    3    5    7
    ## [2,]    2    4    6    8

``` r
# We can also create matrices like this:

m <- matrix(1:8, nrow = 2, ncol = 4, byrow = FALSE)
m
```

    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    3    5    7
    ## [2,]    2    4    6    8

``` r
# And we can also let us output the dimensions again:
dim(m)
```

    ## [1] 2 4

Note the argument `byrow`, which has the default value `FALSE`. If we
set the argument `byrow = TRUE`, then we get:

``` r
m2 <- matrix(1:8, nrow = 2, ncol = 4, byrow = TRUE)
m2
```

    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    2    3    4
    ## [2,]    5    6    7    8

We can transpose matrices, i.e., the rows become columns, and the
columns become rows:

``` r
m_transposed <- t(m)
m_transposed
```

    ##      [,1] [,2]
    ## [1,]    1    2
    ## [2,]    3    4
    ## [3,]    5    6
    ## [4,]    7    8

There are two more functions we should get to know: `cbind()` and
`rbind()`. These are used to join vectors or matrices.

`cbind()` combines the columns (column-bind) of vectors/matrices to one
object:

``` r
x1 <- 1:3
x1
```

    ## [1] 1 2 3

``` r
x2 <- 10:12
x2
```

    ## [1] 10 11 12

``` r
m1 <- cbind(x1, x2)
m1
```

    ##      x1 x2
    ## [1,]  1 10
    ## [2,]  2 11
    ## [3,]  3 12

This results in a matrix `m1` with the output vectors as columns.

`rbind()` combines the rows (row-bind) of vectors/matrices to one
object:

``` r
m2 <- rbind(x1, x2)
m2
```

    ##    [,1] [,2] [,3]
    ## x1    1    2    3
    ## x2   10   11   12

Matrices can also be indexed with `[]`. But we have to specify here
which row(s) and column(s) we want to get, using
`[rownumber, columnnumber]`.

The row number and column number are separated by a comma. If
`row number` or `column number` are left blank, it means: “Select all
rows/columns.”

``` r
# The first cells: Row 1, Column 1
m1[1,1]
```

    ## x1 
    ##  1

``` r
# Row 1, Column 2
m1[1,2]
```

    ## x2 
    ## 10

``` r
# Row 2 to 3, Column 1
m1[2:3, 1]
```

    ## [1] 2 3

``` r
# All Rows, Column 1
m1[, 1]
```

    ## [1] 1 2 3

``` r
# Row 2, all Coloums
m1[2, ]
```

    ## x1 x2 
    ##  2 11

#### Missing Values

Missing values are declared with `NA`.

``` r
numbers <- c(12, 13, 15, 11, NA, 10)
numbers
```

    ## [1] 12 13 15 11 NA 10

The `is.na()` function can be used to test whether something is actually
a missing value:

``` r
is.na(numbers)
```

    ## [1] FALSE FALSE FALSE FALSE  TRUE FALSE

``` r
numbers_without_na <- na.omit(numbers)
numbers_without_na
```

    ## [1] 12 13 15 11 10
    ## attr(,"na.action")
    ## [1] 5
    ## attr(,"class")
    ## [1] "omit"

The `na.omit()` function removes all incomplete cases of a data object.

``` r
na.omit(numbers)
```

    ## [1] 12 13 15 11 10
    ## attr(,"na.action")
    ## [1] 5
    ## attr(,"class")
    ## [1] "omit"

``` r
#The first line of the output consists of all cases that are not NA. However, the output also consists of additional information such as the positions of the deleted values and the class. If you want to get rid of these attributes, you can simply use the as.numeric function:

numbers_omit <- as.numeric(na.omit(numbers))
numbers_omit
```

    ## [1] 12 13 15 11 10

### **Character Vectors**

Character vectors (strings) are used to represent text.

``` r
text <- c("these are", "some strings")
text
```

    ## [1] "these are"    "some strings"

``` r
typeof(text)
```

    ## [1] "character"

``` r
# text consists of 2 elements
length(text)
```

    ## [1] 2

Like `numeric` vectors, `character` vectors can be indexed, i.e., we can
select individual elements.

There is a function with which we can merge character vectors:

``` r
paste(text[1], text[2], sep = " ")
```

    ## [1] "these are some strings"

``` r
# Special case with sep = ""
abc <- c("a", "b", "c")
paste0(1:3, abc)
```

    ## [1] "1a" "2b" "3c"

``` r
first_name <- "Luke"
last_name <- "Skywalker"
paste("My name is", first_name, last_name, sep = " ")
```

    ## [1] "My name is Luke Skywalker"

``` r
number <- 9
# Although number is an integer, it becomes a character by using paste():
paste(number, "is an integer", sep = " ")
```

    ## [1] "9 is an integer"

### **Logical Vectors**

Logical vectors can take 3 values; either `TRUE`, `FALSE` or `NA`.

``` r
log_var <- c(TRUE, FALSE, TRUE)
log_var
```

    ## [1]  TRUE FALSE  TRUE

Logical vectors are mainly used to index numeric vectors, e.g., to
select all positive elements of a vector.

``` r
# x is a vector of standard normally distributed random numbers (i.e., we draw here a random sample of size n = 24 from a normally distributed population with mean 0 and standard deviation 1). 

set.seed(5434) # makes the example reproducible

x <- rnorm(24)
x
```

    ##  [1]  1.06115528  0.87480990 -0.30032832  1.21965848  0.09860288  1.89862128
    ##  [7] -1.54699798  0.96349219 -0.64968432 -1.09672125 -0.55326456 -0.29394388
    ## [13]  0.58151046 -0.15135071  1.66997280 -0.10726874  0.51633289 -0.64741465
    ## [19]  0.10489022 -0.95484078  0.22940461 -0.54106301 -0.76310004  1.22446844

``` r
# We now need a logical vector that indicates for each element whether this element satisfies the condition (x should be positive):

x > 0
```

    ##  [1]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE
    ## [13]  TRUE FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE FALSE  TRUE

``` r
# Now we index the vector x with it:
x[x > 0]
```

    ##  [1] 1.06115528 0.87480990 1.21965848 0.09860288 1.89862128 0.96349219
    ##  [7] 0.58151046 1.66997280 0.51633289 0.10489022 0.22940461 1.22446844

``` r
# We can also save the index
index <- x > 0

# and thus index x:
x[index]
```

    ##  [1] 1.06115528 0.87480990 1.21965848 0.09860288 1.89862128 0.96349219
    ##  [7] 0.58151046 1.66997280 0.51633289 0.10489022 0.22940461 1.22446844

``` r
#We can also search for all elements of x that are one standard deviation above the mean:

x_mean <- mean(x)
x_sd <- sd(x)
x_mean
```

    ## [1] 0.1182059

``` r
x_sd
```

    ## [1] 0.9156615

``` r
x > (x_mean + x_sd)
```

    ##  [1]  TRUE FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [13] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE

``` r
x[x > (x_mean + x_sd)]
```

    ## [1] 1.061155 1.219658 1.898621 1.669973 1.224468

``` r
# or in just one command:

x[x > (mean(x) + sd(x))]
```

    ## [1] 1.061155 1.219658 1.898621 1.669973 1.224468

``` r
# this indicates which elements of x satisfy the condition
which(x > (mean(x) + sd(x)))
```

    ## [1]  1  4  6 15 24

``` r
#In this example, the elements 1, 4, 6, 15, 24 are one standard deviation or more above the mean. We can also use this to index the vector; instead of using a logical vector, we just explicitly say which elements we want.

x[which(x > (mean(x) + sd(x)))]
```

    ## [1] 1.061155 1.219658 1.898621 1.669973 1.224468

``` r
# x[which(x > 0)] and x[x > 0] are equivalent

x[which(x > (mean(x) + sd(x)))] == x[x > (mean(x) + sd(x))]
```

    ## [1] TRUE TRUE TRUE TRUE TRUE

### Factors

`numeric`, `logical` and `character` vectors are also called
`atomic vectors` in R because they represent the fundamental data types.
The `factor` object type is needed to represent categorical data or
grouping variables. A `factor` is an integer vector that is provided
with additional information (metadata). These `attributes` are the
object class `factor` and the `levels`.

``` r
# Gender is a character vector
gender <- c("male", "female", "male", "male", "female")
gender
```

    ## [1] "male"   "female" "male"   "male"   "female"

``` r
typeof(gender)
```

    ## [1] "character"

``` r
attributes(gender)
```

    ## NULL

Now we can define a factor with the function `factor()`:

``` r
gender <- factor(gender, levels = c("female", "male"))
gender
```

    ## [1] male   female male   male   female
    ## Levels: female male

``` r
# gender now has the data type integer
typeof(gender)
```

    ## [1] "integer"

``` r
# but the `class` factor
class(gender)
```

    ## [1] "factor"

``` r
# and the attributes levels and class
attributes(gender)
```

    ## $levels
    ## [1] "female" "male"  
    ## 
    ## $class
    ## [1] "factor"

### Lists

Another data type is `list`. While vectors consist of elements of the
same type, lists can be composed of heterogeneous elements.

Lists are defined with the `list()` function:

``` r
x <- list(1:3, "a", c(TRUE, FALSE, TRUE), c(2.3, 5.9))
x
```

    ## [[1]]
    ## [1] 1 2 3
    ## 
    ## [[2]]
    ## [1] "a"
    ## 
    ## [[3]]
    ## [1]  TRUE FALSE  TRUE
    ## 
    ## [[4]]
    ## [1] 2.3 5.9

Here we have defined a list x, which contains as elements a numeric
vector, a character, a logical vector and another numeric vector.

Lists can be indexed like vectors:

``` r
x[1]
```

    ## [[1]]
    ## [1] 1 2 3

``` r
x[2]
```

    ## [[1]]
    ## [1] "a"

``` r
x[3]
```

    ## [[1]]
    ## [1]  TRUE FALSE  TRUE

``` r
x[4]
```

    ## [[1]]
    ## [1] 2.3 5.9

## Data Frames

Data Frames can be considered as the most important objects in R. Data
sets are represented in R by data frames. A data frame consists of rows
and columns and corresponds to a data set in SPSS.

Technically, a Data Frame is a list whose elements are equal-length
vectors. The vectors themselves can be `numeric`, `logical` or
`character` vectors, or of course factors. A Data Frame is a
2-dimensional structure, and can be indexed like a vector on the one
hand (more precisely: like a matrix), and like a list on the other hand.

Traditionally, Data Frames are defined in R with the function
`data.frame()`. In RStudio or the `tidyverse` package, data frames are
recently also called `tibbles` or `tbl`. tibbles `are` defined with the
`tibble()` function, and are just a modern variant of a data frame. They
make working with data sets easier.

A Data Frame is defined like this:

``` r
library(dplyr)
```

    ## 
    ## Attache Paket: 'dplyr'

    ## Die folgenden Objekte sind maskiert von 'package:stats':
    ## 
    ##     filter, lag

    ## Die folgenden Objekte sind maskiert von 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
df <- tibble(gender = factor(c("male", "female", "male", "male", "female")), age = c(22, 45, 33, 27, 30))

df
```

    ## # A tibble: 5 x 2
    ##   gender   age
    ##   <fct>  <dbl>
    ## 1 male      22
    ## 2 female    45
    ## 3 male      33
    ## 4 male      27
    ## 5 female    30