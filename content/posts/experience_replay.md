---
title: "Experience Replay and Data Efficiency"
date: 2022-07-14
# weight: 1
# aliases: ["/first"]
tags: ["Reinforcement Learning: an Introduction"]
author: "Orange"
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
To make better use of data, we can use experience replay to increase data efficiency. 

### Experience replay
We can put ${s,a,s',r}$ pairs in the buffer and update Q using mini batch methods. To decrease noise in the replay, we average over several samples. (That's why minibatch)

![](/img/rl/experience_replay.png)

### Infer-Collect framework

![](/img/rl/collect_infer.png)

![](/img/rl/NFQ.png)