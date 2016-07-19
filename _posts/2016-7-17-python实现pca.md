---
title: python实现pca
updated: 2016-07-17 16：30
---


PCA()函数有两个参数，第一个参数是用于进行pca操作的数据集，第二个参数topNfeat是一个可选参数，即应用的n个特征，需要指定，否则函数会返回前9999999个特征，或者原始数据中所有的特征。

	from numpy import *

	def loadDataSet(fileName, delim='\t'):
   		fr = open(fileName)
    	stringArr = [line.strip().split(delim) for line in fr.readlines()]
    	datArr = [map(float,line) for line in stringArr]
    	return mat(datArr)

	def pca(dataMat, topNfeat=9999999):
    	meanVals = mean(dataMat, axis=0)
    	meanRemoved = dataMat - meanVals #去除平均值
    	covMat = cov(meanRemoved, rowvar=0)
    	eigVals,eigVects = linalg.eig(mat(covMat))
    	eigValInd = argsort(eigVals)            #从小到大排序
    	eigValInd = eigValInd[:-(topNfeat+1):-1]  
    	redEigVects = eigVects[:,eigValInd]      
    	lowDDataMat = meanRemoved * redEigVects
    	reconMat = (lowDDataMat * redEigVects.T) + meanVals #将数据转换到新空间
    	return lowDDataMat, reconMat
   
效果图：
![image](/Users/Guolz/GitHub/JLUNeverMore.github.io/_posts/pca_2.png)

图1: 原始数据集（三角形点表示）及第一主成分(圆形点)表示

利用PCA 对半导体制造数据降维
	
代码及数据集地址：https://github.com/JLUNeverMore/python_PCA

该数据包含很多的缺失值。这些缺失值是以NaN（Not a Number）标识的。我们用平均值来代替缺失值，平均值根据那些非NaN得到。

	def replaceNanWithMean():
    datMat = loadDataSet('secom.data', ' ')
    numFeat = shape(datMat)[1]
    for i in range(numFeat):
        meanVal = mean(datMat[nonzero(~isnan(datMat[:,i].A))[0],i]) #values that are not NaN (a number)
        datMat[nonzero(isnan(datMat[:,i].A))[0],i] = meanVal  #set NaN values to mean
    return datMat
    
在该数据集上应用PCA。首先确认所需特征和可以去除特征的数目。PCA会给出数据中所包含的信息量。数据指的是接受的原始材料，其中可能包含噪声和不相关信息。信息是指数据中的相关部分。
通过计算，我们的到主成分数目与方差的百分比的关系图：

	dataMat = pca.replaceNanWithMean()
	meanVals = mean(dataMat, axis=0)
	meanRemoved = dataMat - meanVals #remove mean
	covMat = cov(meanRemoved, rowvar=0)
	eigVals,eigVects = linalg.eig(mat(covMat))
	eigValInd = argsort(eigVals)            #sort, sort goes smallest to largest
	eigValInd = eigValInd[::-1]#reverse
	sortedEigVals = eigVals[eigValInd]
	total = sum(sortedEigVals)
	varPercentage = sortedEigVals/total*100

	fig = plt.figure()
	ax = fig.add_subplot(111)
	ax.plot(range(1, 21), varPercentage[:20], marker='^')
	plt.xlabel('Principal Component Number')
	plt.ylabel('Percentage of Variance')
	plt.show()
	
	
![image](/Users/Guolz/GitHub/JLUNeverMore.github.io/_posts/pca_1.png)

上图为前20个主成分占总方差的百分比。可以看出，大部分方差都包含在前面的几个主成分中，舍弃后面的主成分并不会损失太多的信息。如果保留前六个主成分，则数据集可以从590个特征压缩成6个特征，大概实现了100:1的压缩。

以上分析能够得到所用到的主成分的数目，然后我们可以将该数目输入到pca算法中，最后的到约简后的数据就可以在分类器中使用了。

