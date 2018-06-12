---
layout: post
title:  "63. 不同路径 II"
categories: 算法
tags: leetcode 数组
---

* content
{:toc}

<!--more-->

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

![](https://leetcode-cn.com/static/images/problemset/robot_maze.png)


网格中的障碍物和空位置分别用 1 和 0 来表示。

说明：m 和 n 的值均不超过 100。

示例 1:

```
输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
解释:
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```

解：跟前面一题差不多，主要是注意初始化时，原始矩阵obstacleGrid只要已经出现了一个1，后面的路径矩阵ways就都为0，无路可走了，状态转移的时候判断一下obstacleGrid是否为1，为1的话直接设ways为0。

```
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] ways = new int[m][n];

        //初始化
        for (int i = 0; i < m; i++) {
            if (obstacleGrid[i][0] != 1) {
                ways[i][0] = 1;
            } else {
                ways[i][0] = 0;
                break;
            }
        }
        for (int j = 0; j < n; j++) {
            if (obstacleGrid[0][j] != 1) {
                ways[0][j] = 1;
            } else {
                ways[0][j] = 0;
                break;
            }
        }

        //状态转换
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (obstacleGrid[i][j] != 1) {
                    ways[i][j] = ways[i - 1][j] + ways[i][j - 1];
                } else {
                    ways[i][j] = 0;
                }
            }
        }
        return ways[m - 1][n - 1];
    }
```





