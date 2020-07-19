# #31 Next Permutation

## Please check the problem description [here](https://leetcode.com/problems/next-permutation/).


## Single Pass

```Java
public class Solution {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        while (i >= 0 && nums[i + 1] <= nums[i]) {
            i--;
        }
        if (i >= 0) {
            int j = nums.length - 1;
            while (j >= 0 && nums[j] <= nums[i]) {
                j--;
            }
            swap(nums, i, j);
        }
        reverse(nums, i + 1);
    }

    private void reverse(int[] nums, int start) {
        int i = start, j = nums.length - 1;
        while (i < j) {
            swap(nums, i, j);
            i++;
            j--;
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

* **Logic**
  * if the array is in total descending order, no next permutation
  * try to find from the **right**, the first pair of elts that are in descending order, that is `nums[i-1] < nums[i]`
  * than the elts to the **right** of `nums[i-1]` (exclusive) is in descending order
  * just from the **right**, find the elt just bigger than `nums[i-1]`, swap it
  * and then, reverse the **right** array so that the next smallest permutation is guaranteed.
* **Runtime**: $\mathcal{O}(n)$
* **Space**: $\mathcal{O}(1)$