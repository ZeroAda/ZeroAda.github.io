---
title: "Dynamic Programming for MDP"
date: 2021-08-14
# weight: 1
# aliases: ["/first"]
tags: ["Reinforcement Learning: an Introduction"]
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
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
math: true
type: post
---

Before we delve into solving MDP by dynamic programming, let's review concepts in MDP!
We have defined the **value function** for each states if we follow the policy $\pi$ as the expected return:
$$ v_{\pi}(s) = E_{\pi}[G_t|S_t = s] = E_{\pi}[\sum_{k=0}^{\infty} \sigma^k R_{t+k+1}|S_t = s]$$

The **state-value function** for policy $\pi$ is:
$$q_{\pi}(s,a)=E_{\pi}[G_t|S_t = s,A_t=a]=E_{\pi}[\sum_{k=0}^{\infty} \sigma^k R_{t+k+1}|S_t = s,A_t=a]$$

There are recursive properties for value function and state-action functions. We will encounter them many times afterwards.
The Bellman equation for $v_{\pi}$ is:
$$
v_{\pi}(s) = \sum_a \pi(a|s) \sum_{r,s'} p(r,s'|s,a)(r+\sigma v_{\pi}(s'))
$$
for all s $\in$ S

The Bellman equation for $q_{\pi}$ is:

$$
q_{\pi}(s,a) = \sum_{r,s'} p(r,s'|s,a)(r+\sigma \sum_{a'} \pi(a'|s') q_{\pi}(s',a'))
$$
for all s,a $\in$ S,A

To get more reward as possible, we want to find the optimal policy $\pi*$ (maybe many) and they share one optimal value function and state-action function. They also have recursive properties. They are called Bellman optimality equations.
$$q*(s,a) = max_{\pi}q_{\pi}(s,a)=\pi(a|s) \sum_{r,s'} p(r,s'|s,a)(r+\sigma max_{a'} q*(s',a'))$$

$$v*(s ) = max_{\pi}v_{\pi}(s)=max_{a} \sum_{r,s'} p(r,s'|s,a)(r+\sigma v*(s'))$$

Our goal is to find solutions so we can use greedy action to behave the best!
It is a equation system with n state(unknowns) and n equations. We can only do this under the condition that 
1. dynamics of the environment is known 
2. computational resources are sufficient to complete the computation 
3. the states have the Markov property

Now we are ready to see what we can do with DP! In general, it's a method to iteratively or recurisvely achieve the result by dividing and reusing the problem.