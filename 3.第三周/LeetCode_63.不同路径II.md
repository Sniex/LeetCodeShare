# [63. 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)

### 题目

> 一个机器人位于一个 m x n 网格的左上角 （\[0\]\[0\] ）。
>
> 机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（\[m\]\[n\]）。
>
> 现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

### 题解

> 参考62题的动态规划，思路一样，在遇到障碍物的时候，设置成有0条道路可以到达

### 代码

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int[] arr = new int[obstacleGrid[0].length];
        arr[0] = 1;
        for (int i = 0; i < obstacleGrid.length; i++) {
            for (int j = 0; j < obstacleGrid[0].length; j++) {
                if (obstacleGrid[i][j] == 1) {
                    arr[j] = 0;
                } else if (j > 0) {
                    arr[j] += arr[j - 1];
                }
            }
        }
        return arr[obstacleGrid[0].length - 1];
    }
}
```

