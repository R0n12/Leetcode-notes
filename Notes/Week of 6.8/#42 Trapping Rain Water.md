# #42 Trapping Rain Water

## Please check the problem description [here](https://leetcode.com/problems/trapping-rain-water/).

## First Impressions

>1. try to iterate through the array to find the left bound and the right bound and make it  $\mathcal{O}(n)$.
>2. However, it was hard to track and keep increment the value since there are conditions that not all the max right are fulfilled.

## Brute Force
```Java
    class Solution {
    public int trap(int[] height) {
        int ans = 0;
        for(int i = 0; i< height.length;i++){
            int left_max = 0;
            int right_max = 0;
            for(int a = i; a >= 0; a--){
                left_max = Math.max(left_max, height[a]);
            }
            for(int b = i; b<height.length;b++){
                right_max = Math.max(right_max, height[b]);
            }
            ans += (Math.min(left_max, right_max)-height[i]);
        }
        return ans;
    }
}
```
Loop through the array, instead of finding right bound and left bound for the entire array, search both bounds for each block, and add the difference between them to the total area.  
right bound: `left_max=Math.max(left_max,height[j])`  
left bound: `right_max=Math.max(right_max,height[j])`  
total: `ans += Math.min(left_max, right_max)-height[current]`

>### Runtime: $\mathcal{O}(n^2)$, since looping through all the index to find bounds for each element in the array.
>### Space: $\mathcal{O}(1)$, no extra space.



