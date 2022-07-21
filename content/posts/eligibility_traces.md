---
title: "Eligibility Trace, Andy Barto"
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


### Harry Klopf's Hedonistic Hypothesis
Neurons will maximize the local analog of pleasure and minimize the local analog of pain, i.e. it is a RL agent.


### specific hypothesis
When a neuron fires an action potential, all the contributing synapses become eligible to undergo changes in their efficacies, or weights.

If the action potential is followed within an appropriate time period by an increase in reward, an efficacies of all eligible synapses increase (or decrease in the case of punishment).

Klopf proposed an eligibility trace graph:

![](/img/rl/eligible_trace.png)

In RL, eligibility trace is an exponential decrease graph:

![](/img/rl/eligible_trace2.png)

Contingent eligibility: depends on pre- and post- synaptic activity. Lead to three factor learning.
Non-contingent eligibility: depends only on pre-synaptic activity. Lead to two factor learning.

![](/img/rl/eligible_trace3.png)

In actor-critic algorithm, we can regard critic as non-contingent eligibility, and actor as contingent eligibility.

![](/img/rl/eligible_trace_4.png)