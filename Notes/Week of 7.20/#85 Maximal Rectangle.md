# #85 Maximal Rectangle

## Please check the problem description [here](https://leetcode.com/problems/maximal-rectangle/)

### 1. DP: Better Brute Force on Histograms

```Java
    class Solution {
    public int maximalRectangle(char[][] matrix) {

        if (matrix.length == 0) return 0;
        int maxarea = 0;
        int[][] dp = new int[matrix.length][matrix[0].length];

        for(int i = 0; i < matrix.length; i++){
            for(int j = 0; j < matrix[0].length; j++){
                if (matrix[i][j] == '1'){

                    // compute the maximum width and update dp with it
                    dp[i][j] = j == 0? 1 : dp[i][j-1] + 1;

                    int width = dp[i][j];

                    // compute the maximum area rectangle with a lower right corner at [i, j]
                    for(int k = i; k >= 0; k--){
                        width = Math.min(width, dp[k][j]);
                        maxarea = Math.max(maxarea, width * (i - k + 1));
                    }
                }
            }
        } return maxarea;
    }
}
```

* **Syntax**
  * `dp[i][j] = j == 0? 1: dp[i][j-1] + 1` -> `?` operator
  * ```Java
     dp[i][j] = 1 if(j == 0)
     dp[i][j] = dp[i][j-1] + 1 if (j!=0)
* **Logic**
  * calculate maxwidth for each cell in the grid
  * for each calculated cell, treat it as the lower right corner of a certain rectangle.
  * count upward until the first row, update minimum width and maximum area.
  * Use another matrix `dp[][]` to store each cell's calculated maximum cumulated width.
  * ![alt text](Week%20of%207.20%20Images/8501.png)
* **Runtime**: $\mathcal{O}(N^2M)$
  * calculate max area for each cell -> $N\cdot M$
  * for each cell, count up toward the first row -> $N$
* **Space**: $\mathcal{O}(NM)$ -> equal `dp[][]` matrix
  
> 1. 也是另一种遍历吧，通过存储一定的宽度在另一个数据结构里来加快最大面积的查找。
> 2. 依旧是针对每个点的遍历



