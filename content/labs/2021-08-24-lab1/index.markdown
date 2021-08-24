---
title: 'Introduce Yourself'
author: "Alison Hill"
output:
  html_document:
    theme: flatly
    toc: TRUE
    toc_float: TRUE
    toc_depth: 2
    number_sections: TRUE
---





> Read all the way through step 6, and note that there is a file that needs to be turned in to Sakai before Wednesday at noon!

# Overview

This guide will lead you through the steps to install and use [R, a free and open-source software environment for statistical computing and graphics.](https://www.r-project.org) 


What is R?

* **R** is the name of the programming language itself, based off of S from Bell Labs, which users access through a command-line interpreter (`>`)

What is RStudio?

* **RStudio** is a powerful and convenient user interface that allows you to access the R programming language along with a lot of other bells and whistles that enhance functionality (and sanity). 

Our end goal is to get you looking at a screen like this:

![](./images/00_final-screenshot.png)

# Install R

Install R from [CRAN, the Comprehensive R Archive Network](https://cran.rstudio.com). Please choose a **precompiled binary distribution** for your operating system.

* If you need more help, check out one of the following videos (courtesy of Roger Peng at Johns Hopkins Biostatistics):
    - [Installing R on a mac](https://www.youtube.com/watch?v=Icawuhf0Yqo&feature=youtu.be)
    - [Installing R on windows](https://www.youtube.com/watch?v=mfGFv-iB724&feature=youtu.be)
* If you need even more help, read this [step-by-step guide](https://beckmw.files.wordpress.com/2014/09/r_install_guide.pdf), including screenshots.

## Check in

Launch R. You should see one console with a command line interpreter (`>`). Close R.

# Install RStudio 

Install the free, open-source edition of RStudio: http://www.rstudio.com/products/rstudio/download/

RStudio provides a powerful user interface for R, called an *integrated development environment*. RStudio includes:

* a console (the standard command line interface: `>`), 
* a syntax-highlighting editor that supports direct code execution, and 
* tools for plotting, history, debugging and workspace management.


## Check in

Launch RStudio. You should get a window similar to the screenshot you see [here](https://www.rstudio.com/wp-content/uploads/2014/04/rstudio-workbench.png), but yours will be empty. Look at the bottom left pane: this is the same console window you saw when you opened R in step 1.15. 

* Place your cursor where you see `>` and type `x <- 2 + 2`, hit enter or return, then type `x`, and hit enter/return again. 
* If `[1] 4` prints to the screen, you have successfully installed R and RStudio, and you can move onto installing packages.

# Install packages

The version of R that you just downloaded is considered base R, which provides you with good but basic statistical computing and graphics powers. For analytical and graphical super-powers, you'll need to install add-on packages, which are user-written, to extend/expand your R capabilities. Packages can live in one of two places:

* They may be carefully curated by CRAN (which involves a thorough submission and review process), and thus are easy install using `install.packages("name_of_package", dependencies = TRUE)`. 
* Alternatively, they may be available via GitHub. To download these packages, you first need to install the `devtools` package.


```r
install.packages("devtools")
library(devtools)
install_github("name_of_package")
```

Place your cursor in the console again (where you last typed `x` and `[4]` printed on the screen). You can use the first method to install the following packages directly from CRAN, all of which we will use:

  * [`dplyr`,](http://dplyr.tidyverse.org)
  * [`ggplot2`,](http://ggplot2.tidyverse.org)
  * [`babynames`](https://github.com/hadley/babynames)

  
You can download all of these at once, too:

```r
install.packages(c("dplyr", "ggplot2", "babynames"), 
                 dependencies = TRUE)
```

<p class="text-info"> __Heads up:__ We should formally introduce the combine command, [`c()`](http://stat.ethz.ch/R-manual/R-patched/library/base/html/c.html), used above. You will use this often- any time you want to combine things into a vector.</p>


```r
c("hello", "my", "name", "is", "alison")
```

```
[1] "hello"  "my"     "name"   "is"     "alison"
```

```r
c(1:3, 20, 50)
```

```
[1]  1  2  3 20 50
```

Mind your use of quotes carefully with packages.

* To *install* a package, you put the name of the package in quotes as in `install.packages("name_of_package")`. 
* To *use* an already installed package, you must load it first, as in `library(name_of_package)`, leaving the name of the package bare. You only need to do this once per RStudio session.
* If you want *help*, no quotes are needed: `help(name_of_package)` or `?name_of_package`.
* If you want the *citation* for a package (and you should give credit where credit is due), ask R as in `citation("name_of_package")`.


```r
install.packages("dplyr", dependencies = TRUE)
library(dplyr)
help("dplyr")
```


```r
citation("ggplot2")
```

```

To cite ggplot2 in publications, please use:

  H. Wickham. ggplot2: Elegant Graphics for Data Analysis.
  Springer-Verlag New York, 2016.

A BibTeX entry for LaTeX users is

  @Book{,
    author = {Hadley Wickham},
    title = {ggplot2: Elegant Graphics for Data Analysis},
    publisher = {Springer-Verlag New York},
    year = {2016},
    isbn = {978-3-319-24277-4},
    url = {https://ggplot2.tidyverse.org},
  }
```


<p class="text-info"> __Heads up:__ R is **case-sensitive**, so `?dplyr` works but `?Dplyr` will not. Likewise, a variable called `A` is different from `a`.</p>

# Make a name plot

Open a new R script in RStudio by going to `File --> New File --> R Script`. For this first foray into R, I'll give you the code, so sit back and relax and feel free to copy and paste my code with some small tweaks.

First load the packages:


```r
library(babynames) # contains the actual data
library(dplyr) # for manipulating data
library(ggplot2) # for plotting data
```


Next, we'll follow [best practices for inspecting a freshly read dataset](https://cran.r-project.org/doc/contrib/de_Jonge+van_der_Loo-Introduction_to_data_cleaning_with_R.pdf). Also, see ["What I do when I get a new data set as told through tweets"](http://simplystatistics.org/2014/06/13/what-i-do-when-i-get-a-new-data-set-as-told-through-tweets/) for more ideas about exploring a new dataset. Here are some critical commands to obtain a high-level overview (HLO) of your freshly read dataset in R. We'll call it saying hello to your dataset:


```r
glimpse(babynames) # dplyr
```

```
Rows: 1,924,665
Columns: 5
$ year <dbl> 1880, 1880, 1880, 1880, 1880, 1880, 1880, 1880, 1880, 1880, 1880,…
$ sex  <chr> "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", …
$ name <chr> "Mary", "Anna", "Emma", "Elizabeth", "Minnie", "Margaret", "Ida",…
$ n    <int> 7065, 2604, 2003, 1939, 1746, 1578, 1472, 1414, 1320, 1288, 1258,…
$ prop <dbl> 0.07238359, 0.02667896, 0.02052149, 0.01986579, 0.01788843, 0.016…
```

```r
head(babynames) # base R
```

```
# A tibble: 6 × 5
   year sex   name          n   prop
  <dbl> <chr> <chr>     <int>  <dbl>
1  1880 F     Mary       7065 0.0724
2  1880 F     Anna       2604 0.0267
3  1880 F     Emma       2003 0.0205
4  1880 F     Elizabeth  1939 0.0199
5  1880 F     Minnie     1746 0.0179
6  1880 F     Margaret   1578 0.0162
```

```r
tail(babynames) # same
```

```
# A tibble: 6 × 5
   year sex   name       n       prop
  <dbl> <chr> <chr>  <int>      <dbl>
1  2017 M     Zyhier     5 0.00000255
2  2017 M     Zykai      5 0.00000255
3  2017 M     Zykeem     5 0.00000255
4  2017 M     Zylin      5 0.00000255
5  2017 M     Zylis      5 0.00000255
6  2017 M     Zyrie      5 0.00000255
```

```r
names(babynames) # same
```

```
[1] "year" "sex"  "name" "n"    "prop"
```


If you have done the above and produced sane-looking output, you are ready for the next bit. Use the code below to create a new data frame called `alison`.


```r
alison <- babynames %>%
  filter(name == "Alison" | name == "Allison") %>% 
  filter(sex == "F") 
```

* The first bit makes a new dataset called `alison` that is a copy of the `babynames` dataset- the `%>%` tells you we are doing some other stuff to it later.

* The second bit `filters` our `babynames` to only keep rows where the `name` is either Alison or Allison (read `|` as _"or"_.) 

* The third bit applies another `filter` to keep only those where sex is female.

Let's check out the data.


```r
alison
```

```
# A tibble: 218 × 5
    year sex   name        n      prop
   <dbl> <chr> <chr>   <int>     <dbl>
 1  1905 F     Alison      7 0.0000226
 2  1907 F     Alison      5 0.0000148
 3  1908 F     Allison     6 0.0000169
 4  1910 F     Alison      5 0.0000119
 5  1910 F     Allison     5 0.0000119
 6  1911 F     Allison     9 0.0000204
 7  1912 F     Allison    12 0.0000204
 8  1912 F     Alison      9 0.0000153
 9  1913 F     Alison     12 0.0000183
10  1913 F     Allison     7 0.0000107
# … with 208 more rows
```

```r
glimpse(alison)
```

```
Rows: 218
Columns: 5
$ year <dbl> 1905, 1907, 1908, 1910, 1910, 1911, 1912, 1912, 1913, 1913, 1914,…
$ sex  <chr> "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", …
$ name <chr> "Alison", "Alison", "Allison", "Alison", "Allison", "Allison", "A…
$ n    <int> 7, 5, 6, 5, 5, 9, 12, 9, 12, 7, 22, 11, 16, 13, 24, 15, 20, 15, 3…
$ prop <dbl> 2.259e-05, 1.482e-05, 1.692e-05, 1.192e-05, 1.192e-05, 2.037e-05,…
```

Again, if you have sane-looking output here, move along to plotting the data!


```r
plot <- ggplot(alison, aes(x = year, 
                           y = prop,  
                           group = name, 
                           color = name)) + 
  geom_line()  
```

Now if you did this right, you will not see your plot! Because we saved the `ggplot` with a name (`plot`), R just saved the object for you. But check out the top right pane in RStudio again: under `Values` you should see `plot`, so it is there, you just have to ask for it. Here's how:


```r
plot 
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

# Make a new name plot

Edit my code above to create a new dataset. Pick 2 names to compare how popular they each are (these could be different spellings of your own name, like I did, but you can choose any 2 names that are present in the dataset). Make the new plot, changing the name of the first argument `alison` in `ggplot()` to the name of your new dataset.


## Save and share 

Save your work so you can share your favorite plot with us. You will not like the looks of your plot if you mouse over to `Export` and save it. Instead, use `ggplot2`'s command for saving a plot with sensible defaults:


```r
help(ggsave)
```


```r
ggsave("alison_hill.pdf", plot) # please make the filename unique!
```

Upload this exported plot to Sakai before Wednesday at noon.

# Other cool `babynames` projects


- Julia Silge *'My Baby Boomer Name Might Have Been "Debbie"'*: https://juliasilge.com/blog/my-baby-boomer-name/
    - Use Julia's Shiny app: https://juliasilge.shinyapps.io/PredictNamesApp/
![](https://juliasilge.com/figs/2016-02-29-My-Baby-Boomer-Name/unnamed-chunk-8-1.png)

- Hilary Parker: Hilary: The Most Poisoned Baby Name in US History: https://hilaryparker.com/2013/01/30/hilary-the-most-poisoned-baby-name-in-us-history/

![](https://hilaryparker.files.wordpress.com/2013/01/more_names_trimmed2.png)



# Resources

- https://alison.rbind.io/html/jamboree_heart_ggplot.html

- http://moderndive.com/2-getting-started.html

- http://r4ds.had.co.nz

- https://www.rstudio.com/resources/cheatsheets/

- https://rweekly.org
