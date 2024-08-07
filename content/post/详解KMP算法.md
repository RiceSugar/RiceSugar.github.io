---
title: "详解KMP算法"
description: "解释KMP算法的实现和next数组的实现"
tags: [ "Algorithm", "KMP"]
date: 2024-02-06
slug: "kmp-algorithm"
---

### KMP
- 快速查找子串位置的优化算法

#### 时间复杂度
- O(m + n)

#### next 数组含义
- next 数组代表当前位置下，子串中相同前后缀的最长长度，如果匹配失败，这个长度将作为可回溯的位置
- 例如：
	```text
	下标 i:		1 	2	3	4	5	6	7   8   ...
	文本串 S：	a   b   c   d	a	b	e	f   ...
	模式串 P：	a   b   c   d   a   b   c   e
	next数组：	0   0   0   0	1	2	3	0
	```
  - 该算法的模拟过程
    - 约定使用`i`作为`文本串S`的下标，`j`作为`模式串P`的下标
    - 在匹配过程中，当 `i = 7` 时, 此时模式串中 `j = 6`，发现 `s[i] != p[j + 1]` 不匹配，此时进行回溯，发现对应的 `next[j] = 2`，所以下标`j`回溯到下标为`2`的位置进行继续匹配
  - 该算法的原理
    - 因为对于`文本串S`中已经匹配的子串 `abcdab`，我们可以发现**该子串的后缀**（后缀不包括第一个字符）和**模式串的前缀**（前缀不包括最后一个字符）存在**共同的部分**，即子串 `abcdab`中的后缀 `ab`。 
    - 所以我们可以对前后缀进行利用，不需要从头开始匹配，而是从模式串 `ab` 的位置，即下标为`2`的位置继续匹配即可。而在具体实现中，我们根据计算出的 `next` 数组就可以跳转到该位置
  - 如何计算这个共同部分的长度，也就是 `next` 数组？
    - 我们可以使用双指针来计算，`i` 指针用于遍历字符串，`j` 指针用于计算有多长字符串匹配
    - 此处计算也用到了上面字符串匹配的思想，当匹配成功时，`i`和 `j` 同时 `+1` ，当匹配失败时 `p[i] != p[j + 1]`，此时的子串为 `p[0~j]`，对于该子串，我们也会发现有前后缀共同的部分，我们可以利用 `next[j]` 跳转到共同部分的下标。
    - 因为此时的 `j < i`，并且我们已经计算好了 `i` 之前的 next 数组，所以我们就可以直接利用 next 数组来计算 `j` 的位置，即 `j = next[j]`，在计算next数组时也节省了从头开始匹配的时间。
  
#### 创建next数组
```cpp
//经过跳转到字符串中间，减少了从头开始匹配的时间，next数组标记当前字符串匹配失败后应该返回的上一位置
for(int i = 2, j = 0; i <= n; ++i){
	//原数组下标为1~n, i与j + 1错开一位，防止自己和自己匹配，所以i从2开始
    while(j && p[i] != p[j + 1]) j = ne[j];
	//如果下一位不匹配就返回到j的上一个匹配成功的字符串的位置
	//例如ABCDABD
	//i和j+1在位置7且不相同，则j将会返回到位置2继续尝试
	//因为下一位第3位仍然不匹配，所以再次返回到上一位第0位
    if(p[i] == p[j + 1]) j++;//如果匹配成功j将会++
    ne[i] = j;//此时j位置就是最长的匹配长度
}
```

#### 输出子串位置
```cpp
for(int i = 1, j = 0; i <= m; ++i){//这里从1开始为了i和j + 1重合起点
    while(j && s[i] != p[j + 1]) j = ne[j];//如果匹配失败，j返回上一个节点
    if(s[i] == p[j + 1]) j++;//匹配成功，j++
    if(j == n){//完全成功
        cout << i - n << " ";//输出位置
        j = ne[j];//返回上一位置，因为next数组表示当前位置与前缀的最大子串长度，当前位置可能是下一p子串的中间点
    }
}
```

#### java实现
此处实现中，数组起始位置为 0, j 起始位置为 -1
```java
class Solution {
    public int strStr(String haystack, String needle) {
        char[] s = haystack.toCharArray();
        char[] p = needle.toCharArray();
        int[] next = new int[p.length];
        int j = -1;
        next[0] = j; 
		// 初始化模式串中第 0 个位置应该回溯到 -1 的位置
        for(int i = 1; i < p.length; i++){
            while (j > -1 && p[i] != p[j + 1]) j = next[j]; 
			// 当下一个字符串不匹配时，并且可以回溯（j > -1），就回溯到上一个匹配成功的位置
            if(p[i] == p[j + 1]) j++; 
			// 当下一个字符串匹配时，j++
            next[i] = j; 
			// 标记当前位置 i 字符串匹配成功的位置为 j
        }

        j = -1;
        for(int i = 0; i < s.length; i++){ 
			// 注意此处的 i 变为 0，因为要匹配的是 s 文本串，从头开始匹配
            while (j > -1 && s[i] != p[j + 1]) j = next[j];
            if(s[i] == p[j + 1]) j++;
            if(j == p.length - 1){ 
				// 匹配成功，返回位置
                return i - p.length + 1;
            }
        }
        return -1;
    }
}
```

----
注：
- 在严蔚敏的《数据结构》中，next数组计算方式有所出入。
- 要原因是书中使用的比较方式为对`下标i`和`下标j`进行比较，而非此处的`下标i`和`下标j+1`进行比较，因此只需将此处计算的**next数组**每位`+1`后**整体右移**，再将数组第一位修改为`0`，进行偏移