---
title: 链表-合并两个链表
date: 2017-12-10 22:03:11
tags:
- 算法
---
> leetcode 第21题

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:
```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

解法：
```
package linked_list;

import org.junit.Test;

/**
 * @author xy
 * @date 2017/12/10 21:31
 *
 * Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
 *
 * Example:
 *
 * Input: 1->2->4, 1->3->4
 * Output: 1->1->2->3->4->4
 */
public class MergeTwoSortedLists {
    public static void main(String[] args) {
        ListNode l = new ListNode(1);
        l.next = new ListNode(2);
        l.next.next = new ListNode(4);

        ListNode ll = new ListNode(1);
        ll.next = new ListNode(3);
        ll.next.next = new ListNode(4);

        mergeTwoLists(l,ll);
    }
    public static ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null){
            return l2;
        }
        if(l2 == null){
            return l1;
        }
        ListNode l4 = new ListNode(0);
        ListNode l3 = l4;
        while( l1 != null && l2 != null ){
            if( l1.val > l2.val ){
                l3.next = l2 ;
                l2 = l2.next;
            }else{
                l3.next = l1;
                l1 = l1.next;
            }
            l3 = l3.next;
        }
        l3.next = l1 == null ? l2 : l1;
        return l4.next;
    }

    @Test
    public void test(){
        ListNode l = new ListNode(0);
        ListNode l1 = new ListNode(1);
        l.next = l1;
    }
}

class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

```
