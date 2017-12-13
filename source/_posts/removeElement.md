---
title: 移除数组中的元素
date: 2017-12-11 22:08:33
tags:
- 算法
---
> leetcode 第27题

Given an array and a value, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:
 ```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.
```

解法：

```
package array;

import org.junit.Test;

/**
 * @author xy
 * @date 2017/12/11 21:48
 *
 * Given an array and a value, remove all instances of that value in-place and return the new length.
 *
 * Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
 *
 * The order of elements can be changed. It doesn't matter what you leave beyond the new length.
 *
 * Example:
 *
 * Given nums = [3,2,2,3], val = 3,
 *
 * Your function should return length = 2, with the first two elements of nums being 2.
 */
public class removeElement {
    public static void main(String[] args) {
        int[] a = {1,2,3,4,1,1};
        int val = 2;
        int aa = removeElement(a,val);
        System.out.println(aa);
    }

    public static int removeElement(int[] nums, int val) {
        int flag = 0;
        for(int i = 0;i < nums.length;i++){
            if( nums[i] != val ){
                nums[flag] = nums[i];
                flag ++;
            }
        }
        return flag;
    }

    @Test
    public void test(){

    }
}

```
