---
layout:     post
title:      机器学习 —— KNN算法
subtitle:   
date:       2018-03-29
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - Machine Learning
---

# Introduction

&emsp;&emsp;k近邻(k-nearest neighbor，K-NN)是一种基本的分类与回归方法，我们通常使用knn作为分类器使用。knn算法比较直观：给定一个训练数据集，对于新的一个测试数据，在训练集上找出与该测试数据最为临近的k个样本，这k个样本的多数属于某个类（类别投票），就将该测试数据判为这个类。

![knn_example](https://raw.githubusercontent.com/AlistarHu/alistarhu.github.io/master/img/ml_knn_example.png)

用一个小例子具体说明一下knn分类的过程，如上图所示，对于测试样本（绿色点）我们需要对其所属类别进行预测。当k=3时，离其最近的3个点（实线圈中的点）中有2个点属于红色1个点属于蓝色，红色样本多于蓝色样本，所以我们将绿色样本点判为红色样本点所属的类别；当k=5时，离其最近的5个点（虚线圈中的点）中有3个蓝色点2个红色点，这时我们将绿色样本点判为蓝色样本所属的类别。

由这个例子我们可以看出，**knn模型并不具有显示的模型学习过程**，knn使用的模型实际上对应于对特征空间的划分，模型由：**距离度量、k值选取、分类决策规则** 三个要素决定。

## 距离度量

特征空间中两个实例点的距离反映了两者的相似度，评价两者相似的距离度量有很多种，这里我们最常用的是 **欧氏距离**。

更为一般的，knn模型的特征空间一般是n维实数向量空间$\mathbb{R}^n$，可以采用$L_p$距离，$L_p$距离定义如下所示：

[img[http://latex.codecogs.com/gif.latex?L_p(x_i , x_j)= ( \sum_{l=1}^{n} | x_{i}^{(l)} - x_{j}^{(l)} |^{p} )^ \frac{1}{p}]]

当p=2时，为欧式距离；p=1时，为曼哈顿距离。当$L_p$距离的p取不同值时，计算出的距离会有所差别，由此得出的最近邻点也会不同。

## k值选取

knn中k值的选取会对算法结果产生较大影响
- 如果k取较小的值，相当于使用了较小的邻域对实例点进行预测，只有与输入实例较近的样本才会对预测起作用；但预测也会对近邻的实例点非常敏感，如果近邻的实例点时噪声则会预测出错。**k值减小意味着模型复杂度增大，容易发生过拟合**。
- 如果k取较大的值，使用了较大的邻域中的样本对实例进行预测，可以减少估计误差；但同时与输入实例距离较远（不太相似）的训练样本也参与了预测，可能会影响预测结果。**k值过大会使得模型过于简单，从而忽略了训练实例中大量的有用信息**。

# Code Example

```python
# -*- coding: utf-8 -*-
"""
Created on Wed Mar 28 14:13:54 2018

@author: hulei
"""
import numpy as np
import os

# Predict the label of the test_x
def classify0(test_x, train_x, train_label, k):
    train_size=train_x.shape[0]
    # Broadcasting (don't make broadcasting is ok too, np will make it for us automatic when subtrack operation )
    test_x=np.tile(test_x,(train_size,1))   
    sqDiffMat=(test_x-train_x)** 2
    sqDistance=np.sum(sqDiffMat,axis=1)
    distance=sqDistance**0.5
    sortDistIdx=np.argsort(distance)    # get indices that would sort an array
    classCount={}
    for i in range(k):  # Statistic the labels of the nearest k samples
        curLabel=train_label[sortDistIdx[i],0]
        type(curLabel)
        classCount[curLabel]=classCount.get(curLabel,0)+1
    sortClassCount=sorted(classCount.items(), key=lambda x: x[1], reverse=True) # Get the sorted list[(key,value),...]
    return int(sortClassCount[0][0])        

# Load data from txt to numpy
def txt2numpy(fileName):
    f=open(fileName)
    lines=f.readlines() # Return a list of str: [line ,line,...]
    resMat=np.zeros((len(lines),3))
    label=np.zeros((len(lines),1),dtype=int)
    idx=0
    for line in lines:
        line=line.strip()   # Delete the \n of each line
        listFromLine=line.split('\t')
        resMat[idx,:]=listFromLine[0:3]
        label[idx,:]=listFromLine[-1]
        idx+=1
    return resMat,label

# Display the features
def plotScatter(data, labels, idx1, idx2):
    import matplotlib.pyplot as plt
    plt.figure(figsize=(8, 5), dpi=80)
    axes = plt.subplot(111)
    type1_x = []
    type1_y = []
    type2_x = []
    type2_y = []
    type3_x = []
    type3_y = []
    for i in range(label.shape[0]):
        if labels[i] == 1:  # didntLike
            type1_x.append(data[i][idx1])
            type1_y.append(data[i][idx2])
        if labels[i] == 2:  # smallDoses
            type2_x.append(data[i][idx1])
            type2_y.append(data[i][idx2])
        if labels[i] == 3:  # largeDoses
            type3_x.append(data[i][idx1])
            type3_y.append(data[i][idx2])

    type1 = axes.scatter(type1_x, type1_y, s=20, c='red')
    type2 = axes.scatter(type2_x, type2_y, s=40, c='green')
    type3 = axes.scatter(type3_x, type3_y, s=50, c='blue')

    plt.xlabel('fly distance km')
    plt.ylabel('play games time rito')
    axes.legend((type1, type2, type3), ('didntLike', 'smallDoses', 'largeDoses'), loc=2)
    plt.show()

def easyPlotScatter(data, labels, idx1, idx2):
    import matplotlib.pyplot as plt
    #   easy version
    plt.figure()
    plt.scatter(data[:,idx1], data[:,idx2], s=3*label, c=np.squeeze(label), label=np.squeeze(label))
    plt.title('Scatter')
    plt.xlabel('x')
    plt.ylabel('y')
    plt.legend(loc='best')
    plt.grid(True)
    plt.show()

# Norm the feature to 0~1
def autoNorm(data):
    minVals=np.min(data,axis=0)
    maxVals=np.max(data,axis=0)
    normalData=(data-minVals)/(maxVals-minVals)
    return normalData

def loadMnist(filename):
    res=np.zeros((1,1024))
    f=open(filename)
    for i in range(32):
        line=f.readline()
        for j in range(32):
            res[0,32*i+j]=int(line[j])
    return res

def handWriteClassfier():
    trainFileList=os.listdir('digits/trainDigits')
    train_num=len(trainFileList)
    train_data=np.zeros((train_num,1024))
    train_label=np.zeros((train_num,1))
    # Load each train sample
    for i in range(train_num):
        fileName=trainFileList[i]
        train_data[i,:]=loadMnist('digits/trainDigits/{}'.format(fileName))
        fileStr=fileName.split('.')[0]  # Get the name except of the .txt
        train_label[i,:]=int(fileStr.split('_')[0])
    # For test
    errCount=0
    testFileList=os.listdir('digits/testDigits')
    test_num=len(testFileList)
    for i in range(test_num):
        fileName=testFileList[i]
        testFeature=loadMnist('digits/testDigits/{}'.format(fileName))
        fileStr=fileName.split('.')[0]  # Get the name except of the .txt
        testLabel=int(fileStr.split('_')[0])
        testRes=classify0(testFeature, train_data, train_label, 3)
        print('the classifier came back with: {:d}, the real answer is: {:d}'.format(testRes, testLabel))
        if testRes!=testLabel:
            errCount+=1
    print('The total number of error is: {:d}'.format(errCount))
    print('The total accuracy rate is: {:f}'.format(1-errCount/test_num))

if __name__ =='__main__':
    # Case 1
    data,label=txt2numpy('datingTestSet2.txt')
    plotScatter(data,label,0,1)
    norMat,ma,mi=autoNorm(data)
    # Case2 for mnist classfier use knn
    handWriteClassfier()    # Accuracy is 0.989429
```
