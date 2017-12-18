---
title: 判断两个树是否相同
date: 2017-12-18 22:12:02
tags:
- 算法
---
> leetcode 第100题
Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.


Example 1:
```
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```
Example 2:
```
Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
```
Example 3:
```
Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
```
解法：
```
package tree;

import apple.laf.JRSUIUtils;
import org.junit.Test;

/**
 * @author xy
 * @date 2017/12/18 21:25
 *
 * Given two binary trees, write a function to check if they are the same or not.
 *
 * Two binary trees are considered the same if they are structurally identical and the nodes have the same value.
 *
 *
 * Example 1:
 *
 * Input:     1         1
 *           / \       / \
 *          2   3     2   3
 *
 * [1,2,3],   [1,2,3]
 *
 * Output: true
 * Example 2:
 *
 * Input:     1         1
 *           /           \
 *          2             2
 *
 *         [1,2],     [1,null,2]
 *
 * Output: false
 * Example 3:
 *
 * Input:     1         1
 *           / \       / \
 *          2   1     1   2
 *
 *         [1,2,1],   [1,1,2]
 *
 * Output: false
 */
public class sameTree {
    public static void main(String[] args) {
        TreeNode tn1 = new TreeNode(1);
        tn1.left = new TreeNode(2);
        //tn1.right = new TreeNode(1);

        TreeNode tn2 = new TreeNode(1);
        //tn2.left = new TreeNode(1);
        tn2.right = new TreeNode(2);

        System.out.println(isSameTree(tn1,tn2));
    }

    public static boolean isSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null){
            return true;
        }
        if(p == null || q == null){
            return false;
        }
        if(p.val == q.val){
            return isSameTree(p.left,q.left) && isSameTree(p.right,q.right);
        }
        return false;

    }

    @Test
    public void test(){

    }
}
```
巩固：
```
1.树遍历要递归来做
```
