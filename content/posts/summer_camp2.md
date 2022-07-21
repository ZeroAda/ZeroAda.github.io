---
title: "Summer camp: R Day2"
date: 2022-07-13
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


### Create dataframe
#### Create variables
```R
## i. name
names <- c("Ada","Robert","Mia")

## ii. age
ages <- c(20,21,22)


## iii. Factor, so that you can add levels that not exist in the data
year <- c("Freshman","Sophomore","Junior")
year <- factor(year, levels=c("Freshman","Sophomore",
                              "Junior","Senior"))
```

#### Create dataframe

```R
students <- data.frame(names,ages,year)

```

### Query a dataframe

```R
students$names
```

### Set working dictory

get working dicrectory
```R
getwd()
```
set working directory
```R
setwd()
```
or go to "session" and set working directory

or build R file in the directory you want to work in