---
title: 链表-去除连续重复的元素
date: 2017-12-19 22:46:57
tags:
- 算法
---
> leetcode 第83位

Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.

解法：
```
package linked_list;

import org.junit.Test;

/**
 * @author xy
 * @date 2017/12/19 22:05
 *
 * Given a sorted linked list, delete all duplicates such that each element appear only once.
 *
 * For example,
 * Given 1->1->2, return 1->2.
 * Given 1->1->2->3->3, return 1->2->3.
 */
public class RemoveDuplicatesfromSortedList {
    public static void main(String[] args) {
        ListNode ln = new ListNode(1);
        ListNode ln1 = new ListNode(1);
        ListNode ln2 = new ListNode(2);
        ln.next = ln1;
        ln1.next = ln2;
        deleteDuplicates(ln);


    }

    public static ListNode deleteDuplicates(ListNode head) {
        ListNode ln = head;
        while( ln != null && ln.next != null ){
            if(ln.next.val == ln.val){
                ln.next = ln.next.next;
            }else{
                ln = ln.next;
            }
        }
        return head;
    }

    @Test
    public void test(){

    }
}
```

