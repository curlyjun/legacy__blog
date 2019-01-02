---
layout: post
title: 002_Reverse Integer
category: Algorithm
tags: algorithm easy
comments: true
---

# 002_Reverse Integer

### 문제

[문제 링크](https://leetcode.com/problems/reverse-integer/)

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```
Input: 123
Output: 321
```

**Example 2:**

```
Input: -123
Output: -321
```

**Example 3:**

```
Input: 120
Output: 21
```

**Note:**
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

------



### 내 풀이

```js
var reverse = function(x) {

    var reVal = "";
    var revNumArr = x.toString().split("").reverse();
    if(revNumArr[revNumArr.length-1] === '-'){
        revNumArr.pop();
        reVal += '-';
    }
    for(var i = 0 ; i < revNumArr.length; i++){
            reVal += revNumArr[i];
    }
    if(Number(reVal) > Math.pow(2,31)-1 || Number(reVal) < Math.pow(-2,31)){
        return 0;
    }
    return Number(reVal);
};
```

좋은 방법이 생각이 안나서 무식하게 풀었다. 절차적으로 나의 풀이를 나타내자면

1. 들어온 수를 문자열로 바꾸고 `split()`을 이용해 배열에 자릿수별로 저장한 후에 `reverse()` 함수로 뒤집어 준다.
2. 마지막 인덱스에 - 가있으면 `pop()` 해준뒤 `reVal`에 더해준다.
3. for문으로 뒤집어진 수가 들어있는 배열을 차례대로 돌며 `reVal`에 넣어준다.
4. 32비트 정수형 범위에 맞는지 확인후 `reVal`을 숫자로 바꾸어 리턴해준다.

처음엔 32비트 정수형 조건을 걸지 않아서 실패했다. 

### Solution 참고해서 풀어본 풀이.

```js
var reverse = function(x) {
    if(x <0){
        return -reverse(-x);
    }
    var rev = 0;
    while(x !=0){
        var pop = x % 10;
        x = Math.floor(x/10);
        rev = rev * 10 + pop;
    }
    if(rev > Math.pow(2,31)-1 || rev < Math.pow(-2,31)){
        return 0;
    }
    return rev;
};
```

 솔루션엔 나머지 연산자를 이용해 while 문을 도는 것이였다. 이 방법도 나름 괜찮다고 느꼈지만 내가 잘못 푼 것인지 처음 푼 방식이 더 속도가 잘나왔다..