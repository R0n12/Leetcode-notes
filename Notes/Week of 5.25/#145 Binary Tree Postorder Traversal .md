# #145 Binary Tree Postorder Traversal

## Please check the problem description [here](https://leetcode.com/problems/binary-tree-postorder-traversal/).

## First Impressions

>1. Postorder: left -> right -> root

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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        if(root != null){
            if(root.left != null){
                result.addAll(postorderTraversal(root.left));
            }
            if(root.right != null){
                result.addAll(postorderTraversal(root.right));
            }
            result.add(root.val);
        }
        return result;
    }
}
```
>1. initialize java list with: `new ArrayList<Integer>();`, `ArrayList` is not an abstract class.

>Runtime: $\mathcal{O}(n)$, $T(n) = 2T(n/2)+c$  
>Space: $\mathcal{O}(n)$ worst case, $\mathcal{O}(logn)$ average case


