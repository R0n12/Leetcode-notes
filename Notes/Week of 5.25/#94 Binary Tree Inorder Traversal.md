# #94 Binary Tree Inorder Traversal

## Please check the problem description [here](https://leetcode.com/problems/binary-tree-inorder-traversal/).

## First Impressions
> 1. Inorder Traversal: traverse from left -> root -> right
> 2. Java List initialization:   
> `List<Integer> result = new ArrayList<Integer>();`  
> `result.addAll();`

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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        if(root != null){
            if(root.left != null){
                result.addAll(inorderTraversal(root.left));   
            }
            result.add(root.val);
            if(root.right != null){
                result.addAll(inorderTraversal(root.right));
            }
        }
        return result;
    }
}
```
> 1. check if root has a value: Exception input `[]`
> 2. check if left child or right child has a value.

>Runtime: $\mathcal{O}(n)$, $T(n) = 2T(n/2)+c$  
>Space: $\mathcal{O}(n)$ worst case, $\mathcal{O}(logn)$ average case

## First Try: Iterative

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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> temp = new Stack<TreeNode>();
        while(root != null||!temp.isEmpty()){
            while(root!=null){
            temp.push(root);
            root = root.left;
            }
            root = temp.pop();
            result.add(root.val);
            root = root.right;
        }
        return result;
    }
}
```

> 1. Java Stack Initialization: `Stack<TreeNode> temp = Stack<TreeNode>();`

>Runtime: $\mathcal{O}(n)$ , visiting each node exactly once  
>Space: $\mathcal{O}(n)$, keeping the entire tree in the stack.



