---
title: Sklearn入门
declare: true
date: 2021-03-11 18:07:09
tags: 机器学习
categories: [Python,机器学习]
toc: true
---



<meta name="referrer" content="no-referrer" />  

<!--more-->

# Scikit-learn 入门

[TOC]

scikit-learn 又称sklearn是Python在机器学习方面的一个第三方库,功能强大，值得学习。本文的学习方式为**官网文档 + 动手实践**的方法。学习路线按照模型的种类来学习，现在让我们开始吧!

## Part 1 线性模型 (Linear Model)

### 1.1 线性回归模型

线性回归模型的假设函数为:
$$
h_\theta(x)=\theta_0+\theta_1x_1+\theta_2x_2+...
$$
我们的目的是找出模型参数θ，那么在sklearn中，我们需要进行如下操作：

```python
import matplotlib.pyplot as plt
import numpy as np
from sklearn import datasets,linear_model
from sklearn.metrics import mean_squared_error
"""
依次导入模块,
从sklearn中到处datases数据集和线性模型
从metrics(度量)中导入均方根误差，
我们选择糖尿病数据集的第一维特征做实验
"""
#加载数据集
diabetes_x,diabetes_y = datasets.load_diabetes(return_X_y=True)
#选取原数据集所有行,新增一个数组维度，取第一维特征
diabetes_x = diabetes_x[:,np.newaxis,2]
#切片选取特征向量
diabetes_x_train = diabetes_x[:-20]
diabetes_x_test = diabetes_x[-20:]
#切片选取标签
diabetes_y_train = diabetes_y[:-20]
diabetes_y_test = diabetes_y[-20:]
#新建线性回归模型对象
regr = linear_model.LinearRegression()
#拟合数据集
regr.fit(diabetes_x_train,diabetes_y_train)
#预测测试集
diabetes_y_predicted = regr.predict(diabetes_x_test)
#打印模型参数θ
print("Coefficients: ",regr.coef_)
#计算均方根误差值
print("Cost function Value: %.2f"%mean_squared_error(diabetes_y_test,diabetes_y_predicted))
#画图
plt.scatter(diabetes_x_test,diabetes_y_test,color="black")
plt.plot(diabetes_x_test,diabetes_y_predicted,color="red")

plt.xticks()
plt.yticks()
plt.show()

```

在线性回归模型中存在**两个重要属性**，**coef\_和intercept\_**。
$$
coef\_ \;显示 \;[\theta_1...\theta_n]\\
intercept\_\;显示 \;\theta_0(截距)
$$
同时它也存在两个核心方法**fit和predict**声明如下：

```python
    def fit(self, X, y, sample_weight=None):
        """
        Fit linear model.

        Parameters
        ----------
        X : {array-like, sparse matrix} of shape (n_samples, n_features)
            Training data

        y : array-like of shape (n_samples,) or (n_samples, n_targets)
            Target values. Will be cast to X's dtype if necessary

        sample_weight : array-like of shape (n_samples,), default=None
            Individual weights for each sample

            .. versionadded:: 0.17
               parameter *sample_weight* support to LinearRegression.

        Returns
        -------
        self : returns an instance of self.
        """
        pass
```

在fit方法中：X 是特征向量组成的矩阵，y是训练标签向量，sample_weight为一个向量代表样本权重。该方法用于拟合数据集。

```python
    def predict(self, X):
        """
        Predict using the linear model.

        Parameters
        ----------
        X : array-like or sparse matrix, shape (n_samples, n_features)
            Samples.

        Returns
        -------
        C : array, shape (n_samples,)
            Returns predicted values.
        """
        pass
```

在predict方法中：X为测试集或交叉验证集的特征矩阵，返回一个预测结果的向量。

### 1.2 逻辑回归模型





