---
title: 在数组中找任意值的位置
date: 2017-12-12 21:48:56
tags:
- 算法
---
>leetcode 第35题

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example 1:
```
Input: [1,3,5,6], 5
Output: 2
```
Example 2:
```
Input: [1,3,5,6], 2
Output: 1
```
Example 3:
```
Input: [1,3,5,6], 7
Output: 4
```
Example 4:
```
Input: [1,3,5,6], 0
Output: 0
```
解法：
```
package array;

import org.junit.Test;

/**
 * @author xy
 * @date 2017/12/12 21:31
 *
 * Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
 *
 * You may assume no duplicates in the array.
 *
 * Example 1:
 *
 * Input: [1,3,5,6], 5
 * Output: 2
 * Example 2:
 *
 * Input: [1,3,5,6], 2
 * Output: 1
 * Example 3:
 *
 * Input: [1,3,5,6], 7
 * Output: 4
 * Example 1:
 *
 * Input: [1,3,5,6], 0
 * Output: 0
 */
public class searchInsertPosition {
    public static void main(String[] args) {
        int[] arr = {1,3,5,6};
        int num = 0;
        int nn = searchInsert(arr,num);
        System.out.println(nn);
    }

    public static int searchInsert(int[] nums, int target) {
        int flag = 0;
        while( true ){
            if(nums[flag] < target){
                flag ++;
            }else{
                break;
            }
            if( flag >= nums.length ){
                break;
            }
        }
        return flag;
    }

    @Test
    public void test(){

    }
}

```
