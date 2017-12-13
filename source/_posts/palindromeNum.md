---
title: 判断数字是否为回文
date: 2017-12-13 22:16:05
tags:
- 算法
---
>leetcode 第9题 

Determine whether an integer is a palindrome. Do this without extra space.
解法：
```
import org.junit.Test;

import java.util.ArrayList;
import java.util.List;

/**
 * @author xy
 * @date 2017/12/13 21:38
 *
 * Determine whether an integer is a palindrome. Do this without extra space.
 * 判断数字是否为回文
 */
public class palindromeNumber {
    public static void main(String[] args) {
        int num = -2147447412;
        Boolean tof = isPalindrome( num );
        System.out.println(tof);
    }

    //我自己的写法
    public static boolean isPalindrome(int x) {
        int num = x;
        if( num < 0 ){
            return false;
        }
        List<Integer> a = new ArrayList<Integer>();
        while( num != 0 ){
            int i = num % 10;
            a.add(i);
            num = num / 10;
        }
        for( int j = 0; j < a.size()/2;j++ ){
            if( !a.get(j).equals(a.get(a.size() - 1 - j))){
                return false;
            }
        }
        return true;
    }

    //其他人的做法
    public static boolean others(int x){
        // Special cases:
        // As discussed above, when x < 0, x is not a palindrome.
        // Also if the last digit of the number is 0, in order to be a palindrome,
        // the first digit of the number also needs to be 0.
        // Only 0 satisfy this property.
        if(x < 0 || (x % 10 == 0 && x != 0)) {
            return false;
        }

        int revertedNumber = 0;
        while(x > revertedNumber) {
            revertedNumber = revertedNumber * 10 + x % 10;
            x /= 10;
        }

        // When the length is an odd number, we can get rid of the middle digit by revertedNumber/10
        // For example when the input is 12321, at the end of the while loop we get x = 12, revertedNumber = 123,
        // since the middle digit doesn't matter in palidrome(it will always equal to itself), we can simply get rid of it.
        return x == revertedNumber || x == revertedNumber/10;
    }

    @Test
    public void test(){
    }
}

```
