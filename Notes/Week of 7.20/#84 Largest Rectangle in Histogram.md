# #84 Largest Rectangle in Histogram

## Description
Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![Alt text](https://assets.leetcode.com/uploads/2018/10/12/histogram.png)

Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.

![Alt text](https://assets.leetcode.com/uploads/2018/10/12/histogram_area.png)

The largest rectangle is shown in the shaded area, which has area = `10` unit.

## Example
```java
Input: [2,1,5,6,2,3]
Output: 10
```
---
## Code

### 1. Brute Force (__NOT PASSING__)

>1. find the minimal height between any pair of rectangles by brute force searching.
>2. calculate max area, store and compare.


```Java

    class Solution {
    public int largestRectangleArea(int[] heights) {
        int result = 0;
        for(int i = 0; i<heights.length;i++){
            for(int j = i; j<heights.length;j++){

                // set minimal to max, so we can keep compare
                int minimal = Integer.MAX_VALUE;

                // search through all the spaces between and find the minimal height
                for(int k = i;k<=j;k++){
                    minimal = Math.min(minimal,heights[k]);
                   
                }

                // compare and store the max result
                 result = Math.max(result,minimal*(j-i+1));
            }
        }
        return result;
    }
}
```

### Runtime:

$\mathcal{O}(n^3)$, two for loops $\mathcal{O}(n^2)$, go through the gap to find the minimal height $\mathcal{O}(n)$.

### Space:

No extra storage needed, $\mathcal{O}(1)$ space complexity.

### 2. Better Brute Force

>same logic as the first solution, reduce one for-loop.

```Java
    class Solution {
    public int largestRectangleArea(int[] heights) {
        int result = 0;
        for(int i = 0; i<heights.length;i++){
            int minimal = Integer.MAX_VALUE;
            for(int j = i; j<heights.length;j++){

                // compare and store as soon as the searching begins
                minimal = Math.min(minimal,heights[j]);
                result = Math.max(result, minimal*(j-i+1));
            }
        }
        return result;
    }
}
```

### Runtime:

$\mathcal{O}(n^2)$, two for loops $\mathcal{O}(n^2)$

### Space:

No extra storage needed, $\mathcal{O}(1)$ space complexity.

## Using Stack

```Java
    public class Solution {
    public int largestRectangleArea(int[] heights) {
        Stack < Integer > stack = new Stack < > ();
        stack.push(-1);
        int maxarea = 0;
        for (int i = 0; i < heights.length; ++i) {
            while (stack.peek() != -1 && heights[stack.peek()] >= heights[i])
                maxarea = Math.max(maxarea, heights[stack.pop()] * (i - stack.peek() - 1));
            stack.push(i);
        }
        while (stack.peek() != -1)
            maxarea = Math.max(maxarea, heights[stack.pop()] * (heights.length - stack.peek() -1));
        return maxarea;
    }
}
```




