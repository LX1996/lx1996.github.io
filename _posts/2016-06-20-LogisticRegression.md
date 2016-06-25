---
title: Logistic Regression笔记
updated: 2016-06-20 16:14
---
Content:

2 Logistic Regression. 

　　2.1 Classification. 

　　2.2 Hypothesis representation. 

　　　　2.2.1 Interpreting hypothesis output. 

　　2.3 Decision boundary. 

　　　　2.3.1 Non-linear decision boundaries. 

　　2.4 Cost function for logistic regression. 

　　　　2.4.1 A convex logistic regression cost function. 

　　2.5 Simplified cost function and gradient descent. 

　　　　2.5.1 Probabilistic interpretation for cost function. 

　　　　2.5.2 Gradient Descent for logistic regression. 

　　2.6 Multiclass classification problem

key words: logistic regression, classification, decision boundary, convex function, One-vs-all


![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192030519-812563713.png=100x)

![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192042019-93741073.png)
![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192054848-888347764.png)
![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192140926-1899896864.png)
![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192155379-1587196352.png)
![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192208660-714307135.png)
![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192222738-878325537.png)
![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192238551-194444970.png)
![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192250035-1875959994.png)
![](http://images2015.cnblogs.com/blog/788978/201603/788978-20160328192302598-1542727721.png)

**2.6 Multiclass classification problem**

现实中也常遇到多分类问题(multiclass classification problem)，如判断手写的数字是0~9中的哪一个就是一个有10类的问题。多分类学习的基本思路是“拆解法”，即将多分类任务拆为若干个二分类任务求解。具体来说，先对问题进行拆分，然后为拆分出的每个二分类任务训练一个分类器（也就是h(x)）；在预测时，对这些分类器的预测结果进行集成。

下面介绍一个常用的拆分策略-“One-vs-all”.

One-vs-all每次将一个类的样例作为正例(“1”)，所有其他类作为反例(“0”)来训练n个分类器。在预测时，有两种情况看

情况1：若仅有一个分类器预测为正例，则对应的类别标记作为最终分类结果；
情况2：若有多个分类器预测为正例，则选择分类器的预测置信度最大的类别标记为分类结果。
例如对于图2-10所示的多分类问题，我们先将三角形，正方形，叉分别标记为类别1，2，3，然后做如下划分：

先将三角形看作正例“1”，正方形和叉看作反例“0”，训练出hθ1(x)
再将正方形看作正例“1”，三角形和叉看作反例“0”，训练出hθ2(x)
最后将叉看作正例“1”，三角形和正方形看作反例“0”，训练出hθ3(x)
预测时每一个预测值都是一个形如[hθ1(x), hθ2(x), hθ3(x)]的向量。选出最大的h(x)，它的上标就是对应的类别标记。例如若预测值为[0.13, 0.24, 0.79]，对应的就是上文所说的情况1，即只有hθ3(x) > 0.5表现为正例，所以应该认为是属于3标记类，即为叉。若预测值为[0.12, 0.83, 0.56], 对应的就是上文所说的情况2，hθ2(x) 和hθ3(x)都大于0.5，都预测为正例，但hθ2(x)> hθ3(x)，所以应该预测是属于2标记类，即为正方形。
![](http://images2015.cnblogs.com/blog/788978/201604/788978-20160404225732875-1143292626.png)


