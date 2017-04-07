---
## 1."Low-shot visual Recognition by Shrinking and Hallucinating Features"
---

### 论文主要贡献：
---
- In the low-shot learning phase, the learner is exposed to a set of novel classes with only a few examples per class and must learn a classifier over the joint label space of base and novel classes.
- 在low-shot learning阶段，学习者在每类中可以学到的样本数量非常少,
- Firs we show that the feature representation learnt in the first phase has a large impact on low-shot generalization ability.
- Specifically, we formulater a loss function that penalizes the difference between classifiers learnt on large and small datasets 
<center>![algorithm](../images/fcn_application/1.JPG)</center>
<center>本文建立了三个网络进行伤痕识别</center>

<center>![algorithm](../images/fcn_application/2.JPG)</center>
<center>诊断网络结构</center>

### 论文思考
- 论文使用了一种新的思路进行伤痕诊断

