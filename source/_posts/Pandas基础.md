---
title: Pandas 基础
declare: true
date: 2020-04-08 09:31:48
toc: true
tags: Python
categories: [计算机基础,Python]

---



<meta name="referrer" content="no-referrer" />  

<!--more-->

# Pandas 基础

[TOC]

## Part 0 Pandas 是什么的

Pandas是基于Numpy的一个工具用来解决数据分析任务。

在Pandas里我们有两个重要的类。一个是**Series**，另一个是**DataFrame**。

先介绍Series，你可以把它理解成一个可以自定义索引的列向量。

![](https://images.gitee.com/uploads/images/2020/0717/164107_553b90c0_5550632.png )

其次是DataFrame，你可以暂时地把它理解成一张二维表(像数据库里的那种):

![](https://images.gitee.com/uploads/images/2020/0720/105044_7926e42a_5550632.png)

介绍完这两大类的特征之后。我们来谈谈怎么学。

把它们当作两个数据结构，我们先学如何创建，然后就是老一套的增，删，改，查

## Part 1 Series 

### 1.1 创建 Series 对象

直接撸源码，看看它要啥：

![](https://images.gitee.com/uploads/images/2020/0717/165107_21fde128_5550632.png )

重要的参数有：**data**，**index**，**name**

> data => 指定数据
>
> index => 指定索引
>
> name=> 给Series起个名

```python
import pandas as pd

my_series = pd.Series(data=[1,2,3,4],index=['a','b','c','d'],name="my test")
print(my_series)
```

```
运行结果：
a    1
b    2
c    3
d    4
Name: my test, dtype: int64
```

看看空的Series是什么类型

```python
import pandas as pd

my_series = pd.Series()
print(type(my_series))
print(my_series)
```

```
运行结果：
<class 'pandas.core.series.Series'>
Series([], dtype: float64)
```



一般而言，我们习惯以传参的形式进行类的实例化。而且一般数据是从文件中读取出来的，我们接下来，准备介绍两种生成Series对象的方法。**自定义指定法**和**从dict类型中生成**

#### 0x00 自定义生成

自定义生成的核心在于如何定义索引。你可以不指定索引，那样的话pandas会自动生成一个：

**range(0,len(data),1) 的数字索引**

先看正常模式：

```python
import pandas as pd

data = [1,2,3,4]
index = ['a','b','c','d']
my_series = pd.Series(data= data,index = index)
```

```
运行结果：
a    1
b    2
c    3
d    4
dtype: int64
```

再看不指定索引的模式

```python
import pandas as pd

data = [1,2,3,4]
my_series = pd.Series(data= data)
print(my_series)
```

```
运行结果：
0    1
1    2
2    3
3    4
dtype: int64
```



#### 0x01 从dict中生成

由于字典类型本身就是键值对，所以字典类型的数据没有必要声明索引

```python
import pandas as pd

data = {'a':10,'b':20,'c':30}
my_series = pd.Series(data= data)
print(my_series)
```

```
运行结果：
a    10
b    20
c    30
dtype: int64
```

当然了，你要是不信邪偏要给它安索引，会发生如下效果：

```python
import pandas as pd

data = {'a':10,'b':20,'c':30}
index = ['aa','bb','cc']
my_series = pd.Series(data= data,index = index)
print(my_series)
```

```
运行结果：
aa   NaN
bb   NaN
cc   NaN
dtype: float64
```

**NaN代表找不到该索引对应的元素**



### 1.2 Series的运算

既然，Series可以看成自定义索引的列向量，那么势必是Series可以进行运算的

#### 0x00 Series 的四则运算

同型运算

```python
import pandas as pd

d1 = {'a':1,'b':2,'c':3}
d2 = {'a':10,'b':20,'c':30}
s1 = pd.Series(data = d1)
s2 = pd.Series(data = d2)
print("加法\n",s1+s2)
print("减法\n",s1-s2)
print("乘法\n",s1*s2)
print("除法\n",s1/s2)
```

```
运行结果
加法
 a    11
b    22
c    33
dtype: int64
减法
 a    -9
b   -18
c   -27
dtype: int64
乘法
 a    10
b    40
c    90
dtype: int64
除法
 a    0.1
b    0.1
c    0.1
dtype: float64
```

不同型运算

```python
import pandas as pd

d1 = {'a':1,'b':2,'c':3}
d2 = {'a':10,'b':20,'c':30,'d':40}

s1 = pd.Series(data = d1)
s2 = pd.Series(data = d2)

print("加法\n",s1+s2)
print("减法\n",s1-s2)
print("乘法\n",s1*s2)
print("除法\n",s1/s2)
```

```
运行结果
加法
 a    11.0
b    22.0
c    33.0
d     NaN
dtype: float64
减法
 a    -9.0
b   -18.0
c   -27.0
d     NaN
dtype: float64
乘法
 a    10.0
b    40.0
c    90.0
d     NaN
dtype: float64
除法
 a    0.1
b    0.1
c    0.1
d    NaN
dtype: float64
```

索引打乱运算

```python
import pandas as pd

d1 = {'a':1,'b':2,'c':3}
d2 = {'c':10,'a':20,'b':30}

s1 = pd.Series(data = d1)
s2 = pd.Series(data = d2)

print("加法\n",s1+s2)
print("减法\n",s1-s2)
print("乘法\n",s1*s2)
print("除法\n",s1/s2)
```

```
运行结果
加法
 a    21
b    32
c    13
dtype: int64
减法
 a   -19
b   -28
c    -7
dtype: int64
乘法
 a    20
b    60
c    30
dtype: int64
除法
 a    0.050000
b    0.066667
c    0.300000
dtype: float64

```

$\color{red}{结论：Series间的四则运算是通过索引进行的，对应索引进行运算，如果是Series和数进行运算，那么会对Series内的所有元素做相同操作。}$

#### 0x01 Series 四则运算函数

```python
import pandas as pd

d1 = {'a':1,'b':2,'c':3}
d2 = {'c':10,'a':20,'b':30}

s1 = pd.Series(data = d1)
s2 = pd.Series(data = d2)

print("加法\n",s1.add(s2))
print("减法\n",s1.sub(10))
print("乘法\n",s1.mul(s2))
print("除法\n",s1.div(2))
```

```
运行结果：
加法
 a    21
b    32
c    13
dtype: int64
减法
 a   -9
b   -8
c   -7
dtype: int64
乘法
 a    20
b    60
c    30
dtype: int64
除法
 a    0.5
b    1.0
c    1.5
dtype: float64
```

### 1.3 Series对象的增删改查

#### 0x00 索引方式

##### 通过索引进行索引

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']

s = pd.Series(data = data,index = index)
print(s['a'])
print("=======")
print(s[['a','c','e']])
print("=======")
print(s['a':'d'])
```

```
运行结果：
1
=======
a    1
c    3
e    5
dtype: int64
=======
a    1
b    2
c    3
d    4
dtype: int64
```

注意，**Series的$\color{red}{索引切片}$是左闭右闭的**

##### 通过下标进行索引

**※下标从 0 开始**

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']

s = pd.Series(data = data,index = index)
print(s[0])
print("=======")
print(s[[1,2]])
print("=======")
print(s[0:3])
```

```
运行结果：
1
=======
b    2
c    3
dtype: int64
=======
a    1
b    2
c    3
dtype: int64
```



##### 通过 .loc[] 进行索引

**loc本质上和通过索引进行索引一样，但是只能在loc内写索引**，而且它后面接的是 **中括号 [ ] ** 。

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']

s = pd.Series(data = data,index = index)
print(s.loc['a'])
print("=======")
print(s.loc[['a','c','e']])
print("=======")
print(s.loc['a':'d'])
```

```
运行结果：
1
=======
a    1
c    3
e    5
dtype: int64
=======
a    1
b    2
c    3
d    4
dtype: int64
```

我知道你想不信邪地试试向里写数字下标，下面我给你演示一下：

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']

s = pd.Series(data = data,index = index)
print(s.loc[1])
print("=======")
print(s.loc[[0,2,4]])
print("=======")
print(s.loc[0:4])
```

```
运行结果：
TypeError: cannot do label indexing on <class 'pandas.core.indexes.base.Index'> with these indexers [1] of <class 'int'>
```



##### 通过 .iloc[] 进行索引

同理，它和数字下标索引是等价的，你可以把它理解成 indexlocate[],

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']

s = pd.Series(data = data,index = index)
print(s.iloc[1])
print("=======")
print(s.iloc[[0,2,4]])
print("=======")
print(s.iloc[0:4])
```

```
运行结果：
2
=======
a    1
c    3
e    5
dtype: int64
=======
a    1
b    2
c    3
d    4
dtype: int64
```

当然了，它和 loc[] 相似，它里面不能写字母的索引。这里我就不演示了。但是报错信息可以列举一下

```
TypeError: Cannot index by location index with a non-integer key
```



##### 通过布尔数组进行索引

布尔数组就是形如：

```python
boolean_array = [True,False,False,True,True,False]
```

的数组。



```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']
boolean_array = [True,False,False,True,True,False]

s = pd.Series(data = data,index = index)

print(s[boolean_array])
```

```
运行结果：
a    1
d    4
e    5
dtype: int64

```

当然了，我们一般不会手动声明这个布尔数组，而是通过查询查出来的，比如：

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']
# boolean_array = [True,False,False,True,True,False]

s = pd.Series(data = data,index = index)

print(s[s>4])
```

```
运行结果：
e    5
f    6
dtype: int64

```

##### 通过get()方法进行索引

只需要给get提供key，它就能找出value

![](https://images.gitee.com/uploads/images/2020/0718/104052_f6f38074_5550632.png )

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']
# boolean_array = [True,False,False,True,True,False]

s = pd.Series(data = data,index = index)

print(s.get('a'))
```

```
Result:
1
```

<br>

#### 0x01 修改方式

修改分为两大种，**改值**和**改索引**

##### 值更改

简略而言就是查出来之后直接赋值就行

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']

s = pd.Series(data = data,index = index)

s['a'] = 10
s[1] = 20
s.loc['c'] = 30
s.iloc[3] = 40
print(s)

```

```
Result:
a    10
b    20
c    30
d    40
e     5
f     6
dtype: int64
```

还有一个库函数 replace()可以用

![](https://images.gitee.com/uploads/images/2020/0718/104626_6af7f990_5550632.png)

重要参数有 3 个

> to_replace => 待更换的值(值列表)
>
> value => 更换的值(值列表)
>
> inplace => 是否直接在当前变量内更改

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']

s = pd.Series(data = data,index = index)

s1 = s.replace(to_replace = [1,2,7],value=[10,20,30],inplace=False)
print(s1)
print("=======")
print(s)


```

```
Result:
a    10
b    20
c     3
d     4
e     5
f     6
dtype: int64
=======
a    1
b    2
c    3
d    4
e    5
f    6
dtype: int64
```

当找不到值的时候，默认跳过

##### 索引更改

改索引需要调用库函数 **rename()**

![](https://images.gitee.com/uploads/images/2020/0718/105204_60f0dcca_5550632.png)

index里面写一个字典作为索引更改的映射。

它也有一个inplace代表是否在本对象内更改

```python
import pandas as pd

data = [1,2,3,4,5,6]
index = ['a','b','c','d','e','f']

s = pd.Series(data = data,index = index)

s1 = s.rename(index={'a':'aa'},inplace = False)
print(s1)
print("=======")
print(s)

```

```
Result:
aa    1
b     2
c     3
d     4
e     5
f     6
dtype: int64
=======
a    1
b    2
c    3
d    4
e    5
f    6
dtype: int64
```



#### 0x02 增加方式

##### 通过索引增加

当添加一个不存在的索引时，可以增加一个元素。



```python
import pandas as pd

data = [1,2,4,5]
index = ['a','b','d','e']

s = pd.Series(data = data,index = index)
s['c'] = 3

print(s)

```

```
a    1
b    2
d    4
e    5
c    3
dtype: int64
```



##### 通过append增加

![](https://images.gitee.com/uploads/images/2020/0718/105935_40eaba6b_5550632.png )

重要参数有 2 个：

> to_append => 待追加的Series或list或tuple
>
> ignore_index => False保留原来的索引,True生成默认的数值索引

```python
import pandas as pd

data = [1,2,3]
index = ['a','b','c']

s = pd.Series(data = data,index = index)
s1 = pd.Series(data = [100,200,300],index = ['x','y','z'])
s = s.append(s1,ignore_index=False)
print(s)
```

```
Result:
a      1
b      2
c      3
x    100
y    200
z    300
dtype: int64
```





#### 0x03 删除方式

##### 通过 del 关键字删除

```python
import pandas as pd

data = [1,2,3]
index = ['a','b','c']

s = pd.Series(data = data,index = index)
del s['a']
print(s)
```

```
Result:
b    2
c    3
dtype: int64
```



##### 通过 drop() 删除

![](https://images.gitee.com/uploads/images/2020/0718/110605_eab28213_5550632.png )

重要参数有：

> labels => 索引
>
> inplace => 是否在本对象内删除

```python
import pandas as pd

data = [1,2,3]
index = ['a','b','c']

s = pd.Series(data = data,index = index)
s.drop(labels=['a','b','c'],inplace=True)
print(s)
```

```
Result: 
Series([], dtype: int64)
```

## 1.3 Series对象的相关函数

#### 0x00 重复值和空值操作

unique => 返回一个不重复值的数组

```python
import pandas as pd

data = {'a':1,'b':2,'c':3,'d':5,'f':5,'g':5}
index = ['aa','bb','c','d','f','g']
s = pd.Series(data,index)
res = s.unique()
print(res)
```

```
Result:
[nan  3.  5.]
```

<br>

nunique(dropna = True) => 统计不重复值的个数【默认drop NaN】

```python
import pandas as pd

data = {'a':1,'b':2,'c':3,'d':5,'f':5,'g':5}
index = ['aa','bb','c','d','f','g']
s = pd.Series(data,index)
res = s.nunique(dropna=True)
print(res)
```

```
Result:
2
```

<br>

Series.isnull() <==> pandas.isnull(Series s)

Series.notnull() <==> pandas.notnull(Series s)

```python
import pandas as pd

data = {'a':1,'b':2,'c':3,'d':5,'f':5,'g':5}
index = ['aa','bb','c','d','f','g']
s = pd.Series(data,index)
print(s.isnull())
```

```
Result:
aa     True
bb     True
c     False
d     False
f     False
g     False
dtype: bool
```



```python
import pandas as pd

data = {'a':1,'b':2,'c':3,'d':5,'f':5,'g':5}
index = ['aa','bb','c','d','f','g']
s = pd.Series(data,index)
print(pd.notnull(s))
```

```
Result:
aa    False
bb    False
c      True
d      True
f      True
g      True
dtype: bool
```

<br>

dropna =>删除空值

```python
def dropna(self, axis=0, inplace=False, **kwargs):
    pass
```

```python
import pandas as pd

data = {'a':1,'b':2,'c':3,'d':5,'f':5,'g':5}
index = ['aa','bb','c','d','f','g']
s = pd.Series(data,index)
print(s.dropna())
```

```
Result:
c    3.0
d    5.0
f    5.0
g    5.0
dtype: float64

```

<br>

fillna => 用字符填充空值

```python
    def fillna(
        self,
        value=None,
        method=None,
        axis=None,
        inplace=False,
        limit=None,
        downcast=None,
        **kwargs
    ): pass
```

```python
import pandas as pd

data = {'a':1,'b':2,'c':3,'d':5,'f':5,'g':5}
index = ['aa','bb','c','d','f','g']
s = pd.Series(data,index)
print(s.fillna(0))
```

```
Result:
aa    0.0
bb    0.0
c     3.0
d     5.0
f     5.0
g     5.0
dtype: float64
```

<br>

count() => 计数无NaN的个数

```python
import pandas as pd

data = {'a':1,'b':2,'c':3,'d':5,'f':5,'g':5}
index = ['aa','bb','c','d','f','g']
s = pd.Series(data,index)
print(s.count())
```

```
Result:
4
```

<br>

sort_values() => 值排序，默认升序

sort_index() => 索引排序，字典序

```python
    def sort_values(
        self,
        axis=0,
        ascending=True,
        inplace=False,
        kind="quicksort",
        na_position="last",
    ): pass
```



```python
    def sort_index(
        self,
        axis=0,
        level=None,
        ascending=True,
        inplace=False,
        kind="quicksort",
        na_position="last",
        sort_remaining=True,
    ): pass
```



```python
import pandas as pd

data = {'z':100,'x':123,'a':2,'q':23,'O':22,'o':12,'b':3000,'c':52}
s = pd.Series(data = data)
print(s.sort_values())

```

```
Result:
a       2
o      12
O      22
q      23
c      52
z     100
x     123
b    3000
dtype: int64
```

<br>

```python
import pandas as pd

data = {'z':100,'x':123,'a':2,'q':23,'O':22,'o':12,'b':3000,'c':52}
s = pd.Series(data = data)
print(s.sort_index())

```

```
Result:
O      22
a       2
b    3000
c      52
o      12
q      23
x     123
z     100
dtype: int64
```



#### 0x01 数值统计

和Numpy一样

```
s.max()
s.min()
s.mean()
s.std()
s.var()
s.sum()
...
```



#### 0x02 字符串操作

pandas 中使用 **Series.str **进行字符串操作和Python自带的字符串操作很类似

##### 大小写转换

Series.str.lower()

Series.str.upper()

Series.str.captitalize()

Series.str.swapcase()

<br>

lower()

```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])

print(a.str.lower())
```

```
Result:
0         apple
1          pear
2         peach
3    blue barry
dtype: object
```

<br>

upper()

```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])

print(a.str.upper())
```

```
Result:
0         APPLE
1          PEAR
2         PEACH
3    BLUE BARRY
dtype: object
```

<br>

captitalize()

```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])

print(a.str.capitalize())
```

```
Result:
0         Apple
1          Pear
2         Peach
3    Blue barry
dtype: object
```

<br>

swapcase()

```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])

print(a.str.swapcase())
```

```
Result:
0         APPLE
1          pear
2         pEACH
3    BLUE BARRY
dtype: object
```

<br>



##### 字符串拼接

Series.str.cat()

注意：同一维度的Series才能进行拼接,可以指定拼接的分隔符,否则报这个错：

```
ValueError: All arrays must be same length, except those having an index if `join` is not None
```



```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])

print(a.str.cat(b,sep=','))
```

```
Result:
0           apple,carrot
1           PEAR,cabbage
2            Peach,lemon
3    blue barry,mushroom
dtype: object

```

<br>

字符间拼接符号

Series.str.join()



```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])

print(a.str.join("?"))
```

```
Result:
0              a?p?p?l?e
1                P?E?A?R
2              P?e?a?c?h
3    b?l?u?e? ?b?a?r?r?y
dtype: object


```

<br>

##### 字符串内容判断

contains()

startswith()

endswith()

...

startswith()

```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])

print(a.str.startswith("a"))
```

```
Result:
0     True
1    False
2    False
3    False
dtype: bool


```

<br>

endswith()

```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])
s = a.append(b)
print(s.str.endswith("e"))
```

```
Result:
0     True
1    False
2    False
3    False
0    False
1     True
2    False
3    False
dtype: bool


```

<br>

contains()

regex 用来指定是否使用正则表达式

```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])
s = a.append(b)
print(s.str.contains('ca',regex=False))
```

```
Result:
0    False
1    False
2    False
3    False
0     True
1     True
2    False
3    False
dtype: bool


```

<br>

还有类似：

```
isupper()
isdigit()
isdecimal()
...
```

等等Python自带的字符串内容判断函数在此就不列举了

##### 字符串提取

Series.str.extract()

通过正则表达式提取。

注意写正则表达式的时候要在最外层套上括号,否则会报：

```
ValueError: pattern contains no capture groups
```



```python
import pandas as pd

a = pd.Series(['apple','PEAR','Peach','blue barry'])
b = pd.Series(['carrot','cabbage','lemon','mushroom'])
s = a.append(b)
print(s.str.extract(r'(^P[a-z].*)',expand=False))
```

```
Result:
0      NaN
1      NaN
2    Peach
3      NaN
0      NaN
1      NaN
2      NaN
3      NaN
dtype: object
```



## Part 2 DataFrame 

DataFrame对象本质上是**拥有相同索引的Series按列排列构成的，加上列索引的二维表**

它的竖列叫做**columns**，横行和Series一样叫索引**index**。通过使用columns和index可以进行确定元素位置。

### 2.1 创建DataFrame对象

#### 0x00 空对象

```python
import pandas as pd

df = pd.DataFrame()
print(type(df))
print(df)
```

```
Result:
<class 'pandas.core.frame.DataFrame'>
Empty DataFrame
Columns: []
Index: []
```

<br>

#### 0x01 data无行索引，无列索引

```
import pandas as pd

data = [[1,2,3,4],
        [5,6,7,8]]
df = pd.DataFrame(data = data)
print(df)
```

```
Result:
   0  1  2  3
0  1  2  3  4
1  5  6  7  8
```

**不指定行索引或列索引pandas还是会自动生成整数索引**

<br>

#### 0x02 DataFrame 属性

```python
import pandas as pd

data = {
    'Fruit':{'price':18,'number':50},
    'Vegetable':{'price':12,'number':30},
    'Meat':{'price':200,'number':20}
}
df = pd.DataFrame(data = data)
print("=====查看列索引=====")
print(df.columns)
print("=====查看行索引=====")
print(df.index)
print("=====查看值=====")
print(df.values)
print("=====查看数据类型=====")
print(df.dtypes)
print("=====查看所有索引=====")
print(df.axes)
print("=====查看DataFrame形状=====")
print(df.shape)
print("=====查看元素个数=====")
print(df.size)
```

```
Result:
=====查看列索引=====
Index(['Fruit', 'Vegetable', 'Meat'], dtype='object')
=====查看行索引=====
Index(['price', 'number'], dtype='object')
=====查看值=====
[[ 18  12 200]
 [ 50  30  20]]
=====查看数据类型=====
Fruit        int64
Vegetable    int64
Meat         int64
dtype: object
=====查看所有索引=====
[Index(['price', 'number'], dtype='object'), Index(['Fruit', 'Vegetable', 'Meat'], dtype='object')]
=====查看DataFrame形状=====
(2, 3)
=====查看元素个数=====
6
```

<br>

#### 0x03 data无行索引，有列索引

```python
import pandas as pd
data2 = {'A':[1,4],'B':[2,5],'C':[3,6]}
index2 = ['a','b']
columns2=['A','B','D']
df = pd.DataFrame(data = data2)
print(df)
```

```
Result:
   A  B  C
0  1  2  3
1  4  5  6
```

形式参数index还是指行索引，不传就使用默认的数字索引

<br>

#### 0x04 data 有行索引，无列索引

```python
import pandas as pd
data2 = {'A':[1,4],'B':[2,5],'C':[3,6]}
index2 = ['a','b']
columns2=['A','B','D']
df = pd.DataFrame(data = data2,index = index2,columns=columns2)
print(df)
```

```
Result:
   A  B    D
a  1  2  NaN
b  4  5  NaN
```

随意指定已存在的columns就会产生空值

<br>

#### 0x05 data有行索引，有列索引

```python
import pandas as pd

data = {
    'Fruit':{'price':18,'number':50},
    'Vegetable':{'price':12,'number':30},
    'Meat':{'price':200,'number':20}
}
df = pd.DataFrame(data = data)
print(df)


```

```
Result:
        Fruit  Vegetable  Meat
price      18         12   200
number     50         30    20
```

同时指定行索引index和列索引columns，当然像我这样把数据直接组织成行列有结构的不用指定也行。

### 2.2 pandas时间序列

#### 0x00 pd.date_range() 创建一个时间序列

```python
import pandas as pd

dates = pd.date_range('2020/01/23',periods=5)
print(dates)
```

```
Result:
DatetimeIndex(['2020-01-23', '2020-01-24', '2020-01-25', '2020-01-26',
               '2020-01-27'],
              dtype='datetime64[ns]', freq='D')
```

> DataFrame中时间默认用 “-” 分割

> periods是周期，freq 是单位频率[秒，天，月，年...]

```python
import pandas as pd

date_rng = pd.date_range(start='01/01/2020',end='09-01-2020',freq='H') #最好将日期格式统一，这里是为了方便演示
print(date_rng)
```

```
DatetimeIndex(['2020-01-01 00:00:00', '2020-01-01 01:00:00',
               '2020-01-01 02:00:00', '2020-01-01 03:00:00',
               '2020-01-01 04:00:00', '2020-01-01 05:00:00',
               '2020-01-01 06:00:00', '2020-01-01 07:00:00',
               '2020-01-01 08:00:00', '2020-01-01 09:00:00',
               ...
               '2020-08-31 15:00:00', '2020-08-31 16:00:00',
               '2020-08-31 17:00:00', '2020-08-31 18:00:00',
               '2020-08-31 19:00:00', '2020-08-31 20:00:00',
               '2020-08-31 21:00:00', '2020-08-31 22:00:00',
               '2020-08-31 23:00:00', '2020-09-01 00:00:00'],
              dtype='datetime64[ns]', length=5857, freq='H')


```

时间序列能干啥？它能用于生成时间行索引

```python
import pandas as pd
import numpy as np
date_rng = pd.date_range(start='2020-07-20',end='2020-08-15',freq='D')
data = np.random.randint(0,1000,size=len(date_rng))
df = pd.DataFrame(data = data,index = date_rng,columns=['Money'])
print(df)
```

```
Result:
            Money
2020-07-20    246
2020-07-21    530
2020-07-22    586
2020-07-23    356
2020-07-24    903
2020-07-25    952
2020-07-26    595
2020-07-27    363
2020-07-28    566
2020-07-29    329
2020-07-30    863
2020-07-31    493
2020-08-01    459
2020-08-02    389
2020-08-03    472
2020-08-04    136
2020-08-05    272
2020-08-06    318
2020-08-07    862
2020-08-08    673
2020-08-09    232
2020-08-10    320
2020-08-11    765
2020-08-12    756
2020-08-13     37
2020-08-14    360
2020-08-15    911

```

#### 0x01 to_datetime() 字符串转时间格式

```python
def to_datetime(
    arg,
    errors="raise",
    dayfirst=False,
    yearfirst=False,
    utc=None,
    box=True,
    format=None,
    exact=True,
    unit=None,
    infer_datetime_format=False,
    origin="unix",
    cache=True,
):pass
```



```python
import pandas as pd

s = pd.Series(data = ['2020-06-24','2019-05-08','2020/07/02','2018/02/02'])
s1 = pd.to_datetime(s)
print(s1)
```

```
Result:
0   2020-06-24
1   2019-05-08
2   2020-07-02
3   2018-02-02
dtype: datetime64[ns]
```



### 2.3 CSV文件和pandas

csv文件想必大家都知道，这一节我们要做的事情就是进行csv文件和pandas的DataFrame数据类型之间的转换。

#### 0x00 pd.read_csv()

函数参数原型:

```python
def _make_parser_function(name, default_sep=","):
    def parser_f(
        filepath_or_buffer: FilePathOrBuffer,
        sep=default_sep,
        delimiter=None,
        # Column and Index Locations and Names
        header="infer",
        names=None,
        index_col=None,
        usecols=None,
        squeeze=False,
        prefix=None,
        mangle_dupe_cols=True,
        # General Parsing Configuration
        dtype=None,
        engine=None,
        converters=None,
        true_values=None,
        false_values=None,
        skipinitialspace=False,
        skiprows=None,
        skipfooter=0,
        nrows=None,
        # NA and Missing Data Handling
        na_values=None,
        keep_default_na=True,
        na_filter=True,
        verbose=False,
        skip_blank_lines=True,
        # Datetime Handling
        parse_dates=False,
        infer_datetime_format=False,
        keep_date_col=False,
        date_parser=None,
        dayfirst=False,
        cache_dates=True,
        # Iteration
        iterator=False,
        chunksize=None,
        # Quoting, Compression, and File Format
        compression="infer",
        thousands=None,
        decimal=b".",
        lineterminator=None,
        quotechar='"',
        quoting=csv.QUOTE_MINIMAL,
        doublequote=True,
        escapechar=None,
        comment=None,
        encoding=None,
        dialect=None,
        # Error Handling
        error_bad_lines=True,
        warn_bad_lines=True,
        # Internal
        delim_whitespace=False,
        low_memory=_c_parser_defaults["low_memory"],
        memory_map=False,
        float_precision=None,
    ):pass

```

参数多吧，吓人吧，我们挑几个重要的讲：

> filepath: 文件路径
>
> sep: 类型str 指定分隔符
>
> delimeter: 和sep一样默认参数是None，而不是英文逗号
>
> header：整数值指定DataFrame的columns的名称在哪一行
>
> encoding：默认None 指定字符编码

```python
import pandas as pd

FILE_PATH = r"Book-URL.csv"

df = pd.read_csv(FILE_PATH,sep=',',encoding='UTF-8')
print(df)
```

```
Result:
                                               Book-Title                                        Image-URL-L
0                                     Classical Mythology  http://images.amazon.com/images/P/0195153448.0...
1                                            Clara Callan  http://images.amazon.com/images/P/0002005018.0...
2                                    Decision in Normandy  http://images.amazon.com/images/P/0060973129.0...
3       Flu: The Story of the Great Influenza Pandemic...  http://images.amazon.com/images/P/0374157065.0...
4                                  The Mummies of Urumchi  http://images.amazon.com/images/P/0393045218.0...
...                                                   ...                                                ...
271374                         There's a Bat in Bunk Five  http://images.amazon.com/images/P/0440400988.0...
271375                            From One to One Hundred  http://images.amazon.com/images/P/0525447644.0...
271376  Lily Dale : The True Story of the Town that Ta...  http://images.amazon.com/images/P/006008667X.0...
271377                        Republic (World's Classics)  http://images.amazon.com/images/P/0192126040.0...
271378  A Guided Tour of Rene Descartes' Meditations o...  http://images.amazon.com/images/P/0767409752.0...

[271379 rows x 2 columns]

```

指定header，即，从哪一行开始，默认是0

```python
import pandas as pd

FILE_PATH = r"Book-URL.csv"

df = pd.read_csv(FILE_PATH,sep=',',encoding='UTF-8',header=271377)
print(df)
```

```
  Lily Dale : The True Story of the Town that Talks to the Dead http://images.amazon.com/images/P/006008667X.01.LZZZZZZZ.jpg
0                        Republic (World's Classics)             http://images.amazon.com/images/P/0192126040.0...          
1  A Guided Tour of Rene Descartes' Meditations o...             http://images.amazon.com/images/P/0767409752.0...          

```

skiprows，忽略的行数

```python
import pandas as pd

FILE_PATH = r"Book-URL.csv"

df = pd.read_csv(FILE_PATH,sep=',',encoding='UTF-8',skiprows=lambda x:x&1 ==0)
print(df)
```

```
D:\Python37\python.exe D:/ProgramLearning/Python/DataSetHandle/AutoDealDataSet/学习相关模块/learn_pandas.py
                                      Classical Mythology http://images.amazon.com/images/P/0195153448.01.LZZZZZZZ.jpg
0                                    Decision in Normandy  http://images.amazon.com/images/P/0060973129.0...          
1                                  The Mummies of Urumchi  http://images.amazon.com/images/P/0393045218.0...          
2       What If?: The World's Foremost Military Histor...  http://images.amazon.com/images/P/0425176428.0...          
3       Under the Black Flag: The Romance and the Real...  http://images.amazon.com/images/P/0679425608.0...          
4                             Nights Below Station Street  http://images.amazon.com/images/P/0771074670.0...          
...                                                   ...                                                ...          
135684  Tropical Rainforests: 230 Species in Full Colo...  http://images.amazon.com/images/P/1582380805.0...          
135685                                  Anti Death League  http://images.amazon.com/images/P/014002803X.0...          
135686                         There's a Bat in Bunk Five  http://images.amazon.com/images/P/0440400988.0...          
135687  Lily Dale : The True Story of the Town that Ta...  http://images.amazon.com/images/P/006008667X.0...          
135688  A Guided Tour of Rene Descartes' Meditations o...  http://images.amazon.com/images/P/0767409752.0...          

[135689 rows x 2 columns]

```

跳过**原来所有偶数索引（新索引依旧是从0开始的自动生成索引）**，记录个数比原来的减半

#### 0x01 查看整体属性

Series 对象

> Series.index
>
> Series.name
>
> Series.values
>
> Series.dtype

DataFrame对象

> DataFrame.index
>
> DataFrame.columns
>
> DataFrame.values
>
> DataFrame.dtypes

其它属性

> .ndim : 查看维数
>
> .shape ： 查看形状
>
> .size：元素个数

```python
import pandas as pd

FILE_PATH = r"Book-URL.csv"

df = pd.read_csv(FILE_PATH,sep=',',encoding='UTF-8',skiprows=lambda x:x&1 ==0)
print("=====.ndim : 查看维数=====")
print(df.ndim)
print("=====.shape ： 查看形状=====")
print(df.shape)
print("=====.size：元素个数=====")
print(df.size)

```

```
Result:
=====.ndim : 查看维数=====
2
=====.shape ： 查看形状=====
(135689, 2)
=====.size：元素个数=====
271378
```

当然了还有一个省事的函数 DataFrame.info()

```python
import pandas as pd

FILE_PATH = r"Book-URL.csv"

df = pd.read_csv(FILE_PATH,sep=',',encoding='UTF-8',skiprows=lambda x:x&1 ==0)
print(df.info())

```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 135689 entries, 0 to 135688
Data columns (total 2 columns):
Classical Mythology                                             135689 non-null object
http://images.amazon.com/images/P/0195153448.01.LZZZZZZZ.jpg    135687 non-null object
dtypes: object(2)
memory usage: 2.1+ MB
None

```

查看x行，后x行的记录

DataFrame.head()

DataFrame.tail()

```python
import pandas as pd

FILE_PATH = r"Book-URL.csv"

df = pd.read_csv(FILE_PATH,sep=',',encoding='UTF-8',skiprows=lambda x:x&1 ==0)
print(df.head(5))

```

```
                                 Classical Mythology http://images.amazon.com/images/P/0195153448.01.LZZZZZZZ.jpg
0                               Decision in Normandy  http://images.amazon.com/images/P/0060973129.0...          
1                             The Mummies of Urumchi  http://images.amazon.com/images/P/0393045218.0...          
2  What If?: The World's Foremost Military Histor...  http://images.amazon.com/images/P/0425176428.0...          
3  Under the Black Flag: The Romance and the Real...  http://images.amazon.com/images/P/0679425608.0...          
4                        Nights Below Station Street  http://images.amazon.com/images/P/0771074670.0...  
```

tail :

```python
import pandas as pd

FILE_PATH = r"Book-URL.csv"

df = pd.read_csv(FILE_PATH,sep=',',encoding='UTF-8',skiprows=lambda x:x&1 ==0)
print(df.tail(5))

```

```
                                      Classical Mythology http://images.amazon.com/images/P/0195153448.01.LZZZZZZZ.jpg
135684  Tropical Rainforests: 230 Species in Full Colo...  http://images.amazon.com/images/P/1582380805.0...          
135685                                  Anti Death League  http://images.amazon.com/images/P/014002803X.0...          
135686                         There's a Bat in Bunk Five  http://images.amazon.com/images/P/0440400988.0...          
135687  Lily Dale : The True Story of the Town that Ta...  http://images.amazon.com/images/P/006008667X.0...          
135688  A Guided Tour of Rene Descartes' Meditations o...  http://images.amazon.com/images/P/0767409752.0...    
```

随机抽样 .sample()

```python
import pandas as pd

FILE_PATH = r"Book-URL.csv"

df = pd.read_csv(FILE_PATH,sep=',',encoding='UTF-8',skiprows=lambda x:x&1 ==0)
print(df.sample(5))


```

```
                                      Classical Mythology http://images.amazon.com/images/P/0195153448.01.LZZZZZZZ.jpg
40964                                     Frugal Luxuries  http://images.amazon.com/images/P/1568654928.0...          
92500                                     Shadow Marriage  http://images.amazon.com/images/P/0373107064.0...          
11982                                 The Girl in the Box  http://images.amazon.com/images/P/0553282611.0...          
101829  The Silent War: The Cold War Battle Beneath th...  http://images.amazon.com/images/P/0684872137.0...          
113936                                 Im Strom der Zeit.  http://images.amazon.com/images/P/3404141652.0...          

Process finished with exit code 0

```

统计信息 .describe()

默认排除NaN

```python
import pandas as pd

FILE_PATH = r"Book-URL.csv"

df = pd.read_csv(FILE_PATH,sep=',',encoding='UTF-8',skiprows=lambda x:x&1 ==0)
print(df.describe())


```

```
       Classical Mythology http://images.amazon.com/images/P/0195153448.01.LZZZZZZZ.jpg
count               135689                                             135687          
unique              126850                                             135621          
top           Little Women  http://images.amazon.com/images/P/157912061X.0...          
freq                    13                                                  2          

Process finished with exit code 0
```

#### 0x02 pd.to_csv()

把一个DataFrame类型写成.csv文件

```python
import pandas as pd

data = {
    "A":{'a':1,'b':2},
    "B":{'a':11,'b':22},
    "C":{'a':111,'b':222}
}

df = pd.DataFrame(data = data)
df.to_csv("test.csv",index=False,sep=',')

```

![输入图片说明](https://images.gitee.com/uploads/images/2020/0720/162306_50e81e6f_5550632.png "屏幕截图.png")

#### 0x03 pd.read_excel()

```python
def read_excel(
    io,
    sheet_name=0,
    header=0,
    names=None,
    index_col=None,
    usecols=None,
    squeeze=False,
    dtype=None,
    engine=None,
    converters=None,
    true_values=None,
    false_values=None,
    skiprows=None,
    nrows=None,
    na_values=None,
    keep_default_na=True,
    verbose=False,
    parse_dates=False,
    date_parser=None,
    thousands=None,
    comment=None,
    skip_footer=0,
    skipfooter=0,
    convert_float=True,
    mangle_dupe_cols=True,
    **kwds
):pass
```

```python
import pandas as pd
file_path = r"001.xlsx"
df = pd.read_excel(file_path)
print(df)

```

```
     id name  grade
0  1111   zs     34
1  2222   df     23
2  3333   gf     12

```

[更多详情请点击这里](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html#pandas.read_excel)

### 2.4 DataFrame对象的增删改查

#### 0x00 索引

DataFrame是一个二维表，所以它肯定会有行列两种方式的索引。

##### 快速查看

为4种，行2种，列两种

先是列的两种

```python
import pandas as pd
data = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
index = ['a','b','c','d']
columns = ['A','B','C','D']
df = pd.DataFrame(data = data,index=index,columns=columns)
print(df['A'])
print(df.A)
print(df[['A','C','D']])

```

```
a     1
b     5
c     9
d    13
Name: A, dtype: int64
a     1
b     5
c     9
d    13
Name: A, dtype: int64
    A   C   D
a   1   3   4
b   5   7   8
c   9  11  12
d  13  15  16

Process finished with exit code 0

```

行的两种，注意，**DataFrame不支持单行的行索引和行下标访问法**，想访问行可以通过切片

```python
import pandas as pd
data = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
index = ['a','b','c','d']
columns = ['A','B','C','D']
df = pd.DataFrame(data = data,index=index,columns=columns)

print(df[0:1])#左闭右开
print("===============")
print(df['a':'b'])#左闭右闭



```

```
   A  B  C  D
a  1  2  3  4
===============
   A  B  C  D
a  1  2  3  4
b  5  6  7  8
```

##### .loc[] 方式

由于DataFrame是二维的，我们loc的方式也就和原先不同了，原来Series可以通过切片，列表，单一值三种方式使用loc，现在还有一个列也就意味着有着至少9种的排列组合方式

```python
import pandas as pd
data = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
index = ['a','b','c','d']
columns = ['A','B','C','D']
df = pd.DataFrame(data = data,index=index,columns=columns)

print(df.loc['a','A'])
print("==================")
print(df.loc[['a','b'],'A'])
print("==================")
print(df.loc['a':'c','A'])


```

```
1
==================
a    1
b    5
Name: A, dtype: int64
==================
a    1
b    5
c    9
Name: A, dtype: int64
```

同样loc内只能写索引，不能写下标。

#####  .iloc[] 方式

```python
import pandas as pd
data = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
index = ['a','b','c','d']
columns = ['A','B','C','D']
df = pd.DataFrame(data = data,index=index,columns=columns)

print(df.iloc[0,0])
print("==================")
print(df.iloc[[0,2],0])
print("==================")
print(df.iloc[0:,2])


```

```
1
==================
a    1
c    9
Name: A, dtype: int64
==================
a     3
b     7
c    11
d    15
Name: C, dtype: int64

Process finished with exit code 0

```

##### 0x01 改值

第一种就是选出来改，第二种还是replace方法。

```python
import pandas as pd
data = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
index = ['a','b','c','d']
columns = ['A','B','C','D']
df = pd.DataFrame(data = data,index=index,columns=columns)

print(df)
print("=========更改后=========")
df.loc['a','A'] = 100
df.replace(to_replace=[5,9,13],value=[500,900,1300],inplace=True)
print(df)

```

```
    A   B   C   D
a   1   2   3   4
b   5   6   7   8
c   9  10  11  12
d  13  14  15  16
=========更改后=========
      A   B   C   D
a   100   2   3   4
b   500   6   7   8
c   900  10  11  12
d  1300  14  15  16

Process finished with exit code 0

```

##### 0x02 改索引

直接改和用函数rename改

```python
import pandas as pd
data = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
index = ['a','b','c','d']
columns = ['A','B','C','D']
df = pd.DataFrame(data = data,index=index,columns=columns)

df1 = df.copy()
df1.index = ['x','y','z','alpha']
df1.columns = ['AA','BB','CC','DD']
print(df1)

```

```
       AA  BB  CC  DD
x       1   2   3   4
y       5   6   7   8
z       9  10  11  12
alpha  13  14  15  16

```

rename修改法:

```python
import pandas as pd
data = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
index = ['a','b','c','d']
columns = ['A','B','C','D']
df = pd.DataFrame(data = data,index=index,columns=columns)

df1 = df.copy()
df1.rename(index = {'a':'x','b':'y'},columns={'A':'AA','B':'BB'},inplace = True)
print(df1)

```

```
   AA  BB   C   D
x   1   2   3   4
y   5   6   7   8
c   9  10  11  12
d  13  14  15  16
```

##### 0x03 新增行列

之前新增行有一个Pandas.concat()的函数还有一个未知索引直接添加法

我们来一一实验：

```python
import pandas as pd
data = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
index = ['a','b','c','d']
columns = ['A','B','C','D']
df = pd.DataFrame(data = data,index=index,columns=columns)

df.loc['e'] = [17,18,19,20]

df1 = pd.DataFrame(data=[[111,222,333,444],[555,666,777,888]],index=['f','g'],columns = columns)
df2 = pd.concat([df,df1],axis=0)

print(df2)
```

```
     A    B    C    D
a    1    2    3    4
b    5    6    7    8
c    9   10   11   12
d   13   14   15   16
e   17   18   19   20
f  111  222  333  444
g  555  666  777  888
```

$\color{red}{注意，在使用concat方法时要指明维度axis我们是行的批量添加，所以axis=0}$

新增列

同理，可以直接指定未知列标，或者concat中参数改为axis=1

```python
import pandas as pd
data = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
index = ['a','b','c','d']
columns = ['A','B','C','D']
df = pd.DataFrame(data = data,index=index,columns=columns)

df['E'] = [11,22,33,44]

df1 = pd.DataFrame(data=[[111,222],[333,444],[555,666],[777,888]],index=['a','b','c','d'],columns = ['F','G'])
df2 = pd.concat([df,df1],axis=1)

print(df2)
```

```
    A   B   C   D   E    F    G
a   1   2   3   4  11  111  222
b   5   6   7   8  22  333  444
c   9  10  11  12  33  555  666
d  13  14  15  16  44  777  888
```



##### 0x03 删除行列

同理，由del关键字删的方法，也有drop方法删的方法

```python
import pandas as pd
data = [[1,2,3,4,11],[5,6,7,8,22],[9,10,11,12,33],[13,14,15,16,44]]
index = ['a','b','c','d']
columns = ['A','B','C','D','E']
df = pd.DataFrame(data = data,index=index,columns=columns)

print(df)
print("========删除列后=======")
del df['A']

df.drop(['B','C','D'],axis=1,inplace=True)
print(df)

```

```
    A   B   C   D   E
a   1   2   3   4  11
b   5   6   7   8  22
c   9  10  11  12  33
d  13  14  15  16  44
========删除列后=======
    E
a  11
b  22
c  33
d  44

Process finished with exit code 0

```



## Part 3 使用 Pandas 进行数据清洗

数据清洗是指通过纠正数据文件中的错误的最后一道程序，包括检查数据一致性，处理异常值，处理缺失值，光滑噪声和去重等。

### 0x00 介绍各个操作内容

一致性检查：根据变量的合理取值范围和相互作用，检查数据是否合乎要求，发现数值上，范围上，逻辑上不合理甚至矛盾的数据

缺失值的处理方式:

> 1. 删除数据
> 2. 数据补全，人工填充，全局常量填充，统计量填充，回归，建模填充

异常值处理：

> 检测异常点
>
> > 1. 简单统计分析
> > 2. 3alpha原则
> > 3. 箱型图统计
>
> 删除异常值
>
> 不处理
>
> 统计量替换
>
> 视为缺失值

噪声处理

噪声是被测变量的随机误差或方差，观测值 = 真实值 + 噪声。

离群点属于观测值

我们数据清洗的主要对象是

残缺数据：信息缺失

噪声数据：值有误差

错误数据：由于系统不健全导致后台数据有问题，例如出现21位的中国手机号

#### 0x01 缺失值处理

##### 相关函数

df.dropna() 删除

df.fillna() 填充

df.isnull() 判断缺失值

df.notnull()

df.isna() 判断缺失值

df.notna()

```python
import pandas as pd
import numpy as np

data = {
    'A':[12,34,33,55,65],
    'B':[12,43,55,np.nan,np.nan],
    'C':[12,34,554,79,98],
    'D':[23,np.nan,555,np.nan,np.nan]
}

df = pd.DataFrame(data)
print(df)

```

```
    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    NaN
2  33  55.0  554  555.0
3  55   NaN   79    NaN
4  65   NaN   98    NaN
```

```python
import pandas as pd
import numpy as np

data = {
    'A':[12,34,33,55,65],
    'B':[12,43,55,np.nan,np.nan],
    'C':[12,34,554,79,98],
    'D':[23,np.nan,555,np.nan,np.nan]
}

df = pd.DataFrame(data)
print(df.isna())
print("===================")
print(df.isnull())
print("===================")
print(df['A'].isna())

```

```
       A      B      C      D
0  False  False  False  False
1  False  False  False   True
2  False  False  False  False
3  False   True  False   True
4  False   True  False   True
===================
       A      B      C      D
0  False  False  False  False
1  False  False  False   True
2  False  False  False  False
3  False   True  False   True
4  False   True  False   True
===================
0    False
1    False
2    False
3    False
4    False
Name: A, dtype: bool
```

##### 删除空值

```python
def dropna(self, axis=0, how="any", thresh=None, subset=None, inplace=False):
```

axis：指定维度，0是index行，1是columns列，how指定方式，any是只要有空全部删掉，all是全空才删掉

按行删

```python
import pandas as pd
import numpy as np

data = {
    'A':[12,34,33,55,65],
    'B':[12,43,55,np.nan,np.nan],
    'C':[12,34,554,79,98],
    'D':[23,np.nan,555,np.nan,np.nan]
}

df = pd.DataFrame(data)
print(df)
print("==========删除后===========")
df.dropna(axis=0,how="any",inplace=True)
print(df)

```

```
    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    NaN
2  33  55.0  554  555.0
3  55   NaN   79    NaN
4  65   NaN   98    NaN
==========删除后===========
    A     B    C      D
0  12  12.0   12   23.0
2  33  55.0  554  555.0
```

按列删

```python
import pandas as pd
import numpy as np

data = {
    'A':[12,34,33,55,65],
    'B':[12,43,55,np.nan,np.nan],
    'C':[12,34,554,79,98],
    'D':[23,np.nan,555,np.nan,np.nan]
}

df = pd.DataFrame(data)
print(df)
print("==========删除后===========")
df.dropna(axis=1,how="any",inplace=True)
print(df)

```

```
0  12  12.0   12   23.0
1  34  43.0   34    NaN
2  33  55.0  554  555.0
3  55   NaN   79    NaN
4  65   NaN   98    NaN
==========删除后===========
    A    C
0  12   12
1  34   34
2  33  554
3  55   79
4  65   98
```

再测试一个 all 模式

```python
import pandas as pd
import numpy as np

data = {
    'A':[12,34,33,55,65],
    'B':[12,43,55,np.nan,np.nan],
    'C':[12,34,554,79,98],
    'D':[23,np.nan,555,np.nan,np.nan]
}

df = pd.DataFrame(data)
print(df)
print("==========删除后===========")
df.dropna(axis=0,how="all",inplace=True)
print(df)

```

```
    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    NaN
2  33  55.0  554  555.0
3  55   NaN   79    NaN
4  65   NaN   98    NaN
==========删除后===========
    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    NaN
2  33  55.0  554  555.0
3  55   NaN   79    NaN
4  65   NaN   98    NaN

Process finished with exit code 0

```



##### 替换空值

```python
def fillna(
        self,
        value=None,
        method=None,
        axis=None,
        inplace=False,
        limit=None,
        downcast=None,
        **kwargs
    ):pass
```

value:替换值

axis：确定维度

method：

> 1. ffill :用前面一个值代替缺失值，当axis = 0时。backfill/bfill用后面的值代替前面的值。注意它不能和value连用。

limit：填充的个数

```python
import pandas as pd
import numpy as np

data = {
    'A':[12,34,33,55,65],
    'B':[12,43,55,np.nan,np.nan],
    'C':[12,34,554,79,98],
    'D':[23,np.nan,555,np.nan,np.nan]
}

df = pd.DataFrame(data)
print(df)
print("==========填充后===========")
df.fillna(value=0,inplace=True)
print(df)

```

```

    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    NaN
2  33  55.0  554  555.0
3  55   NaN   79    NaN
4  65   NaN   98    NaN
==========填充后===========
    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    0.0
2  33  55.0  554  555.0
3  55   0.0   79    0.0
4  65   0.0   98    0.0

Process finished with exit code 0

```

```python
import pandas as pd
import numpy as np

data = {
    'A':[12,34,33,55,65],
    'B':[12,43,55,np.nan,np.nan],
    'C':[12,34,554,79,98],
    'D':[23,np.nan,555,np.nan,np.nan]
}

df = pd.DataFrame(data)
print(df)
print("==========填充后===========")
df.fillna(value=0,limit=2,inplace=True)
print(df)

```

```

    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    NaN
2  33  55.0  554  555.0
3  55   NaN   79    NaN
4  65   NaN   98    NaN
==========填充后===========
    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    0.0
2  33  55.0  554  555.0
3  55   0.0   79    0.0
4  65   0.0   98    NaN

Process finished with exit code 0

```

```python
import pandas as pd
import numpy as np

data = {
    'A':[12,34,33,55,65],
    'B':[12,43,55,np.nan,np.nan],
    'C':[12,34,554,79,98],
    'D':[23,np.nan,555,np.nan,np.nan]
}

df = pd.DataFrame(data)
print(df)
print("==========填充后===========")
df.fillna(axis=0,method="ffill",inplace=True)
print(df)

```

```

    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    NaN
2  33  55.0  554  555.0
3  55   NaN   79    NaN
4  65   NaN   98    NaN
==========填充后===========
    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34   23.0
2  33  55.0  554  555.0
3  55  55.0   79  555.0
4  65  55.0   98  555.0

Process finished with exit code 0

```

当然咱们可以用方差，平均数之类的来填

```python
import pandas as pd
import numpy as np

data = {
    'A':[12,34,33,55,65],
    'B':[12,43,55,np.nan,np.nan],
    'C':[12,34,554,79,98],
    'D':[23,np.nan,555,np.nan,np.nan]
}

df = pd.DataFrame(data)
print(df)
print("==========填充后===========")
df.fillna(value=df.mean(),inplace=True)
print(df)

```

```
    A     B    C      D
0  12  12.0   12   23.0
1  34  43.0   34    NaN
2  33  55.0  554  555.0
3  55   NaN   79    NaN
4  65   NaN   98    NaN
==========填充后===========
    A          B    C      D
0  12  12.000000   12   23.0
1  34  43.000000   34  289.0
2  33  55.000000  554  555.0
3  55  36.666667   79  289.0
4  65  36.666667   98  289.0
```

##### 重复值处理

两个函数

```python
def duplicated(self, subset=None, keep="first"):
```

```python
def drop_duplicates(self, subset=None, keep="first", inplace=False):
```

subset:指定列，默认是所有列

keep：保留第一个，可选的关键字还有“last”，False

```python
import pandas as pd
import numpy as np

data = [
    ['a',3],
    ['b',4],
    ['a',3],
    ['c',5]
]
columns = ['col1','col2']
df = pd.DataFrame(data,columns=columns)
print(df)
print("==========")
print(df.duplicated())



```

```
  col1  col2
0    a     3
1    b     4
2    a     3
3    c     5
==========
0    False
1    False
2     True
3    False
dtype: bool
```

```python
import pandas as pd
import numpy as np

data = [
    ['a',3],
    ['b',4],
    ['a',3],
    ['c',5]
]
columns = ['col1','col2']
df = pd.DataFrame(data,columns=columns)
print(df)
print("==========")
df.drop_duplicates(inplace= True)
print("==========")
print(df)



```

```
  col1  col2
0    a     3
1    b     4
2    a     3
3    c     5
==========
==========
  col1  col2
0    a     3
1    b     4
3    c     5
```

##### 数据类型转换

实验用的数据集大概内容如下:

![输入图片说明](https://images.gitee.com/uploads/images/2020/0723/113704_27f86aa5_5550632.png "屏幕截图.png")

```
   User-ID        ISBN  Book-Rating
0   276726  0155061224          5.0
1   276729  052165615X          3.0
2   276729  0521795028          6.0
3   276736  3257224281          8.0
4   276737  0600570967          6.0
5   276744  038550120X          7.0
6   276745   342310538         10.0
7   276747  0060517794          9.0
8   276747  0671537458          9.0
9   276747  0679776818          8.0
```

两种查看全局信息的方式：

```python
print(df.dtypes)
```

```
User-ID          int64
ISBN            object
Book-Rating    float64
dtype: object
```

```python
print(df.info())
```

```
User-ID          int64
ISBN            object
Book-Rating    float64
dtype: object
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 433664 entries, 0 to 433663
Data columns (total 3 columns):
User-ID        433664 non-null int64
ISBN           433664 non-null object
Book-Rating    433664 non-null float64
dtypes: float64(1), int64(1), object(1)
memory usage: 9.9+ MB
None
```

###### astype()

```python
def astype(self, dtype, copy=True, errors="raise", **kwargs): pass
```

dtype:指定转换后的类型

copy：是否以拷贝的形式返回结果

```python
import pandas as pd
import numpy as np

FILE_PATH =r"省略掉"

df = pd.read_csv(FILE_PATH)

print(df.dtypes)
df['User-ID'] = df['User-ID'].astype("float")
print("==========转换后==========")
print(df.dtypes)


```

```
User-ID          int64
ISBN            object
Book-Rating    float64
dtype: object
==========转换后==========
User-ID        float64
ISBN            object
Book-Rating    float64
dtype: object
```

astype对于哪些本来就是同一类型的数据很友好，但是遇到了哪些存错的数据，可就不好办了，此时我们需要自定义函数去更改

###### .apply()

```python
import pandas as pd
import numpy as np

def change_gender(string):
    if string == "男":
        return "male"
    else:
        return "female"

data = [
    ['张三','男',19],
    ['李四','女',33],
    ['王五','男',9],
    ['郑浩泓','男',22],
]

columns=['Name','Gender','Age']

df = pd.DataFrame(data = data,columns = columns)
print(df)
df['Gender'] = df['Gender'].apply(change_gender)
print("=====自定义修改后=====")
print(df)

```

```
  Name Gender  Age
0   张三      男   19
1   李四      女   33
2   王五      男    9
3  郑浩泓      男   22
=====自定义修改后=====
  Name  Gender  Age
0   张三    male   19
1   李四  female   33
2   王五    male    9
3  郑浩泓    male   22
```

###### to_numeric()

转数字

```python
import pandas as pd
import numpy as np

def change_gender(string):
    if string == "男":
        return "male"
    else:
        return "female"

data = [
    ['张三','男',19,'3333'],
    ['李四','女',33,'4444'],
    ['王五','男',9,'5555'],
    ['郑浩泓','男',22,'6666'],
]

columns=['Name','Gender','Age','Salary']

df = pd.DataFrame(data = data,columns = columns)
print(df)
df['Gender'] = df['Gender'].apply(change_gender)
df['Salary']=pd.to_numeric(df['Salary'])
print(df.dtypes)
print("=====自定义修改后=====")
print(df.dtypes)

```

```
  Name Gender  Age Salary
0   张三      男   19   3333
1   李四      女   33   4444
2   王五      男    9   5555
3  郑浩泓      男   22   6666
Name      object
Gender    object
Age        int64
Salary     int64
dtype: object
=====自定义修改后=====
Name      object
Gender    object
Age        int64
Salary     int64
dtype: object

Process finished with exit code 0

```

###### to_datatime()

转日期

```python
import pandas as pd
import numpy as np

def change_gender(string):
    if string == "男":
        return "male"
    else:
        return "female"

data = [
    ['张三','男',19,'3333','20200622'],
    ['李四','女',33,'4444','21090909'],
    ['王五','男',9,'5555','20161202'],
    ['郑浩泓','男',22,'6666','20130807'],
]

columns=['Name','Gender','Age','Salary','Resigned-Date']

df = pd.DataFrame(data = data,columns = columns)
print(df)
df['Gender'] = df['Gender'].apply(change_gender)
df['Resigned-Date']=pd.to_datetime(df['Resigned-Date'],format='%Y%m%d')

print("=====自定义修改后=====")
print(df)

```

```
  Name Gender  Age Salary Resigned-Date
0   张三      男   19   3333      20200622
1   李四      女   33   4444      21090909
2   王五      男    9   5555      20161202
3  郑浩泓      男   22   6666      20130807
=====自定义修改后=====
  Name  Gender  Age Salary Resigned-Date
0   张三    male   19   3333    2020-06-22
1   李四  female   33   4444    2109-09-09
2   王五    male    9   5555    2016-12-02
3  郑浩泓    male   22   6666    2013-08-07
```

注意，一定要写时间戳之前的日期，否则会报错



## Part 4 使用Pandas 进行数值统计

#### 4.1 一元统计 

###### .sum()

求和，可通过axis指定方向

###### .mean() .std() .var()

均值，标准差，方差

###### .max() .min() .median()

最大，最小，中值

###### .idxmin() .idxmax()

最小值位置，最大值位置

###### .mode() .shew() .kurt()

众数，偏度，峰度

###### .describe()

一次性输出多个描述性统计指标

#### 4.2 二元统计

演示示例

```python
import pandas as pd
import csv

df = pd.DataFrame(
    {
        "Age":[8,9,10,11,12],
        "Height":[130,135,140,145,150],
        "Score":[100,99,65,32,52]
    })
print(df)

```

```

   Age  Height  Score
0    8     130    100
1    9     135     99
2   10     140     65
3   11     145     32
4   12     150     52
```



###### .cov() 协方差计算

min_period:每列取出NaN后，要参与计算的最小元素个数。

```python
print(df.cov())
```

```
          Age  Height   Score
Age      2.50   12.50  -40.75
Height  12.50   62.50 -203.75
Score  -40.75 -203.75  883.30
```

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.DataFrame(
    {
        "Age":[8,9,10,11,12],
        "Height":[130,135,140,145,150],
        "Score":[100,99,65,32,52]
    })

fig = plt.figure()
plt.scatter(df['Age'],df['Height'],s = 300)
plt.show()

```

![输入图片说明](https://images.gitee.com/uploads/images/2020/0724/142510_ef358b77_5550632.png "屏幕截图.png")

画图可知，身高与年龄正相关,协方差应为正数

```python
print(df['Age'].cov(df['Score']))
print(df['Age'].cov(df['Height']))
```

```
-40.75
12.5
```



######  .corr()计算相关系数

```python
print(df.corr())
```

```
             Age    Height     Score
Age     1.000000  1.000000 -0.867168
Height  1.000000  1.000000 -0.867168
Score  -0.867168 -0.867168  1.000000
```

得分和年龄既合乎是负相关，年龄和身高呈正相关

```python
print(df['Age'].corr(df['Score']))
```

```
-0.8671684996804219
```

#### 4.3 类别型统计运算

###### .count()

```python
def count(self, axis=0, level=None, numeric_only=False):
```

axis: 0 or "index" ,1 or "columns"

level：int or str

numeric_only:boolean 默认False

接下来的实验数据：

```python
import pandas as pd
import numpy as np

data = {
    "Name":["Jack","Michael","Lucy","Tom","Jerry"],
    "Age":[18,np.NaN,23,56,np.NaN],
    "Single":[True,True,False,False,False]
}

df = pd.DataFrame(data = data)
print(df)

```

```
      Name   Age  Single
0     Jack  18.0    True
1  Michael   NaN    True
2     Lucy  23.0   False
3      Tom  56.0   False
4    Jerry   NaN   False

Process finished with exit code 0

```

```python
print(df.count()) #默认 axis = 0,数非NaN的数据个数
```

```
Name      5
Age       3
Single    5
dtype: int64
```

```python
print(df.count(axis = 1)) 
```

```
0    3
1    2
2    3
3    3
4    2
dtype: int64
```

###### .unique() . nunique()

unique() 以数组形式(numpy.ndarray)返回**列的所有唯一值**

nunique():返回**列唯一值的个数

```python
print(df['Name'].unique())
print(df['Name'].nunique())
```

```
['Jack' 'Michael' 'Lucy' 'Tom' 'Jerry']
5
```



###### value_counts()

查看DataFrame中有多少不同值，并计算有多少重复值需要指定index或columns

```python
    def value_counts(
        self, normalize=False, sort=True, ascending=False, bins=None, dropna=True
    ):
```

normalize:True or False 计算频次或频率比

ascending：True or False，排序方式

bins：int pd.cut的快捷方式，对连续数值效果好

```python
print(df['Name'].value_counts(normalize=True))
print(df['Age'].value_counts(normalize=True,bins=2))
```

```
Michael    0.2
Tom        0.2
Lucy       0.2
Jack       0.2
Jerry      0.2
Name: Name, dtype: float64
(17.961, 37.0]    0.4
(37.0, 56.0]      0.2
Name: Age, dtype: float64
```

### Part 5 Apply 函数处理

Apply函数主要的功能之前咱们已经接触过了，现在是详细地讨论。它对DataFrame数据类型适用，主要功能就是针对一列通过自定义函数地方式来进行数据处理。

```python
def apply(self, func, convert_dtype=True, args=(), **kwds): pass
```

第一个参数是函数指针，用来指明自定义函数

默认 axis = 0

```python
import pandas as pd
import numpy as np

data = {
    "Name":["Jack","Michael","Lucy","Tom","Jerry"],
    "Age":[18,63,23,56,2],
    "Single":[True,True,False,False,False],
    "Smoke":[True,True,False,False,False],
}

df = pd.DataFrame(data = data)

df['Adult'] = df['Age'].apply(lambda x: 1 if x>=18 else 0)
print(df)

```

```
      Name  Age  Single  Smoke  Adult
0     Jack   18    True   True      1
1  Michael   63    True   True      1
2     Lucy   23   False  False      1
3      Tom   56   False  False      1
4    Jerry    2   False  False      0
```

由于我懒得写函数了，这里我使用的是Python的匿名函数

还有一个map函数是针对Series对象使用的**（这里指的不是和Python同名的那个映射函数）**

```python
import pandas as pd
import numpy as np

data = {
    "Name":["Jack","Michael","Lucy","Tom","Jerry"],
    "Age":[18,63,23,56,2],
    "Single":[True,True,False,False,False],
    "Smoke":[True,True,False,False,False],
    "House Size":[1,2,3,1,4]
}

df = pd.DataFrame(data = data)
map_dict = {1:"Small",2:"Medium",3:"Large",4:"Very Large"}
# df['Adult'] = df['Age'].apply(lambda x: 1 if x>=18 else 0)
df["House Size"] = df["House Size"].map(map_dict)
print(df)

```

```
      Name  Age  Single  Smoke  House Size
0     Jack   18    True   True       Small
1  Michael   63    True   True      Medium
2     Lucy   23   False  False       Large
3      Tom   56   False  False       Small
4    Jerry    2   False  False  Very Large
```

<br>

### Part 6 Pandas 分组聚合

分组聚合这个概念，大家肯定不陌生，在MySQL中，我们有关键字groupby 和 having，作用就是依据某一字段进行分组操作。在我眼中Pandas的这个分组聚合功能差不多。先看看这函数长啥样吧。

```python
    def groupby(
        self,
        by=None,
        axis=0,
        level=None,
        as_index=True,
        sort=True,
        group_keys=True,
        squeeze=False,
        observed=False,
        **kwargs
    ):
```

```python
import pandas as pd
import numpy as np

company = ["A","B","C","D"]
data = {
    "Company":[ company[x] for x in np.random.randint(0,len(company),10)],
    "Salary": np.random.randint(3000,9200,10),
    "Age":np.random.randint(19,60,10)
}

df = pd.DataFrame(data)

print(type(df.groupby(df["Company"])))
print("==========")
print(df.groupby(df["Company"]))
print("==========")
print(list(df.groupby(df["Company"])))


```

```
<class 'pandas.core.groupby.generic.DataFrameGroupBy'>
==========
<pandas.core.groupby.generic.DataFrameGroupBy object at 0x00000209C237B688>
==========
[('A',   Company  Salary  Age
7       A    8846   38
9       A    3332   57), ('B',   Company  Salary  Age
5       B    8305   20
6       B    3591   55), ('C',   Company  Salary  Age
1       C    6054   46
3       C    6512   26
4       C    4412   25
8       C    3015   31), ('D',   Company  Salary  Age
0       D    8832   35
2       D    5785   36)]

Process finished with exit code 0

```

我们依次会发现groupby之后的对象是叫做**DataFrameGroupBy**

单独打印groupby对象就是一个地址

最后把它变成list里面长成这样

那它能干啥呢？分组之后当然要聚合了，通过这个函数我们可以将**一个大的DataFrame**按需要分成**若干个DataFrame子集**。比如查询不同公司的薪资均值：

```python
import pandas as pd
import numpy as np

company = ["A","B","C","D"]
data = {
    "Company":[ company[x] for x in np.random.randint(0,len(company),10)],
    "Salary": np.random.randint(3000,9200,10),
    "Age":np.random.randint(19,60,10)
}

df = pd.DataFrame(data)


print(df.groupby(df["Company"])["Salary"].mean())


```

```
Company
A    5270.25
B    4591.00
C    5815.00
D    5015.50
Name: Salary, dtype: float64
```

当然还有许多的内置函数，这里我就不一一列举了

![输入图片说明](https://images.gitee.com/uploads/images/2020/0726/111622_b2adc425_5550632.png "屏幕截图.png")

当然还有另外一种方式使用聚合函数，它是**agg函数**

```python
import pandas as pd
import numpy as np

company = ["A","B","C","D"]
data = {
    "Company":[ company[x] for x in np.random.randint(0,len(company),10)],
    "Salary": np.random.randint(3000,9200,10),
    "Age":np.random.randint(19,60,10)
}

df = pd.DataFrame(data)
print(df.groupby(df["Company"]).agg("mean"))

```

```
              Salary    Age
Company                    
A        4538.000000  44.00
B        5297.666667  44.00
C        8983.000000  27.00
D        5842.500000  47.75
```

当然了，我们也一次聚合多种结果，比如计算年龄中位数和薪水的均值

```python
import pandas as pd
import numpy as np

company = ["A","B","C","D"]
data = {
    "Company":[ company[x] for x in np.random.randint(0,len(company),10)],
    "Salary": np.random.randint(3000,9200,10),
    "Age":np.random.randint(19,60,10)
}

df = pd.DataFrame(data)

print(df)
print("===================================")
print(df.groupby(df["Company"]).agg({"Age":"median","Salary":"mean"}))

```

```
  Company  Salary  Age
0       C    3864   49
1       A    6352   54
2       B    8922   45
3       D    3241   52
4       A    8750   46
5       C    6456   59
6       A    4351   30
7       D    8758   54
8       D    4309   52
9       A    3361   30
===================================
         Age  Salary
Company             
A         38  5703.5
B         45  8922.0
C         54  5160.0
D         52  5436.0
```

可能有时我们需要将新统计出的数据导出成新的一列，agg可没有这种功能，此时我们就需要使用**transform函数**，用法和agg基本一样，但是每次只能指定一列。

```python
import pandas as pd
import numpy as np

company = ["A","B","C","D"]
data = {
    "Company":[ company[x] for x in np.random.randint(0,len(company),10)],
    "Salary": np.random.randint(3000,9200,10),
    "Age":np.random.randint(19,60,10)
}

df = pd.DataFrame(data)

print(df)
print("===================================")
df["Median Age"] =  df.groupby(df["Company"])["Age"].transform("median")
df["Avg Salary"] =  df.groupby(df["Company"])["Salary"].transform("mean")
print(df)

```

```
  Company  Salary  Age
0       A    8011   56
1       A    5551   26
2       D    6606   42
3       C    5174   24
4       B    3907   49
5       D    8359   59
6       D    4663   58
7       C    5413   56
8       B    3277   33
9       A    7890   23
===================================
  Company  Salary  Age  Median Age   Avg Salary
0       A    8011   56          26  7150.666667
1       A    5551   26          26  7150.666667
2       D    6606   42          58  6542.666667
3       C    5174   24          40  5293.500000
4       B    3907   49          41  3592.000000
5       D    8359   59          58  6542.666667
6       D    4663   58          58  6542.666667
7       C    5413   56          40  5293.500000
8       B    3277   33          41  3592.000000
9       A    7890   23          26  7150.666667
```

<br>

### Part 7 Pandas 数据合并 (连表)

之前我们用过concat函数进行DataFrame的拼接，现在介绍另外一个函数merge

![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/104018_45d93896_5550632.png "屏幕截图.png")

类似MySQL中的join

```python
import pandas as pd
import numpy as np

teacher = {
    'tid':['001','002','003','004'],
    'name':['Jack','Lucy',"Michael","Zhang Hao Hong"],
    'salary':[3000,4000,5000,6000]
}

classroom = {
    'id':[1,2,3,4],
    'tid':['001','002','003','004'],
    'name':['Earth','Moon','Mars','Jupiter']
}

df1 = pd.DataFrame(teacher)
df2 = pd.DataFrame(classroom)

print(pd.merge(df1,df2,how='inner',on='tid'))

```

```
   tid          name_x  salary  id   name_y
0  001            Jack    3000   1    Earth
1  002            Lucy    4000   2     Moon
2  003         Michael    5000   3     Mars
3  004  Zhang Hao Hong    6000   4  Jupiter
```

这步操作你可以理解成如下SQL语句：

```sql
SELECT * FROM teacher
INNER JOIN classroom
ON teacher.tid = calssroom.tid;
```

当然了，我们在pandas中也可以使用指定多个连表条件

```python
import pandas as pd
import numpy as np

teacher = {
    'id':[1,2,3,4],
    'tid':['001','002','003','004'],
    'name':['Jack','Lucy',"Michael","Zhang Hao Hong"],
    'salary':[3000,4000,5000,6000]
}

classroom = {
    'id':[1,2,3,4],
    'tid':['001','002','003','004'],
    'name':['Earth','Moon','Mars','Jupiter']
}

df1 = pd.DataFrame(teacher)
df2 = pd.DataFrame(classroom)

print(pd.merge(df1,df2,how='inner',on=['tid','id']))

```

```
   id  tid          name_x  salary   name_y
0   1  001            Jack    3000    Earth
1   2  002            Lucy    4000     Moon
2   3  003         Michael    5000     Mars
3   4  004  Zhang Hao Hong    6000  Jupiter
```

pandas 里面没有 MySQL中的 **AS** 关键字进行字段重命名，但是有参数**suffixes指定后缀**

```python
import pandas as pd
import numpy as np

teacher = {
    'id':[1,2,3,4],
    'tid':['001','002','003','004'],
    'name':['Jack','Lucy',"Michael","Zhang Hao Hong"],
    'salary':[3000,4000,5000,6000]
}

classroom = {
    'id':[1,2,3,4],
    'tid':['001','002','003','004'],
    'name':['Earth','Moon','Mars','Jupiter']
}

df1 = pd.DataFrame(teacher)
df2 = pd.DataFrame(classroom)

print(pd.merge(df1,df2,how='inner',on=['tid','id'],suffixes=['_teacher','_classroom']))

```

```
   id  tid    name_teacher  salary name_classroom
0   1  001            Jack    3000          Earth
1   2  002            Lucy    4000           Moon
2   3  003         Michael    5000           Mars
3   4  004  Zhang Hao Hong    6000        Jupiter
```

<br>

### Part 8 Pandas 可视化

pandas的画图依赖matplotlib,所以有些函数其实是matplotlib中的函数。

#### 8.1 pd.plot()

![image-20200727111232482](C:\Users\micha\AppData\Roaming\Typora\typora-user-images\image-20200727111232482.png)

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

df = pd.DataFrame(np.random.randint(-10,10,(10,4)),
                  index=pd.date_range("2020/01/01",periods=10),
                  columns=list("ABCD"))
print(df)
print("================================================")
df = df.cumsum()
df.plot()
plt.show()
```

```
             A  B   C   D
2020-01-01  -1 -7 -10   1
2020-01-02   6 -2  -5  -3
2020-01-03  -4 -6   1   1
2020-01-04   7 -6  -8   0
2020-01-05   9  8  -7   9
2020-01-06  -2 -1   0  -7
2020-01-07   5  1  -4  -5
2020-01-08   2  0 -10  -9
2020-01-09 -10 -7  -5   2
2020-01-10  -8 -6  -1 -10
================================================
```



![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/112404_0ff2a11a_5550632.png "屏幕截图.png")

也可以指定图的x,y轴和各种图像的画法

```python
df.plot(kind="bar")
plt.show()
```

![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/112808_768b70f2_5550632.png "屏幕截图.png")

指定横纵坐标

```python
df.plot(x = 'A',y='B')
plt.show()
```

![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/112947_1a2eeebe_5550632.png "屏幕截图.png")

画直方图

![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/114031_eeb09f99_5550632.png "屏幕截图.png")

画箱型图

![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/114258_11fe2660_5550632.png "屏幕截图.png")

画散点图

![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/114748_98323076_5550632.png "屏幕截图.png")

画堆积图

注意堆积图的值要么全负，要么全正

![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/114850_a7413b3d_5550632.png "屏幕截图.png")

画饼状图

![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/115314_2539cb04_5550632.png "屏幕截图.png")

画六边形图

![输入图片说明](https://images.gitee.com/uploads/images/2020/0727/115647_24525b73_5550632.png "屏幕截图.png")

