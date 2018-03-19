---
title: 平衡二叉树的判断
date: 2018-03-05 22:27:42
tags:
- 算法
---
> leetcode 110题

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
Example 1:

Given the following tree [3,9,20,null,null,15,7]
```
     3
    / \
    9  20
        / \
       15   7
```
Return true.

Example 2:

Given the following tree [1,2,2,3,3,null,null,4,4]:
```
            1
           / \
         2   2
         / \
       3   3
      / \
     4   4
```
Return false.
解法：
```
package tree;

/**
 * @author xy
 * @date 2018/03/05 22:10
 *
 *
 * Given a binary tree, determine if it is height-balanced.
 *
 * For this problem, a height-balanced binary tree is defined as:
 *
 * a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
 * Example 1:
 *
 * Given the following tree [3,9,20,null,null,15,7]:
 *
 *    3
 *   / \
 *  9  20
 *    /  \
 *   15   7
 * Return true.
 *
 * Example 2:
 *
 * Given the following tree [1,2,2,3,3,null,null,4,4]:
 *
 *    1
 *   / \
 *  2   2
 * / \
 *3   3
 * /\
 *4 4
 * Return false.
 */
public class leetcode_110 {
    public static void main(String[] args) {
       TreeNode tn = new TreeNode(3);
       tn.left = new TreeNode(9);
       tn.right = new TreeNode(20);
       tn.right.left = new TreeNode(15);
       tn.right.right = new TreeNode(7);
       System.out.println(isBalanced(tn));
    }

    public static boolean isBalanced(TreeNode root) {
        if(root==null){
            return true;
        }
        return height(root)!=-1;
    }

    public static int height(TreeNode node){
        if(node==null){
            return 0;
        }
        int lH=height(node.left);
        if(lH==-1){
            return -1;
        }
        int rH=height(node.right);
        if(rH==-1){
            return -1;
        }
        if(lH-rH<-1 || lH-rH>1){
            return -1;
        }
        return Math.max(lH,rH)+1;
    }
}
```
