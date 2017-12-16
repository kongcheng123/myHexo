---
title: 爬梯子-递归问题
date: 2017-12-16 16:53:41
tags:
- 算法
---
>leetcode 第70题

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.


Example 1:
```
Input: 2
Output:  2
Explanation:  There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps
```
Example 2:
```
Input: 3
Output:  3
Explanation:  There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

解法：
```
import org.junit.Test;

/**
 * @author xy
 * @date 2017/12/14 22:53
 *
 * leetcode-70
 *
 * You are climbing a stair case. It takes n steps to reach to the top.
 *
 * Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
 *
 * Note: Given n will be a positive integer.
 *
 *
 * Example 1:
 *
 * Input: 2
 * Output:  2
 * Explanation:  There are two ways to climb to the top.
 *
 * 1. 1 step + 1 step
 * 2. 2 steps
 * Example 2:
 *
 * Input: 3
 * Output:  3
 * Explanation:  There are three ways to climb to the top.
 *
 * 1. 1 step + 1 step + 1 step
 * 2. 1 step + 2 steps
 * 3. 2 steps + 1 step
 *
 */
public class climb_stairs {
    public static void main(String[] args) {
        int stairs = 3;
        System.out.println(climbStairs(stairs));
    }

    public static int climbStairs(int n) {
        int i = climb_Stairs(0, n);
        return i;
    }

    public static int climb_Stairs(int i, int n) {
        if (i > n) {
            return 0;
        }
        if (i == n) {
            return 1;
        }
        return climb_Stairs(i + 1, n) + climb_Stairs(i + 2, n);
    }

    @Test
    public void test(){

    }
}
```
感想：典型的递归问题
