## [LeetCode 3.无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

#### 解题思路

核心就是遍历与打表^[1]^

**最长子串**^[2]^: 需要注意子串与子序列^[3]^的区别(题目中也提示到了)

#### 具体方案

*下边说的方案是我的方案, 不一定就是最优方案*

1.  建立一个 ascii 码的映射表, 以区分某个字符是否出现过(记录出现位置)
2.  判断原串是否为空, 若为空则直接返回结果 0
3.  使用两个游标, 标记子串的头和尾, 尾游标遍历原串
4.  若尾游标所指字符在映射表中出现过, 则记录子串长度并将头游标移动至出现重复的字符下一位
5.  重复以上过程, 直到遍历结束

#### 坑

1.  题目没有给出可能出现的字符, 所以 映射表是全部 ascii 表
2.  在判断某个字符是否重复的时候 不能只考虑映射表, 还需要考虑映射表中记录的位置在头游标的前边还是后边

#### 源码

```C
int lengthOfLongestSubstring(char * s){
    int letter[128] = {0};
    int max_len = 1;
    int len = 0;
    if (s[0] == '\0') {
        return 0;
    }
    int i, j;
    for (i = 0, j = 0; s[i] != '\0' && j <= i; i++) {
        int index = s[i];
        
        if (letter[index] > 0 && letter[index] >= j) {
            j = letter[index];
            max_len = (max_len < len) ? len : max_len;
            len = i - j + 1;
        } else {
            len += 1;
        }
        letter[index] = i + 1;
    }
    max_len = (max_len < len) ? len : max_len;
    return max_len;
}
```
#### 附录

---

[1] : 打表	就是制作一个hash 表, 支持随机读取, 用来表示某个 key 是否被使用过等.

[2]: 子串	指的是连续的字符串

[3]: 子序列	不一定连续 但符合原串中前后位置关系的字符序列

