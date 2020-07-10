# #1 2Sum

## Please check the problem description [here](https://leetcode.com/problems/two-sum/).

## Brute Force

```Java
    class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for(int a = 0; a < nums.length; a++){
            for(int b = a + 1; b < nums.length; b++){
                if (nums[a] + nums[b] == target){
                    result[0] = a;
                    result[1] = b;
                } 
                    
            }
        }
        return result;
    }
}
```
* **Syntax**
  * Make sure `result` is initialized globally
* **Logic**
  * start subarray at one position after the first index
* **Java**
  * `int[]` initialization with `new int[]{p1,p2,p3...}` customized number of parameters

## HashMap Two-Pass
