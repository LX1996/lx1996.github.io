---
title: Linear_Regression笔记
updated: 2015-09-09 10:38
---

Content：

1. Linear Regression

　　1.1 Linear Regression with one variable

　　　　1.1.1 Gradient descent algorithm

　　1.2 Linear Regression with multiple variable

　　　　1.2.1 Feature Scaling

　　　　1.2.2 Features and polynomial regression

　　　　1.2.3 Normal equation

　　　　1.2.4 Probalilistic interpretation for cost function

key words: Linear Regression, Gradient Descent, Learning Rate, Feature Scaling, Normal Equation.

1.Linear Regression

1.1 Linear Regression with one variable
	![image](http://images2015.cnblogs.com/blog/788978/201603/788978-20160306203144096-1897459866.png)
	1.1.1 Gradient descent algorithm (梯度下降法)
	![image](http://images2015.cnblogs.com/blog/788978/201603/788978-20160306204343284-1109777704.png)
	迭代次数和learning rate是影响梯度下降法是否成功收敛到最优值的重要因素。

迭代次数：
过少可能使得算法还没有收敛就停止，
过多导致资源（时间等）的浪费；
learning rate:
过小，使得每次迭代时theta的变化量过小，从而算法收敛过慢，换言之需要增加迭代次数使得算法收敛；
过大，使得每次迭代时theta的变化量过大，可能在变化（迭代）过程中越过最优（收敛）点。

1.2 Linear Regression with multiple variables
![image](http://images2015.cnblogs.com/blog/788978/201603/788978-20160306205252080-1475559689.png)
![image](http://images2015.cnblogs.com/blog/788978/201603/788978-20160306210731534-570574008.png)
1.2.1 Feature Scaling（数据规范化）
给出一种规范化策略:

求每个特征量X的平均值mean
求每个特征量X的标准差segma         (matlab中std()函数)
规范化：X = (X-mean) / sigma

1.2.3 Normal equation（正则方程）

theta = pinv(x' * x) * x' * y
