# #23 Merge K Sorted Lists

## Please check the problem description [here](https://leetcode.com/problems/merge-k-sorted-lists/).

## First Impressions

> 1. compare the first node of every list, but what about there are still nodes smaller than previous nodes?

## Brute Force

```Java
    /**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        // Use List instead of int[] to prevent mandatory size specification
        List<Integer> arr = new ArrayList<Integer>();

        for(ListNode ln : lists){
            // check if null node
            while(ln != null){
                arr.add(ln.val);
                ln = ln.next;
            }
        }
        
        // collections sort
        Collections.sort(arr);
        
        ListNode head = new ListNode();
        ListNode h = head;
        
        for(int i: arr){
            ListNode t = new ListNode(i);
            h.next = t;
            h = h.next; 
        }
        h.next = null;
        
        return head.next;
    }
}
```
Add all integer values into an array and sort the array, construct the  `ListNode` with the data.

> ### Runtime: $\mathcal{O}(nlog(n))$， n number of nodes, sorting algorithms sort $\mathcal{O}(nlog(n))$
> ### Space: $\mathcal{O}(n)$, sorting algorithms may take n constant space, new linked list takes n constant space

* __`List`__ interface of Java
* __`Collections.sort()`__ runtime and implementation




