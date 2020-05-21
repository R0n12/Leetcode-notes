# #75 Sort Colors

## Please check the problem description [here](https://leetcode.com/problems/sort-colors/).

## First Try: Brute Force

```Java
    class Solution {
    public void sortColors(int[] nums) {
        Map<Integer,Integer> map = new HashMap<>();
        map.put(0,0);
        map.put(1,0);
        map.put(2,0);
        for(int i = 0;i<nums.length;i++){
            map.put(nums[i], map.get(nums[i]) + 1);
        }
        int index = 0;
        for(int a = 0; a<map.get(0);a++){
            nums[index] = 0;
            index++;
        }
        for(int b = 0; b<map.get(1);b++){
            nums[index] = 1;
            index++;
        }
        for(int c = 0; c<map.get(2);c++){
            nums[index] = 2;
            index++;
        }
    }
}
```

运用hashmap来存储个数

>### Space: additional space required to store counts. two-pass choice
---

## Dual-pivot partitioning sub-routine Quick Sort

```Java
// basic idea
public void sortColors(int[] nums) {
    int lo = 0, hi = nums.length - 1, i = 0;
    
    while (i <= hi) {
        // if current is 0, swap with the low division, move forward low ptr and cur ptr
        if      (nums[i] == 0) swap(nums, lo++, i++);
        // if current is 2, just need to swap with upper division, move down high ptr only
        else if (nums[i] == 2) swap(nums, i, hi--);
        // if current is 2, leave it, just move up cur ptr
        else if (nums[i] == 1) i++;
    }
}
// swap function
private void swap(int[] nums, int i, int j) {
    int t = nums[i];
    nums[i] = nums[j];
    nums[j] = t;
}
```

>No need for additional structures, in place one pass swapping.  
>Runtime: $\mathcal{O}(n)$
