---
title: 299. Bulls and Cows
date: 2018-06-03 21:25:19
tags: [Array]
categories: [LeetCode, Array]
---

## Question
You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.

Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. 

Please note that both secret number and friend's guess may contain duplicate digits.

Note: You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.


## Analysis
有点像anagram，可以通过一个数组代替hashmap记录，可以做到one pass
- bulls 很容易， secret.charAt(i) == guess.charAt(i) bulls++
- cows 
    - if (numbers[secret.charAt(i)-'0']++ < 0) cows++;
    - if (numbers[guess.charAt(i)-'0']-- > 0) cows++;

## Complexity
Time: O(n)
Space: O(1)

## Solution
```Java
public String getHint(String secret, String guess) {
    int len = secret.length();
    int[] arr = new int[256];
    int A = 0;
    int B = 0;
    for (int i = 0; i < len; i++) {
        if (secret.charAt(i) == guess.charAt(i)) {
            A++;
        } else {
            arr[secret.charAt(i)]++;
            arr[guess.charAt(i)]--;    
        }
    }
    
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] < 0) {
            B += arr[i];
        }
    }
    
    
    return A+"A"+(len+B-A)+"B";
}
```

One Pass
```Java
public String getHint(String secret, String guess) {
    int bulls = 0;
    int cows = 0;
    int[] numbers = new int[10];
    for (int i = 0; i<secret.length(); i++) {
        if (secret.charAt(i) == guess.charAt(i)) bulls++;
        else {
            if (numbers[secret.charAt(i)-'0']++ < 0) cows++;
            if (numbers[guess.charAt(i)-'0']-- > 0) cows++;
        }
    }
    return bulls + "A" + cows + "B";
}
```