## [LeetCode 6.Z字形变换](https://leetcode-cn.com/problems/zigzag-conversion/)

#### 解题思路

找规律, 整道题最核心的一点就是变换源字符串中的字符顺序, 根据输入的行数, 确定规律, 再根据规律将源字符串变换为输出串.

#### 具体规律

*下边说的方案是我的方案, 不一定就是最优方案*

1.  当输入的行数为x 的时候

理想输出结果 Z 字形排列的字符串循环节字母个数为$2x-2$

那么第一行输出的字符下标序列就是

 $$0 * (2x-2), 1*(2x-2), 2*(2x-2), ...$$

第二行为

$1, last + (2x-2) - 1*2, last + (2x-2 - (2x-2) - 1*2), ...$

第x行为

$x, last + (2x-2) - x* 2, last + (2x-2 - (2x-2) - x*2), ...$ 

总结规律公式为: 

$$ F(x) = last + \{(j \% 2 ) * (2x - 2) - i*2\} \\ i 行数, j 列数,last 为前一列的值 $$ 

#### 坑

越界问题

#### 源码

```C
char * convert(char * s, int numRows){
    int index = numRows * 2 - 2;
    char *tmp = s;
    int cnt = 0;
    while (*tmp != '\0') tmp++, cnt++;
    if (cnt <= numRows || numRows == 1) return s;
    char *res = malloc(sizeof(char) * (cnt + 1));
    tmp = res;
    for (int i = 0, j = 0, t = 0; i < numRows; i++) {
        t = i;
        j = index - i * 2;
        *tmp++ = s[t];
        while (t + j < cnt) {
            if (j != 0) {
                *tmp++ = s[t + j];
                t += j;
            }
            j = (index == j) ? j : index - j;
        }
    }
    *tmp = '\0';
    return res;
}
```

