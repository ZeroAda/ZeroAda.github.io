---
title: "RL method overview"
date: 2022-07-11
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

There are three kinds of RL in general. The first two are model-free methods.

1. Value: Parameterize value function; Estimate value function $q$ to generate the best policy. **Q learning, SARSA**


2. Policy: Parameterize policy gradient; Objective is to maximize the average return so that find the best policy directly; always combine with value-based method. **Actor Critic**


3. Model: Parameterize the model; Improve model accuracy; always combine with value-based method. **Dyna-Q & Dyna-Q+**

We can also categorize RL into off-policy and on-policy methods. "Off policy" refers to behavior policy and target policy is different while "On policy" refers to it is the same. 

Now, we first introduce Monte Carlo Method to predict and control.

### Monte Carlo idea
"Monte carlo methods are ways of solving the reinforcement elarning problem based on averaging sample returns". It's a way to learn episode-by-episode.

### On-Policy Monte Carlo Prediction
Without any state transition info, we want to estimate value function via averaging return sampled by following the policy.

![](/img/rl/monte-carlo-prediction.png)

why we need to loop backward?
* to compute the return more efficiently.

can we use incremental updates?
* yes

### On-Policy Monte Carlo Control
Following the general policy update, we estimate Q value using MC and update policy accordingly.

However, we need exploring start to encourage exploration so that each state-action pair is selected at least once. 

![](/img/rl/monte-carlo-exploring.png)

OR! We will use "epsilon-soft" policy to encourage that!

![](/img/rl/monte-carlo-control.png)

## Off Policy

Why do we care about off policy learning?
Because Off policy learning are more powerful and general!

**Assumption of Convergence**
Assume b is behavior assumption, $\pi$ is target assumption.
if $\pi(a|s) >0$ implies $b(a|s)>0$, we can learn value function of b.


