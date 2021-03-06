---
layout: post
title: Causal Reasoning
categories: [Critical Thinking]
tags: [Corner Stone]
fullview: false
Description: Causal Reasoning for research. 我们如何从data中提取因果关系?
---

Cause and effect is what scientists really are doing. But how can we infer the data to cause and effect chain? There are infinite inferences.

本文是做ENG2001 Research期间处理数据时对因果关系所作的阅读和思考：我们如何从data中提取因果关系？
重要的不是data，而是如何看待data，或者如何从data中提取信息。这适用于machine learning, data analysis，也适用于基础科学研究。


#### 因果推理

> “研究”是一份奇特的工作。无论撰写多少篇论文，在研讨会上做多 少场演讲，我们也不会变得更加富有。不过，研究中诞生的观点可以作 为公共知识财富，为建设更美好的世界做出贡献。
>
> 中室牧子 津川友介

> “ 浅薄的人相信运气，强大的人相信因果。” 爱默生

#### 因果推理无处不在

因果推理 - 经济学

因果性与相关性 - 心理学研究

​	伦理性问题 

教育和医疗领域



#### 因果关系

因果关系成立条件A->B

1. A与B有相关性：同增同减，具有统计学的显著性
2. A发生在B之前
3. 排除其他影响B 的因素（混杂因素）

#### Methodology方法：如何提取、构建、验证因果关系？

* 确定AB 具体

* 检验3个条件

  * 相关性AB是否是因为：

    * 巧合

    * 混杂因素

    * 逆向因果关系

      * 在社团内担任leader的人有更高的social identity to 这个group，是否因为有了更高的social-identity就会担任leader？

        两个变量，真的可用逆向 吗？还是说另一个变量本身就是indicator

* 构建反事实

  * 事实：发生的事情
  * 反事实：未发生的事情：如果那么

  > “如果克莉奥帕特拉的鼻子再塌一点，世界史就会改写了。”

  * 如果我们可用构建反事实（时光机），观测结果，对比事实，就可以得出AB是否是因果关系

    > 最早创建因果推理体系的哈佛大学统计学家唐纳德·鲁宾把这个问 题称为“因果推理中的根本问题”。然而，要证明因果关系，反事实是必 经之路。

  * 只要观测到反事实就可以因果推理

    * 可是需要有可比较的值替换反事实

* 调整到可比较的值

  > 用最贴切的值替换反事实的结果的一种有效方法是，通过调整形成 “可比较”的组。

  可比较的值形成-->证据（evidence）科学证据：与因果推理直接相关的证据

  ​	等级

  ​	![](/img/post/evidence_hierarchy.png)1. 随机对照试验

两组 - 事实 + 反事实

​			控制变量：随机分组为接受干预的组（干预组）和不接受干预的组（对照组）

​			避免selection bias，即在排除任何人选择的条件，可用保证所有因变量之外的变量被控制在随机分布的水平上，对不同组个体的作用相同



2. 元分析：整合多项研究

3. 自然试验

   > 基于“胎儿起源说”撰写了畅销书《胎内人生》的作家安妮·墨菲·保 罗（Annie Murphy Paul）在TED演讲中曾说过这样一番话：“研究胎儿 起源不是为了追究准妈妈在怀孕过程经历的不幸遭遇或行为，而是为了 帮助下一代的孩子们发现更美好的人生。”

   利用研究对象人群由于法律制度变更、自然灾害等“外生冲击”的影 响而自然分成受影响组（干预组）和不受影响组（对照组）的现象，来 验证因果关系。

   在涉及伦理问题/无法随机分组的情况下

4. 工具变量法

   ![image](img/post/tool_variable.png)

   procedure：找到工具变量，用工具变量做干预因素，分成干预组和对照组做实验

   工具变量：影响原因但不影响结果，同时不存在同时影响原因和结果的第四变量

   栗子：看电视 - > 学习成绩

   工具变量：电视执照

   排除了同时影响是否拥有电视和影响学习成绩的因素，比如家庭经济状况等等

5. 实验前后测 - 改进：双重差分法

   试验前后测：在一段时间里，a点前不干预，a点后干预，观察干预和不干预的结果，得出结论

   问题：1. 趋势影响

      			2. 平均回归：统计学意义
      	        			1. 恐吓从善的平均回归

   改进：双重差分法

   ![image-20201208182902844](/img/post/双重差分.png)

   条件：干预期间没有别的因素影响结果

   同时干预前干预组和对照组的趋势相同

6. 断点回归设计法

   procedure：连续变量里选择断点值，断点值附近没有其他影响结果的事件

   断点值选择：决定成为事实和反事实的点，但不影响结果

   栗子：探究广告增益，49人店铺不投广告，50人投广告

7. 组合相似个体的匹配法

8. 回归分析-基于数据的研究

   一元回归分析：在无混杂因素的情况下，研究AB 的因果关系

   多元回归分析：在有混杂因素的情况下，研究多个变量的数学关系

   

![image-20201208180859335](/img/post/image-20201208180859335.png)



![image-20201208180918814](/img/post/image-20201208180918814.png)



#### Evaluate：评估因果关系

##### 有效性

* 内部效度：AB因果关系的确定程度

  * 对研究对象群体再次施加相同干预后，会出现相同结果的程度

* 外部效度：

  * 指对研究对象之外的群体施加相同干预后，会出现相同结果的程度

  

##### 局限性

协变量和混杂因素

协变量指原因与结果以外的所有其他变 量。比如在现有数据中，除了原因和结果的变量，其他所有变量都是协变量。而混杂因素 是这些协变量中“同时影响原因与结果的变量”。也就是说，协变量中包括混杂因素，也包 括非混杂因素。




#### Reference

* 鲁宾和因本斯合著的《统 计学、社会科学及生物医学领域中的因果推理导论》（Causal Inferen ce for Statistics and Biomedical Sciences: An Introduction ）
* 原因与结果的经济学 [日]中室牧子，[日]津川友介 著 程雨枫 译



