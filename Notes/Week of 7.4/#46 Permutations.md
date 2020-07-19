# #46 Permutations

## Please check the problem description [here](https://leetcode.com/problems/permutations/).


```Java
    class Solution {
  public void backtrack(int n,
                        ArrayList<Integer> nums,
                        List<List<Integer>> output,
                        int first) {
    // if all integers are used up
    if (first == n)
      output.add(new ArrayList<Integer>(nums));
    for (int i = first; i < n; i++) {
      // place i-th integer first 
      // in the current permutation
      Collections.swap(nums, first, i);
      // use next integers to complete the permutations
      backtrack(n, nums, output, first + 1);
      // backtrack
      Collections.swap(nums, first, i);
    }
  }

  public List<List<Integer>> permute(int[] nums) {
    // init output list
    List<List<Integer>> output = new LinkedList();

    // convert nums into list since the output is a list of lists
    ArrayList<Integer> nums_lst = new ArrayList<Integer>();
    for (int num : nums)
      nums_lst.add(num);

    int n = nums.length;
    backtrack(n, nums_lst, output, 0);
    return output;
  }
}
```

* **Logic**
  * Use Backtracking to solve
  * Using recursion to solve
  * first, the big while loop to make each digit as the first digit once -> swap `first` with the `i`th elt
  * Then, in the recursion, make permutation of the `i+1` th elt to the end
  * in the end, swap back head and tail.
* **Java**
  * `Collections.swap()`
  * `List output = new LinkedList()`
* **Runtime** $\mathcal{O}(N!)$ -> $\mathcal{O}(N * N!)$
* **Space** $\mathcal{O}(N!)$