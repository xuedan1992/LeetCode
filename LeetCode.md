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

【列表转字符串】 

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

#### 1、



