---
title: Numpy基础
declare: true
date: 2020-07-30 09:35:50
toc: true
tags: Python
categories: [计算机基础,Python]
---



<meta name="referrer" content="no-referrer" />  

<!--more-->

[TOC]

# NumPy基础



## Part 0 NumPy 是什么

Numpy是Python科学计算中的一个基础包，它包括操作效率高的数组，数学运算，逻辑运算，排序，选择，I/O，基础的线代库，基础统计操作，随机数等等。

而这一系列操作的载体其实就是**numpy 数组**，也就是之后要讲的Ndarray对象。

```python
import numpy as np
l = [1,2,3]
n = np.array([x*2 for x in l])

print((type(l),type(n)))
```

```
(<class 'list'>, <class 'numpy.ndarray'>)
```



## Part 1 Ndarray 对象

NumPy中最重要的对象就是**ndarray的N维数组类型**

ndarray索引从零开始，描述的是相同类型元素集合。

### 0x00 ndarray介绍

> ndarray的每个元素内存中的存储大小相同
>
> ndarray中的每个对象都是数据类型对象的对象（dtype）
>
> ndarray的元素访问可以通过Python数组类型标量进行切片访问

![输入图片说明](https://images.gitee.com/uploads/images/2020/0730/112134_9f7cee20_5550632.png "屏幕截图.png")

上图是体现的是数据类型和数组标量之间的关系

### 0x01 创建NumPy的基本对象Ndarray

```python
def array(p_object, dtype=None, copy=True, order='K', subok=False, ndmin=0):pass
```

p_object : 任何的对象序列

dtype: 数组的所需数据类型

copy: 默认true，对象是否被复制

order{'K','A','C','F'}:可选，指定序列内存排列布局

subok：默认情况下放回的数组强制为父类数组

ndmin：指定返回数组的最小维数

```python
import numpy as np

arr = [1,2,3,4,5]
my_matrix = [[1,2,3],[4,5,6]]
new_arr = np.array(arr)#生成一维数组
new_my_matrix = np.array(my_matrix)#生成二维数组
print(type(new_arr),type(new_my_matrix))
print(new_arr.shape)
print(new_my_matrix.shape)

```

```
<class 'numpy.ndarray'> <class 'numpy.ndarray'>
(5,)
(2, 3)
```

指定数据类型dtype

```python
import numpy as np

my_matrix = [[1,2,3],[4,5,6]]

new_my_matrix = np.array(my_matrix,dtype=float)
print(new_my_matrix)
print(new_my_matrix.dtype)

```

```
[[1. 2. 3.]
 [4. 5. 6.]]
float64
```

指定维度

```python
import numpy as np

my_array = np.array([1,2,3,4,5],dtype=float,ndmin=2)
print(my_array)
print(my_array.dtype)
print(my_array.ndim)

```

```
[[1. 2. 3. 4. 5.]] #这里从1维数组变成了2维数组
float64
2
```

<img src="http://dolphin-public.oss-cn-shanghai.aliyuncs.com/img/Teacher-liang/attr.jpg">

```python
import numpy as np

arr = np.array([i for i in range(1,13)])
arr = arr.reshape((3,4))

print(arr)
print("元素类型:",arr.dtype)
print("元素所占字节数:",arr.itemsize)
print("数组形状:",arr.shape)
print("数组内元素个数:",arr.size)
print("数组内元素所占空间:",arr.nbytes) #实际上比它大
print("数组维数:",arr.ndim) 


```

```
[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
元素类型: int32
元素所占字节数: 4
数组形状: (3, 4)
数组内元素个数: 12
数组内元素所占空间: 48
数组维数: 2
```

这里再附上NumPy中的数据类型图

![输入图片说明](https://images.gitee.com/uploads/images/2020/0730/114707_853cd669_5550632.png "屏幕截图.png")

### 0x02 Ndarray更改类型

方式一： asarray 方法

```python
import numpy as np

arr = np.array([i for i in range(1,13)])
arr = arr.reshape((3,4))

print("原元素数据类型:",arr.dtype)
arr = np.asarray(arr,dtype=np.float64)
print(arr)
print("现元素类型:",arr.dtype)

```

```
原元素数据类型: int32
[[ 1.  2.  3.  4.]
 [ 5.  6.  7.  8.]
 [ 9. 10. 11. 12.]]
现元素类型: float64
```

方式二：astype 方法

```python
import numpy as np

arr = np.array([i for i in range(1,13)])
arr = arr.reshape((3,4))

print("原元素数据类型:",arr.dtype)
arr = arr.astype(np.complex,copy = True)
print(arr)
print("现元素类型:",arr.dtype)

```

```
原元素数据类型: int32
[[ 1.+0.j  2.+0.j  3.+0.j  4.+0.j]
 [ 5.+0.j  6.+0.j  7.+0.j  8.+0.j]
 [ 9.+0.j 10.+0.j 11.+0.j 12.+0.j]]
现元素类型: complex128
```



## Part 2 创建Numpy数组

### 2.1 数组生成

#### 0x00 生成一个全 0 或 1 的数组

```python
def zeros(shape, dtype=None, order='C'):pass
def ones(shape, dtype=None, order='C'):pass
```

```python
import numpy as np

z = np.zeros(3,dtype=np.int64)
o = np.ones(4,dtype=complex)
print(z)
print(o)
o1 = np.ones([3,4],dtype=np.float64)
print(o1)

```

```
[0 0 0]
[1.+0.j 1.+0.j 1.+0.j 1.+0.j]
[[1. 1. 1. 1.]
 [1. 1. 1. 1.]
 [1. 1. 1. 1.]]
```

#### 0x01 生成一个未初始化的空数组

```python
import numpy as np

arr = np.empty(3)
print(arr)
arr.fill(5)
print(arr)
```

```
[ 2.05226842e-289 -7.06270388e-311  2.94261135e-314]
[5. 5. 5.]
```



#### 0x02 单位数组(矩阵)

```python
def eye(N, M=None, k=0, dtype=float, order='C'):pass
```

N：列数

M：行数

k：指定对角线右上方的第k条的斜线的1

```python
import numpy as np

arr = np.eye(4,k=0)
print(arr)
arr2 = np.eye(4,k=1)
print(arr2)

```

```
[[1. 0. 0. 0.]
 [0. 1. 0. 0.]
 [0. 0. 1. 0.]
 [0. 0. 0. 1.]]
[[0. 1. 0. 0.]
 [0. 0. 1. 0.]
 [0. 0. 0. 1.]
 [0. 0. 0. 0.]]
```

##### empty_like,ones_like,zeros_like

三种数组拷贝函数

#### 0x03 指定步长范围数组 arange

```python
import numpy as np

arr = np.arange(4)
print(arr)
print("===========")
arr2 = np.arange(1,20,4)
print(arr2)
```

```
[0 1 2 3]
===========
[ 1  5  9 13 17]
```



#### 0x04 等差数列 linspace

```python
def linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None,
             axis=0):pass
```

start：首项

stop：末项，如果endpoint为True则包含该项

num：生成数列的长度

```python
import numpy as np

arr = np.linspace(1,5,9)
print(arr)

```

```
[1.  1.5 2.  2.5 3.  3.5 4.  4.5 5. ]
```

##### 利用等差数列画个正弦函数

```python
import numpy as np
import matplotlib.pyplot as plt
x = np.linspace(-np.pi,np.pi,100)
print("x.shape: ",x.shape)

y = np.sin(x)
print("y.shape: ",y.shape)

plt.plot(x,y)
plt.show()
```

![输入图片说明](https://images.gitee.com/uploads/images/2020/0731/135609_f7b84a7a_5550632.png "屏幕截图.png")



#### 0x05 等比数列 logspace

```python
import numpy as np

arr = np.logspace(1,100,10)
print(arr)
```

```
[1.e+001 1.e+012 1.e+023 1.e+034 1.e+045 1.e+056 1.e+067 1.e+078 1.e+089
 1.e+100]
```



#### 0x06 生成随机数组 np.random

##### 范围在0~1 的随机数组

```python
import numpy as np

arr = np.random.random(size=5)
print(arr)
```

```
[0.02902678 0.1782832  0.280288   0.28477374 0.2899477 ]
```

##### 服从标准正态分布的随机数

```python
import numpy as np

num = np.random.randn()
print(num)
```

```
1.067611490833676
```

##### 服从均匀分布的随机数

```python
import numpy as np

num = np.random.rand()
print(num)
```

```
0.7849484854012925
```

##### 指定整数范围的随机数

```python
def randint(low, high=None, size=None, dtype='l'):pass
```

low：起始位

high：终止位

size：个数

```python
import numpy as np

arr = np.random.randint(1,10,size = 5)
print(arr)
```

```
[9 5 4 5 4]
```

### 2.2 数组元素访问

#### 0x00 一维数组元素访问

numpy数组下标从0开始，怎么索引正常数组就怎么索引numpy数组，同时numpy数组支持像list类型一样的各种索引操作。

```python
import numpy as np

a = np.array([0,1,2,3,4,5,6,7,8,9,10])
print("正常索引:")
print(a[0],a[2])
print("切片索引:")
print(a[:3])
print("指定步长的切片索引:")
print(a[::2])
print("负索引:")
print(a[-1],a[-2])
```

```
正常索引:
0 2
切片索引:
[0 1 2]
指定步长的切片索引:
[ 0  2  4  6  8 10]
负索引:
10 9
```



#### 0x01 多维数组元素访问

```python
import numpy as np

a = np.arange(12).reshape((3,4))
print(a)
print("正常索引:")
print(a[1,1])
print("取单独一行:")
print(a[:1])
print("取单独一列:")
print(a[:,2])

```

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
正常索引:
5
取单独一行:
[[0 1 2 3]]
取单独一列:
[ 2  6 10]
```

单独提一嘴关于高维索引的问题。

以二维数组为例，如果只写一个下标，那就是默认取对应的那一行。那么由此就可以衍生出**通过切片操作来获取各列**的操作。

以 a[:,2] 为例：

以 逗号 , 为分割，左侧切片表示我要取所有行，右侧声明取所有列下标为2 的子数组。由于numpy数组索引方式比起传统的C奇怪，那么我们就来看看这些奇奇怪怪的索引方式：

```python
import numpy as np

a = np.arange(81).reshape((9,9))
print(a)
print("行列切片索引+步长:")
print(a[2::2,::2]) #从第3行到最后一行，步长为2选行，从第一列到最后一列 步长为2选列
print("负索引切片+步长:")
print(a[-5:,-4:-1:2])#从倒数第5行到最后一行，取倒数第4行到倒数第二行，以步长为2取值


```

```
[[ 0  1  2  3  4  5  6  7  8]
 [ 9 10 11 12 13 14 15 16 17]
 [18 19 20 21 22 23 24 25 26]
 [27 28 29 30 31 32 33 34 35]
 [36 37 38 39 40 41 42 43 44]
 [45 46 47 48 49 50 51 52 53]
 [54 55 56 57 58 59 60 61 62]
 [63 64 65 66 67 68 69 70 71]
 [72 73 74 75 76 77 78 79 80]]
行列切片索引+步长:
[[18 20 22 24 26]
 [36 38 40 42 44]
 [54 56 58 60 62]
 [72 74 76 78 80]]
负索引切片+步长:
[[41 43]
 [50 52]
 [59 61]
 [68 70]
 [77 79]]

```

再追加一个布尔索引，布尔值大部分是通过运算得出的：

```python
import numpy as np

arr = np.arange(10)
print(arr)
boolean = [True,False,False,False,True,True,False,True,False,True]
print("布尔索引结果: ")
print(arr[boolean])
print("==============")
print(arr[arr % 2 == 1])
```

```
[0 1 2 3 4 5 6 7 8 9]
布尔索引结果: 
[0 4 5 7 9]
==============
[1 3 5 7 9]
```

### 2.3 数学运算与统计函数

#### 0x00 ndarray 与 数字

和正常的Python四则运算差不多一样：

```python
import numpy as np

arr = np.arange(1,10,2)
print(arr)
print("开始进行四则运算:")
print(arr+5)
print("==========")
print(arr-5)
print("==========")
print(arr*5)
print("==========")
print(arr/5)

```

```
[1 3 5 7 9]
开始进行四则运算:
[ 6  8 10 12 14]
==========
[-4 -2  0  2  4]
==========
[ 5 15 25 35 45]
==========
[0.2 0.6 1.  1.4 1.8]
```

#### 0x01 ndarray 间的运算

```python
import numpy as np

arr = np.arange(1,10,2)
arr2 = np.arange(2,11,2)
print("arr: ",arr)
print("arr2: ",arr2)
print("=============")
print(arr+arr2)
print(np.add(arr,arr2))
print("=============")
print(arr-arr2)
print(np.subtract(arr,arr2))
print("=============")
print(arr*arr2)
print(np.multiply(arr,arr2))
print("=============")
print(arr/arr2)
print(np.divide(arr,arr2))
print("=============")
print(arr**arr2)
print(np.power(arr,arr2))
print("=============")
print(arr%arr2)
print(np.remainder(arr,arr2))
```

同形的ndarray才能相互运算。

```
arr:  [1 3 5 7 9]
arr2:  [ 2  4  6  8 10]
=============
[ 3  7 11 15 19]
[ 3  7 11 15 19]
=============
[-1 -1 -1 -1 -1]
[-1 -1 -1 -1 -1]
=============
[ 2 12 30 56 90]
[ 2 12 30 56 90]
=============
[0.5        0.75       0.83333333 0.875      0.9       ]
[0.5        0.75       0.83333333 0.875      0.9       ]
=============
[         1         81      15625    5764801 -808182895]
[         1         81      15625    5764801 -808182895]
=============
[1 3 5 7 9]
[1 3 5 7 9]
```

#### 0x02 三角函数

![输入图片说明](https://images.gitee.com/uploads/images/2020/0803/150850_c02c49bb_5550632.png "屏幕截图.png")

#### 0x03 双曲函数

![输入图片说明](https://images.gitee.com/uploads/images/2020/0803/150935_672776ba_5550632.png "屏幕截图.png")

#### 0x04 指数和对数

![image-20200803151034091](C:\Users\micha\AppData\Roaming\Typora\typora-user-images\image-20200803151034091.png)

#### 0x05 数值修约

![输入图片说明](https://images.gitee.com/uploads/images/2020/0803/151119_456b3362_5550632.png "屏幕截图.png")

```python
import numpy as np

print(np.around([8.6,6.2]))
print(np.rint([8.1,6.2]))
```

```
[9. 6.]
[8. 6.]
```

无穷大的表示为：np.inf

```python
import numpy as np

print(np.inf)
print(-np.inf)
```

```
inf
-inf
```

#### 0x06 数值统计

![输入图片说明](https://images.gitee.com/uploads/images/2020/0804/144142_b056c4f5_5550632.png "屏幕截图.png")

这一大堆函数本身求的内容我感觉没有必要进行详细说明，但是其中的axis非常值得说道。

```python
m = np.arange(15).reshape((3,5))
print(m)
print("=====================")
print(m.sum())
print("按行求和 axis = 0: ")
print(m.sum(axis = 0))
print("按列求和 axis = 1: ")
print(m.sum(axis = 1))
```

```
[[ 0  1  2  3  4]
 [ 5  6  7  8  9]
 [10 11 12 13 14]]
=====================
105
按行求和 axis = 0: 
[15 18 21 24 27]
按列求和 axis = 1: 
[10 35 60]
```

axis到底是什么？它其实代表着**按哪个维度进行折叠**。

axis：0代表列：1代表行。当参数axis = 0时，代表**以一行为基本元向每一行进行合并折叠运算 **。列同理。

axis = 0 :

![输入图片说明](https://images.gitee.com/uploads/images/2020/0804/150036_889ed09e_5550632.png "屏幕截图.png")

axis = 1 :

![输入图片说明](https://images.gitee.com/uploads/images/2020/0804/150125_fd132cf5_5550632.png "屏幕截图.png")

比如这里有一个3维数组，按照惯例它可以分成3维标号为0，1，2

```python
import numpy as np

m = np.array(
    [[[1,2,3],[11,22,33],[111,222,333]],
     [[4,5,6],[44,55,66],[444,555,666]]
     ]
)
print(m)
print("m.dimension: ",m.ndim)
print("axis = 0: ") # 3维数组中以2维数组的 行 方向对应加和
print(m.sum(axis= 0))
print("axis = 1: ")# 3维数组中以2维数组的 列 方向对应加和
print(m.sum(axis = 1))
print("axis = 2: ")# 3维数组中以2维数组中的一维数组为单位进行加和
print(m.sum(axis = 2))

```

```
[[[  1   2   3]
  [ 11  22  33]
  [111 222 333]]

 [[  4   5   6]
  [ 44  55  66]
  [444 555 666]]]
m.dimension:  3
axis = 0: 
[[  5   7   9]
 [ 55  77  99]
 [555 777 999]]
axis = 1: 
[[123 246 369]
 [492 615 738]]
axis = 2: 
[[   6   66  666]
 [  15  165 1665]]
```

最大最小值位置:

```python
import numpy as np

a = np.random.randint(1,100,25).reshape((5,5))
print(a)
print("每一行最大值位置: ",np.argmax(a,axis = 1))
print("每一列最大值位置: ",np.argmax(a,axis = 0))
print("全局最大值位置: ",np.argmax(a))
```

```
[[41 60 86 38 14]
 [57 48 14 52 38]
 [31 10 27 21 45]
 [70 46 38  2 98]
 [90  4  8 83 90]]
每一行最大值位置:  [2 0 4 4 0]
每一列最大值位置:  [4 0 0 4 3]
全局最大值位置:  19
```



### 2.4 数组合并与拆分



### 2.5 NumPy 线性代数库



## Part 3 Numpy矩阵

