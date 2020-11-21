
### 题目描述

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

**示例 1：**

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```


限制：

2 <= n <= 100000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof

### 解题思路

一开始，我的思路很简单暴力：对于每个元素通过count方法给出重复的次数，如果返回值大于1，则直接break，并返回该元素。

可是这种方式对于很长的数据，需要花费很长时间。时间复杂度为O(n**n)。这也是自己最后提交时超过了时间限制。

####我的代码

```
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        for i in nums:
            if nums.count(i)>1:
                return i 
                break
```

那么，我们是否可以利用已经遍历过的元素信息呢？

####排序法

首先将数组nums排序，如果相邻的两个元素相等，则返回第一个满足该条件的数字。不过这个方法，会修改原数组。

- 思路是将数组排好序,在查找重复数字,这个思路很简单
- 时间复杂度`O(nlogn)`,空间复杂度`O(1)`

```
class Solution(object):
    def findRepeatNumber(self, nums):
        nums.sort()
        pre = nums[0]
        for index in range(1, len(nums)):
            if pre == nums[index]:
                return pre
            pre = nums[index]
```



#### 哈希表

- 遍历整个数组,当这个数字没有出现过哈希表的时候将其加入进去,如果在哈希表中则直接返回即可
- 时间复杂度`O(n)`,空间复杂度`O(n)`

作者：xiao-xue-66
链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/solution/pythonti-jie-san-chong-fang-fa-by-xiao-xue-66/

```
class Solution(object):
    def findRepeatNumber(self, nums):
        dic = {}
        for i in nums:
            if i not in dic:
                dic[i] = 0
            else:
                return i

```



#### 下标定位法

**解题思路：**
寻找数组中的重复数字，直接想到的方法是遍历数组，并使用 HashMap 统计每个数字的数量，遇到数量大于 11 的数字则返回。此方法时间复杂度和空间复杂度均为 O(N)O(N) 。

题目指出 在一个长度为 n 的数组 nums 里的所有数字都在 0 ~ n-1 的范围内 。 因此，可遍历数组并通过交换操作使元素的 索引 与 值 一一对应（即 nums[i] = i ）。因而，就能通过索引找到对应的值。

遍历中，当第二次遇到数字 x 时，一定有 nums[x] = x （因为第一次遇到 x 时已经将其交换至 nums[x] 处了）。利用以上方法，即可得到一组重复数字。

**算法流程**

- 遍历数组 `nums` ，设索引初始值为 `i = 0`:
  1. **若 `nums[i] == i` ：** 说明此数字已在对应索引位置，无需交换，因此执行 `i += 1` 与 `continue` ；
  2. **若 `nums[nums[i]] == nums[i]` ：** 说明索引 `nums[i]` 处的元素值也为 `nums[i]`，即找到一组相同值，返回此值 `nums[i]`；
  3. **否则：** 当前数字是第一次遇到，因此交换索引为 `i` 和 `nums[i]` 的元素值，将此数字交换至对应索引位置。
- 若遍历完毕尚未返回，则返回 −1 ，代表数组中无相同值。

**复杂度分析：**

- 时间复杂度 O(N)O(N) ： 遍历数组使用 O(N)O(N) ，每轮遍历的判断和交换操作使用 O(1)O(1) 。
- 空间复杂度 O(1)O(1) ： 使用常数复杂度的额外空间。

作者：jyd
链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/solution/mian-shi-ti-03-shu-zu-zhong-zhong-fu-de-shu-zi-yua/
来源：力扣（LeetCode）

```
class Solution:
    def findRepeatNumber(self, nums: [int]) -> int:
        i = 0
        while i < len(nums):
        		#保证i前面的index和值一一对应起来
            if nums[i] == i:
                i += 1
                continue
            #判断是否出现重复    
            if nums[nums[i]] == nums[i]: return nums[i]
            #保证index为nums[i]的值也为nums[i]，即实现与前面互换，互换后用第一个if语句判断是否index与对应的值是否相等，不相等继续执行互换语句直至相等
            nums[nums[i]], nums[i] = nums[i], nums[nums[i]]
        return -1
```

**图解：**

![数组中重复的数字1](/数组中重复的数字1.jpg)

![数组中重复的数字1](/数组中重复的数字2.jpg)

![数组中重复的数字1](/数组中重复的数字3.jpg)

![数组中重复的数字1](/数组中重复的数字4.jpg)

![数组中重复的数字1](/数组中重复的数字5.jpg)

![数组中重复的数字1](/数组中重复的数字6.jpg)

![数组中重复的数字1](/数组中重复的数字7.jpg)

![数组中重复的数字1](/数组中重复的数字8.jpg)

![数组中重复的数字1](/数组中重复的数字9.jpg)



