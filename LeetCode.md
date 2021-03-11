## 一、leetcode



### 1. 最大子序列和

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:

输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。


```python
nums = [-2,1,-3,4,-1,2,1,-5,4]
def maxSubArray(nums):
    if len(nums) == 0:
        return
    maxnum = nums[0]  # 全局最大值
    subMax = nums[0]  # 前一个子组合的最大值
    for i in range(1, len(nums)):
        if subMax > 0:
            # 前一个子组合最大值大于0，正向增益
            subMax = subMax + nums[i]
        else:
            # 前一个子组合最大值小于0，抛弃前面的结果
            subMax = nums[i]
        # 计算全局最大值
        maxnum = max(maxnum, subMax)
    return maxnum
ret = maxSubArray(nums)
print(ret)
```

### 2. 加一
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

示例 1:

输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。

【解题思路】

转成数字
然后+1
最后转回列表


```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]: 
        l = digits  # 换成直观简单的名字
        # 1.strat:列表转成字符串
        s = ""
        for i in l:
            s += str(i)
        # 1.end
        s = int(s)  # 转换数字
        s += 1  # 加一
        s = list(str(s))  # 转换回列表
        # 2.strat:列表元素类型转换回int
        for i in range(len(s)):
            s[i]=int(s[i])
        # 2.end
        return s  # 完结撒花
```
【列表转整数】

```python
a = [1,2,3,4,5]
// join函数要求列表中的元素都是字符串，所以需要将列表中的元素都转换为字符串。
a = [str(i) for i in a]
b = int(''.join(a))
```

【列表（元组）转字符串】 

``` python
a = [1,2,3,4,5]
// join函数要求列表中的元素都是字符串，所以需要将列表中的元素都转换为字符串。
a = [str(i) for i in a]
b = ''.join(a)
```

【字符串转列表】

``` python
str1 = "hi hello world"
print(str1.split(" "))
输出：
['hi', 'hello', 'world']
```



### 3.  test



## 二、剑指offer

### 1、字符串全排列

题目描述

输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则按字典序打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

输入描述:

```
输入一个字符串,长度不超过9(可能有字符重复),字符只包括大小写字母。
```

示例1

输入

```
"ab"
```

返回值

```
["ab","ba"]
```

**python 迭代器**
itertools.permutations()
itertools.permutations(iterable, r=None)
连续返回由 *iterable* 元素生成长度为 *r* 的排列。
如果 *r* 未指定或为 `None` ，*r* 默认设置为 *iterable* 的长度，这种情况下，生成所有全长排列。
排列依字典序发出。因此，如果 *iterable* 是已排序的，排列元组将有序地产出。
即使元素的值相同，不同位置的元素也被认为是不同的。如果元素值都不同，每个排列中的元素值不会重复。

``` python
import itertools
s = itertools.permutations(iterable, r=None)
print(s)
>>>
<itertools.permutations object at 0x00000000012E67C0>
```

【重要】permutations返回的是 **对象地址**，原因是在python3里面，返回值已经不再是list，而是iterators（迭代器）, 所以想要使用，只好将iterator 转换成list。

``` python
import itertools

def Permutation(ss):
    if not ss:
        return ss
    result = []
    s = list(itertools.permutations(ss))
    # 列表中的每个元素（元组）转化为字符串  
    # [('a', 'b', 'c'), ('a', 'c', 'b'), ('b', 'a', 'c'), ('b', 'c', 'a'), ('c', 'a', 'b'), ('c', 'b', 'a')]
    for i in s:
        result.append(''.join(i))
    # 使用set方法给list去重
    result = list(set(result))
    # 排序
    result.sort()
    return result

str1 = Permutation('abc')
print(str1)
>>>
['abc', 'acb', 'bac', 'bca', 'cab', 'cba']
```

题目描述

汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

示例1

输入

```
"abcXYZdef",3
```

返回值

```
"XYZdefabc"
```

``` python
def leftMove(str1,num):
    strlen = len(str1)
    leftMoveNum = num % strlen
    str1 = str1[leftMoveNum:] + str1[:leftMoveNum]
    return str1

ret = leftMove("abcXYZdef", 3)
print(ret)
>>>
XYZdefabc
```

**字符串运算符**

下表实例变量 a 值为字符串 "Hello"，b 变量值为 "Python"：

| 操作符 | 描述                                               | 实例                   |
| :----- | :------------------------------------------------- | :--------------------- |
| +      | 字符串连接                                         | >>>a + b 'HelloPython' |
| *      | 重复输出字符串                                     | >>>a * 2 'HelloHello'  |
| []     | 通过索引获取字符串中字符                           | >>>a[1] 'e'            |
| [ : ]  | 截取字符串中的一部分                               | >>>a[1:4] 'ell'        |
| in     | 成员运算符 - 如果字符串中包含给定的字符返回 True   | >>>"H" in a True       |
| not in | 成员运算符 - 如果字符串中不包含给定的字符返回 True | >>>"M" not in a True   |