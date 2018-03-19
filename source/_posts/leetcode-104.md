---
title: 求二叉树最深高度
date: 2017-12-25 22:10:25
tags:
- 算法
- 二叉树
---
>leetcode 第104题

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

解法：
```
package tree;

import org.junit.Test;

/**
 * @author xy
 * @date 2017/12/21 21:58
 *
 * Given a binary tree, find its maximum depth.(给定一个二叉树，找到它的最大深度。)
 *
 * The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
 * (最大深度是沿着从根节点到最远叶节点的最长路径的节点的数量。)
 */
public class maximumDepthOfBinaryTree {
    public static void main(String[] args) {
        TreeNode tn = new TreeNode(1);
        TreeNode tn1 = new TreeNode(2);
        TreeNode tn2 = new TreeNode(4);
        tn.right = tn1;
        tn1.right = tn2;
        System.out.println(maxDepth(tn));

    }

    public static int maxDepth(TreeNode root) {
        if(root==null){
            return 0;
        }
        return 1+Math.max(maxDepth(root.left),maxDepth(root.right));
    }

    @Test
    public void test(){

    }
}
```
