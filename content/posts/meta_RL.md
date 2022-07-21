---
title: "Meta Reinforcment Learning"
date: 2022-07-14
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
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
math: true
type: post
---



## Meta learning system
This part is based on Lilian Weng's post [meta rl](https://lilianweng.github.io/posts/2019-06-23-meta-rl/).

Meta RL aims to adopt fast when new situations come. 

To make it fast for RL, we introduce inductive bias in the system.

> In meta-RL, we impose certain types of inductive biases from the task distribution and store them in memory. Which inductive bias to adopt at test time depends on the algorithm.

In the training setting, there will be a distribution of environments. Agents need to decide which inductive bias to use when encounter new environment.

![](/img/rl/meta_Rl.png)
*The outer loop trains the parameter weights u, which determine the inner-loop learner (’Agent’, instantiated by a recurrent neural network) that interacts with an environment for the duration of the episode. For every cycle of the outer loop, a new environment is sampled from a distribution of environments, which share some common structure.*


The inductive bias could be hyper-parameters, learned models, loss functions etc. We can also borrow ideas from "Episodic Control" ([Botvinick, et al. 2019](https://www.cell.com/action/showPdf?pii=S1364-6613%2819%2930061-0)) 

> When a new situation is encountered and a decision must be made concerning what action to take, the procedure is to compare an internal representation of the current situation with stored representations of past situations. The action chosen is then the one associated with the highest value, based on the outcomes of the past situations that are most similar to the present.


Meta RL system is composed of **Model with Memory**, **Meta-learning algorithm**, and **A distribution of MDPs**. 

### Potential Algorithm we can look into
**Episodic Control**:
MFEC (Model-Free Episodic Control; [Blundell et al., 2016](https://arxiv.org/abs/1606.04460))

NEC (Neural Episodic Control; [Pritzel et al., 2016](https://arxiv.org/abs/1703.01988))

Episodic LSTM ([Ritter et al., 2018](https://arxiv.org/abs/1805.09692)) 


**Automatic generating reward and train skills.**

[Gupta et al. (2018)](https://arxiv.org/pdf/1806.04640.pdf)
[Eysenbach et al., 2018](https://arxiv.org/pdf/1802.06070.pdf)

idea: pick z as skill, generate policy conditioned on z, and generate discriminator q of z conditioned on s. The objective is to minimize mutual info between states and skills, maximize mutual info between action and skills and policy entropy.

**Unsupervised RL**
[goal generate](https://arxiv.org/pdf/1705.06366.pdf)

**Pretraining RL**
1. Entropy based
        [maximum entropy to encourage explore](https://arxiv.org/pdf/2112.01195.pdf)
2. Skill based [skill](https://openreview.net/pdf?id=jeLW-Fh9bV)
          ![](/img/rl/skill_base.png)
3. Knowledge based
   not many resources
        [knowledge based](https://openreview.net/pdf/18e031ea7b15738b6c8ce6165873fb8f746e363e.pdf)

### Ideas about our projects
1. H1 could be tested by constructing such a action space and see what behaviors will emerge.
   1. A={task action, play action}
   
2. Since we plan to adopt a meta-learning algorithms, it is no need to test H2, H3, H4.
3. Turn external reward to **intrinsic reward?** 
   1. To test proximate cause: turn fun to intrinsic reward: when I push rock into the ground, I feel intrinsic reward - fun. 
   2. To test ultimate cause, Meta learning framework will allow good performance in dynamic environment.