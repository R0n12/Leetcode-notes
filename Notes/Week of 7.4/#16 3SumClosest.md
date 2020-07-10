# #16 3SumClosest

## Please check the problem description [here](https://leetcode.com/problems/3sum-closest/).

## Two Pointers

```Java
    class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int diff = Integer.MAX_VALUE;
        Arrays.sort(nums);
        for(int i = 0; i< nums.length; i++){
            int lo = i + 1;
            int hi = nums.length - 1;
            while(lo < hi){
                int sum = nums[i]+nums[lo]+nums[hi];
                if(Math.abs(target-sum)<Math.abs(diff)){
                    diff = target - sum;
                }
                if (sum < target){
                    lo ++;
                }else{
                    hi --;
                }
            }
        }
        return target - diff;
    }
}
```
* **Logic**
  * fix one pivotal elt
  * increase the low pointer or decrease the high pointer according to the relationship between the resulting sum and the target.
* **Java**
  * `Math.abs()`
  * `Integer.MAX_VALUE`
  * `Arrays.sort()`
* **Runtime**: $\mathcal{O}(n^2)$
  * `Arrays.sort()` uses Dual-Pivot Quicksort -> $\mathcal{O}(nlog(n))$
* **Space**: $\mathcal{O}(log(n))$~$\mathcal{O}(n)$