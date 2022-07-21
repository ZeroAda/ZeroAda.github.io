---
title: "Summer camp: R Day3"
date: 2022-07-20
# weight: 1
# aliases: ["/first"]
tags: ["data analysis"]
author: "Orange"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: true
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
math: true
type: post
---


## Data analysis
### Warm up! 
We can use "describe" in psych package to see the number of participant, mean, std of a variable.

```r
library(psych)
describe(penguins$body_mass_g)
```

result
```
vars   n    mean     sd median trimmed    mad  min  max range
X1    1 342 4201.75 801.95   4050 4154.01 889.56 2700 6300  3600
   skew kurtosis    se
X1 0.47    -0.74 43.36
```

### What is TIDY DATA
* Every column is a variable
* Every row is an observation
* Every cell has one value
It will benefit a lot if we deal with tidy data, for example, easy for data sharing, reproducible, easy to automate...

### Data cleaning
Remove data hierachically!
1. remove variables you do not need
2. remove/filter observations you do not need
3. remove missing values
4. add new variables


### Tidyverse: A tidy universe
use %>% **pipe**

shortcut: ctrl+shift+M

1. remove variables you do not need (and remain what you need)

```r
# We remove flipper_length_mm and body_mass_g and remain the others
penguins_select <- penguins %>% 
  select(penguin, species, island, bill_length_mm, bill_depth_mm, sex, year)


## Or, if you just want to remove columns, you can just do this:
penguins_select2 <- penguins %>% 
  select(-flipper_length_mm,-body_mass_g)


```



2. filter the rows (observations) you want

```r
penguins_filter <- penguins %>% 
  filter(year == 2008 & year==2007 | species=="Adelie")


```
[logical operators](https://www.tutorialspoint.com/r/r_operators.htm)

3. drop all rows with missing value

```r
penguins_clean <- penguins %>% 
  drop_na()
```

4. Build new variables to the dataframe
mutate can do changes to the cells
```r
penguins_clean <- penguins %>% 
  mutate(
    bill_sum = bill_length_mm+bill_depth_mm,
    species = factor(species),
    sex_recoded = case_when(sex == "female" ~ "f",
                            sex == "male" ~ "m"),
    sex_recoded = factor(sex_recoded)
  )

```
* transform variables to factors
* create new variables 
  * numerical operation
  * if else condition

**case_when**
    case_when(
        variable == X ~ value,
        variable == y ~ value,
    )
