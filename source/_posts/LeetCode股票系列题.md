---
title: LeetCode股票系列题
declare: true
toc: true
date: 2020-07-12 16:36:03
tags: [动态规划,贪心,数组]
categories: [算法,计算机基础]
---

<meta name="referrer" content="no-referrer" />  

<!--more-->

# LeetCode股票系列题

本篇文章希望通过做题的形式，疏导出贪心算法，动态规划，暴力破解等算法的核心。让大家更轻松地学习相关算法。

所有题目的来源：力扣（LeetCode）
主页链接：https://leetcode-cn.com
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



## Part 1 开胃菜-买卖股票的最佳时机

### 0x00 题目描述

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。

注意：你不能在买入股票前卖出股票。

示例 1:

输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
示例 2:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。

### 0x01 题目翻译

> 输入：一个整形数组
>
> > 数据含义：数组内的值为股票价格
> >
> > 题目要求：找到**一次交易**中的**最大值**
>
> 输出：一个数字(最大值)

### 0x02 解题思路

#### 暴力破解

这道题，第一眼看过来，最好想的就是暴力破解法，本质上不就是**向右遍历数组**，**做差找到最大值**。

定义两个下标 i , j 让 j = i+1 ，在不出界的条件下 找一个 arr[j] - arr[i] 为最大的值。代码很简单，我们直接上代码。

```c++
int maxProfit(vector<int>& prices)
{
    int max_val = 0;
    for (int i = 0; i < prices.size(); i++)
    {
        for (int j = i + 1; j < prices.size(); j++)
        {
            max_val = max_val > (prices[j] - prices[i]) ? max_val : (prices[j] - prices[i]);
        }
    }
    return max_val;
}
```

 时间复杂度：O(n^2^)

#### 一次遍历

换一种想法，买卖股票的基本原则是**低买高卖**，也就是说，我确定了最低的买入价格，然后只需要选择一个最高的价格去卖出去就行了。

假设给定的数组为：prices = [7, 1, 5, 3, 6, 4]

如果我们在图表上绘制给定数组中的数字，我们将会得到：

![Profit Graph](https://pic.leetcode-cn.com/cc4ef55d97cfef6f9215285c7573027c4b265c31101dd54e8555a7021c95c927-file_1555699418271)



我们只需在历史最低点买入，就不愁卖不出高价了。那么我们只要用一个变量记录一下历史最低价格 min_price，假设自己的股票是在那天买的。那么我们在第 i 天卖出股票能得到的利润就是 prices[i] - min_price。然后找最大值即可。

```c++
int maxProfit(vector<int>& prices)
{
    int min_price = 100000;
    int max_val = 0;

    for(int i = 0;i<prices.size();i++)
    {
        if (prices[i] < min_price)
        {
            min_price = prices[i];
        }
        if (max_val < (prices[i] - min_val))
        {
            max_val = (prices[i] - min_val);
        }
    }
    return max_val;
}
```

时间复杂度：O(n)



## Part 2 买卖股票的最佳时机Ⅱ



### 0x00 题目描述

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以**尽可能地完成更多的交易（多次买卖一支股票）**。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。



示例 1:

输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
示例 2:

输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
示例 3:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。


提示：

1 <= prices.length <= 3 * 10 ^ 4
0 <= prices[i] <= 10 ^ 4

### 0x01 题目翻译

> 输入：一个整形数组
>
> > 数据含义：数组内的值为股票价格
> >
> > 题目要求：找到**多次次交易**中的**最大值**
>
> 输出：一个数字(最大值)

### 0x02 解题思路

#### 暴力破解

暴力破解，永远的神，我们只要排列组合出所有的情况。最后就能找到最大值。

```c++
int calculate(vector<int>& prices, int d)
{
    if (d >= prices.size())
    {
        return 0;
    }
    int ans = 0;
    for (int i = d; i < prices.size(); i++)
    {
        int val = 0;
        for (int j = i + 1; j < prices.size(); j++)
        {
            if (prices[i] < prices[j])//当后项>前项时，才及进行“卖出”操作
            {
                //从 j+1 项接着开始
                int cur_val = calculate(prices, j + 1) + (prices[j] - prices[i]);
                if (cur_val > val)
                {
                    val = cur_val;
                }
            }
        }
        if (val > ans)
        {
            ans = val;
        }
    }
    return ans;
}

int maxProfit(vector<int>& prices)
{
    int ans = 0;
    ans = calculate(prices, 0);
    return ans;
}

```

时间复杂度：O(n^n^)

#### 一次遍历

我们稍稍留心观察就会发现，**最高的利润，是在连续的多个峰（heap）和多个谷（valley）中出现的**

假设给定的数组为：

[7, 1, 5, 3, 6, 4]

如果我们在图表上绘制给定数组中的数字，我们将会得到：

![](https://pic.leetcode-cn.com/d447f96d20d1cfded20a5d08993b3658ed08e295ecc9aea300ad5e3f4466e0fe-file_1555699515174)

如果我们分析图表，那么我们的兴趣点是连续的峰和谷。

那么我们完全可以一次遍历找出这些特殊点，然后做差求和。

```c++
int maxProfit(vector<int>& prices) 
{
    int ans = 0;
    int valley = prices[0];
    int peak = prices[0];
    int i = 0;
    while (i < prices.size() - 1)
    {

        while (i < prices.size() - 1 &&  prices[i] >= prices[i + 1])
        {
            i++;
        }
        valley = prices[i];
        while (i < prices.size() - 1 && prices[i] <= prices[i + 1])
        {
            i++;
        }
        peak = prices[i];
        ans += (peak - valley);
    }
    return ans;
}
```

时间复杂度：O(n)

