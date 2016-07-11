---
title: 用scikit-learn求解一元线性回归
updated: 2016-07-25 10:50
---

scikit-learn的一元线性回归

    import numpy as np
    from sklearn.linear_model import LinearRegression

	x = [[1],[2],[3],[4],[5],[6]]
	y = [[1],[2.1],[2.9],[4.2],[5.1],[5.8]]
	model = LinearRegression()
	model.fit(x, y)
	predicted = model.predict([13])[0]
	print predicted
执行结果

	[[ 12.82666667]]
	
画一元线性图像
	
	import matplotlib.pyplot as plt
	from matplotlib.font_manager import FontProperties
	font = FontProperties()

	plt.figure()
	plt.title('this is title')
	plt.xlabel('x label')
	plt.ylabel('y label')
	plt.axis([0, 25, 0, 25])
	plt.grid(True)
	x = [[1],[2],[3],[4],[5],[6]]
	y = [[1],[2.1],[2.9],[4.2],[5.1],[5.8]]
	plt.plot(x, y, 'k.')
	plt.show()
	

预测 ＋ 作图
	
	import numpy as np
	from sklearn.linear_model import LinearRegression
	import matplotlib.pyplot as plt
	from matplotlib.font_manager import FontProperties

	x = [[1],[2],[3],[4],[5],[6]]
	y = [[1],[2.1],[2.9],[4.2],[5.1],[5.8]]
	model = LinearRegression()
	model.fit(x, y)
	x2 = [[0], [2.5], [5.3], [9.1]]
	y2 = model.predict(x2)

	plt.figure()
	plt.title('linear sample')
	plt.xlabel('x')
	plt.ylabel('y')
	plt.axis([0, 10, 0, 10])
	plt.grid(True)
	plt.plot(x, y, 'k.')
	plt.plot(x2, y2, 'g-')
	plt.show()
	
![image](http://www.shareditor.com/uploads/media/my-context/0001/01/5817c1dfb64abacc3811b88ec69931bdd8ff85fc.png)

模型评估

R方度量方法可以评估线性回归效果，R方也叫确定系数，表示模型对现实数据的拟合程度。R方算法为：1-(残差平方和/样本总体平方和)

也可以用model.score()方法直接计算R方

