# Merge k Sorted Linked Lists
## https://leetcode.com/problems/merge-k-sorted-lists

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:

Input:
[
  1->4->5,
  1->3->4,
  2->6
]

Output: 1->1->2->3->4->4->5->6

# Implementation :

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null)
            return null;
        Queue<Integer> pq = new PriorityQueue<>();
        for(ListNode node : lists){
            while(node != null){
                pq.add(node.val);
                node = node.next;
            }
        }
        ListNode head = null;
        ListNode prev = null;
        while(!pq.isEmpty()){
            ListNode node = new ListNode(pq.remove());
            if(head == null)
                head = node;
            if(prev != null)
                prev.next = node;
            prev = node;
        }
        return head;
    }
}

```

# References :
https://www.youtube.com/watch?v=zLcNwcR6yO4
