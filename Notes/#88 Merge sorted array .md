# #88 Merge Sorted Array

## Please check the problem description [here](https://leetcode.com/problems/merge-sorted-array/).

## Merge and Sort __合并之后排序__

```Java
    class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        //合并数组
        System.arraycopy(nums2,0,nums1,m,n);
        //直接sort
        Arrays.sort(nums1);
    }
}
```
java array sort对于primitive type array用quick sort算法

>### Runtime: $\mathcal{O}((m+n)log(m+n))$, quick sort
>### Space: $\mathcal{O}(1)$, in place sorting

## 


