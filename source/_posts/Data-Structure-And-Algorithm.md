---
title: Data Structure And Algorithm
date: 2019-12-12 22:45:02
copyright: true
tags: [数据结构与算法]
categories: [计算机基础]
typora-root-url: DatastructureAndAlgorithm

---
<meta name="referrer" content="no-referrer" />  

<!--more-->

# 数据结构与算法总纲

## Part 1 数据结构是什么
&emsp;信息中的各个元素在客观世界中是有结构关系的，比如 *学生会的组织架构*。
&nbsp;如何表示这些结构关系，和如何在计算机中存储数据，以及对这些数据进行哪些操作
&nbsp;这些成为了我们要努力解决的问题，而且数据结构与算法作为一名程序员的"内功修为"，

应当好好学习，为以后的学习打好基础。

&emsp;所以，数据结构与算法我们要从以下3个方面学习:

- 1.逻辑结构(是什么)

- 2.存储结构(怎么存)

- 3.相关算法(如何用)

  

## Part 2 基本名词和术语

1.数据(Data)
&emsp;数据是信息的载体，主要分为两大类
&emsp;&emsp;(1)数值型 (integer,float,double...)
&emsp;&emsp;(2)非数值型 (string,语音，图片...)

2.数据元素(Data element)
&emsp;数据元素是描述实体世界中*最小的数据单位*,也称结点（Node）或记录（Record）

3.数据对象(Data object)
&emsp;有相同性质的数据元素的集合

4.数据项(Data item)
&emsp;是数据不可分割的最小单位，也称域(field)

PS:一堆数据项构成数据元素，相同的数据元素构成数据对象，每个数据对象都是数据的一种

5.结构(Structure)
&emsp;数据元素之间存在某种联系，这种联系叫做 *结构*
，依照离散数学我们可以给数据结构一个明确的叙述方式
&emsp;&emsp;Date-Structure = (D,R)
D为数据元素的集合，R是D上关系的集合
**所谓关系包括**
&emsp;i.元素间的->*逻辑结构*(线性结构，非线性结构)
&emsp;ii.该结构在计算机内存中的表示->*存储结构*(顺序存储，链式存储)

![001](https://images.gitee.com/uploads/images/2019/1215/141855_7d3eb9cd_5550632.png)



## Part 3 什么是算法
&emsp;算法是一个集合，一个完成某类特定问题的代码集合。即，算法是解决问题的方法。

根据问题的不同，算法也可以分为好几类，比如:

&emsp;解决数值问题的算法叫数值算法，

&emsp;&emsp;如求解数值积分，代数方程，常微分方程等。

非数值类算法包括，查找算法，排序算法，插入或删除算法以及遍历算法等。

&emsp;既然,算法是为了解决问题而诞生的，那么它自然要满足一下性质:

&emsp;&emsp;**1. 有穷性**&nbsp;：为了解决问题那必然要在规定*步骤*内完成

**&emsp;&emsp;2. 确定性**：&nbsp;解决一种的问题，算法的每一步都应当清晰地具有其唯一的意义

**&emsp;&emsp;3. 有效性**：&nbsp;算法的每一条指令都应当是可执行的，比如0不能做分母

# Part 4 如何度量算法的优劣程度

&emsp;由于计算机性能不同，编译能力不同，导致了程序在计算机内的运行时间是不同的，为了比较解决同一问题的不同算法的运行时间，我们要引入一个不被外界因素所影响的*度量方式*。我们通常把程序语句的执行次数的多少作为算法时间复杂度的度量分析称为**频度统计法**。

&emsp;**语句频度**(Frequency count)：指某语句重复执行的次数。

例如：

```python
def func(n):    
    #算法频度f(n) = 2*n+1    
    cnt = 0#执行1次    
    while n>0:        
        cnt+=1#执行n次        
        n-=1 #执行n次   
    return cnt
```

&emsp;想要全面地分析一个算法的效率，我们应考虑*最好情况下的时间代价*，*平均情况下的时间代价*，*最坏情况下时间代价*，有关这些概念的详细严谨的数学定义在《算法导论》中，在此我就不赘述了。但是，我们主要考虑在最坏情况下的算法时间的复杂度。对于最坏情况我们用大O表示，例如：T(1000) = O(1),T(4n³+5n²+n+1) = O(n³)

### 4.1语句频度可视化



```python
import matplotlib.pyplot as plt

def func(n):
    cnt = 0
    while n>0:
        cnt+=1
        n-=1 
    return cnt#计算执行次数
x =[i+0 for i in range(50)]
cnt =[]
for i in x:
    cnt.append (func(i))
plt.plot(x,cnt)
plt.show()
```

![O(n)](https://images.gitee.com/uploads/images/2019/1215/142032_536c6cbc_5550632.png)
