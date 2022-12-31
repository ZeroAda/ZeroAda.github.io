---
title: "Common Measure in Face Verification"
date: 2022-11-03
# weight: 1
# aliases: ["/first"]
tags: ["Computer Vision"]
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

In face verification task, we have several metrics to measure model performances.

## Verification Rate (FR) under False Acceptance Rate
First, we need to understand the false acceptance rate. There is a table showing reality and prediction.

 ![](/img/face_verification_metrics/false-true.png)

 false acceptance rate is defined as "the percentage of identification instances, in which unauthorised cases are incorrectly accepted".

$$
FAR = \frac{FA}{FT} = \frac{False_Negative}{False_Negative+True_Negative}
$$

 Verification rate is the accuracy of a verification model.

$$
VR = \frac{TP + TN}{all}
$$

## AUC-ROC curve
AUC means area under the curve. ROC is the Receiver operating characteristic.
 ![](/img/face_verification_metrics/ROC.png)

x axis is False Positive Rate: the percentage of error in the positive reality
$$
FPR = \frac{False_Positive}{False_Positive+True_Negative}
$$

y axis is True Positive Rate: the accuracy in the positive reality
$$
TPR = \frac{True_Positive}{True_Positive+False_Negative}
$$

The closer the AUC is to 1, the better the model is. 

To pick a good threshold of the model, it should pick the low FPR and high TPR point.
