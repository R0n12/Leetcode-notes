# #112 Path Sum

## Please check the problem description [here](https://leetcode.com/problems/path-sum/).

## First Impressions
>1. recursively check if child tree satisfy the path sum with a sum of `target-root.val`

## First Try: Recursive
```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root != null){
            if(root.val == sum && root.right == null && root.left == null){
                return true;
            }else{
                return hasPathSum(root.right,sum-root.val)||hasPathSum(root.left,sum-root.val);
            }
        }else{
            return false;
        }
        
    }
}
```

## Second Try: Iterative