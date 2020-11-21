
### 题目描述

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

**限制：**

```
0 <= s 的长度 <= 10000
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof

### 解题思路

对于python中的str是不可变类型，所以可以新建一个空字符串，然后遍历输入的字符串，如果如果是空格则用'%20'替换后添加到新的字符串里面，如果不是则直接添加里面。

#### 算法实现1

```
class Solution:
    def replaceSpace(self, s: str) -> str:
        new_str=''
        for i in s:
            if i == ' ':
                new_str = new_str + '%20'
            else:
                new_str = new_str + i
        return new_str
```

| **27 / 27** 个通过测试用例               | 状态：通过                     |
| ---------------------------------------- | ------------------------------ |
| 执行用时：**36 ms**内存消耗：**13.7 MB** | 用时击败85.38%；内存击败100%。 |

#### 算法实现2

python中join()函数方法用于将序列中的元素以指定的的字符连接生成一个新的字符串。

```
class Solution:
    def replaceSpace(self, s: str) -> str:
        new_str = []
        for i in s:
            if i == ' ': 
            		res.append("%20")
            else: 
            		res.append(i)
        return "".join(res)
```

