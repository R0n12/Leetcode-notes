# #144 Binary Tree Preorder Traversal

## Please check the problem description [here](https://leetcode.com/problems/binary-tree-preorder-traversal/).

## First Impressions
>1. Postorder Traversal: traverse from root -> left -> right

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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        if(root != null){
            result.add(root.val);
            if(root.left!=null){
                result.addAll(preorderTraversal(root.left));
            }
            if(root.right!=null){
                result.addAll(preorderTraversal(root.right));
            }
        }
        return result;
    }
}
```
>1. initialize java list with: `new ArrayList<Integer>();`, `ArrayList` is not an abstract class.