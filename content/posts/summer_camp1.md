---
title: "Summer camp: R Day1"
date: 2022-07-06
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


### Data type in the datasheet

words: "California"
categorical data: a / b / c
logical: TRUE, FALSE
number: 10
missing data: NA

### Hot key

run one chunk in the scripts:

```R
ctrl + Enter
```
run all chunks in the scripts:

```R
ctrl + Enter + Shift
```


### Data type in R

vector
```R
vector <- c("Ada","Emily","Jack")
```
if you combine different data types into one vector, you will get vector consist of string

```R
vector <- c(TRUE,"Ada",10)
```

factor
```R
groups <- factor(c("Treatment1","Treatment2","Control","Treatment2"))
# factor group value into groups, set levels in alphabetical order


```
