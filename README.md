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

# Implementation 1 : Naive 
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
        if(lists == null || lists.length  == 0)
            return null;
        if(lists.length == 1)
            return lists[0];
        
        ListNode mergedList = mergeTwoLists(lists[0], lists[1]);
        for(int i = 2; i < lists.length; i++) {
             mergedList = mergeTwoLists(mergedList, lists[i]);   
        }
        return mergedList;
    }
    
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null || l2 == null)
            return (l1 == null) ? l2 : l1;
        ListNode p1 = l1;
        ListNode p2 = l2;
        
        ListNode head = null;
        ListNode node = null;
        ListNode current = null;
        
        while(p1 != null && p2 != null) {
            if(p1.val <= p2.val) {
                node = new ListNode(p1.val);
                p1 = p1.next;
            } else {
                node = new ListNode(p2.val);
                p2 = p2.next;
            }    
            
            if(head == null) {
                head = node;
                current = node;
            } else {
                current.next = node;
                current = node;
            }
        }
        
        while(p1 != null) {
            node = new ListNode(p1.val);
            current.next = node;
            current = node;
            p1 = p1.next;
        }
        while(p2 != null) {
            node = new ListNode(p2.val);
            current.next = node;
            current = node;
            p2 = p2.next;
        }
        return head;
        
    }
}
```

# Implementation 2 :

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
