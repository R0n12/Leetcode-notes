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
* **Runtime**: $\mathcal{O}(n^2)$
* **Space**: $\mathcal{O}(1)$

## HashMap Two-Pass

```Java
    class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> temp = new HashMap<>();
        int[] result = new int[2];
        for(int i = 0; i< nums.length; i++){
            temp.put(nums[i], i);
        }
        
        for(int a = 0; a < nums.length; a ++){
            int complement = target - nums[a];
            if(temp.containsKey(complement) && temp.get(complement) != a){
                result[0] = a;
                result[1] = temp.get(complement);
            }
        }
        
        return result;
    }
}
```

* **Logic**
  * Make sure to check duplicity of `complement` and `a` 
* **Java**
  * `Map<Integer, Integer> result = new HashMap<>();`
  * `result.put(key, value)`
  * `result.get(key)` -> value
  * `result.containsKey(key)`
* **Runtime**: $\mathcal{O}(n)$
  * `HashMap` reduce look up time to $1$
* **Space**: $\mathcal{O}(n)$

## HashMap One-Pass

```Java
    class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> temp = new HashMap<>();
        int[] result = new int[2];
        
        for(int a = 0; a < nums.length; a ++){
            int complement = target - nums[a];
            if(temp.containsKey(complement) && temp.get(complement) != a){
                result[0] = a;
                result[1] = temp.get(complement);
            }else{
                temp.put(nums[a],a);
            }
        }
        
        return result;
    }
}
```

* **Logic**
  * Instead of first create the full map, this method recorded elt as needed and necessarily.
* **Runtime**: $\mathcal{O}(n)$
  * `HashMap` reduce look up time to $1$
* **Space**: $\mathcal{O}(n)$