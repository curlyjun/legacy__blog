---
layout: post
title: 003_Reverse Integer
category: Algorithm
tags: algorithm easy
comments: true

---

# 003_Palindrome Number

### 문제

[문제 링크](https://leetcode.com/problems/palindrome-number/)

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

**Example 1:**

```
Input: 121
Output: true
```

**Example 2:**

```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

**Example 3:**

```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

**Follow up:**

Coud you solve it without converting the integer to a string?

------

### 내 풀이

```js
//runtime : 256ms
var isPalindrome = function(x) {
    return (x.toString() === x.toString().split("").reverse().join(""))
};
```

문제의 **follow up** 부분을 읽지 못하고 문자열로 바꾼 후에 뒤집어준 후 비교했다... (어쩐지 쉽더라니..)

### 다시 풀어본 풀이

```js
//runtime : 360ms
var isPalindrome = function(x) {
    if(x<0 || (x % 10 === 0)){
        return false;
    }
    var originNum = x;
    var rev = 0;
    while(x !=0){
        var pop = x % 10;
        x = Math.floor(x/10);
        rev = rev * 10 + pop;
    }
    return originNum === rev;
};
```

 [어제 마침 수를 뒤집는 알고리즘](https://curlyjun.github.io/algorithm/2019/01/02/Reverse-Integer/)을 풀어봤기에 같은 방식을 이용해 풀었다. 코드의 실행은 잘 되었으나 속도는 늦어졌다.  

1. **example 2,3**을 반영한 조건을 처음에 넣어주고 
2. 수를 뒤집의면서 변형될 x의 값을 `originNum` 변수에 담아준 뒤에
3. 수를 뒤집어준 후 비교를 하면 된다.

------

다른 사람들의 풀이도 나와 비슷했다.