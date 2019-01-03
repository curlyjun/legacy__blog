---
layout: post
title: 004_Roman to Integer
category: Algorithm
tags: algorithm easy leetcode
comments: true
---

# 004_Roman to Integer

### 문제

[문제 링크](https://leetcode.com/problems/roman-to-integer/)

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

------

### 내 풀이

```js
//runtime : 132ms
var Roman = {
    I: 1,
    V: 5,
    X: 10,
    L: 50,
    C: 100,
    D: 500,
    M: 1000
};
var romanToInt = function(s) {
    var num = 0;
    for(var i = 0 ; i < s.length ; i++){
        if(Roman[s[i]] < Roman[s[i+1]]){	//<<<<< 
            num += Roman[s[i+1]] - Roman[s[i]];
            i++;
        }else{
            num += Roman[s[i]] ;
        }
    }
    return num;
};
```

 처음엔 `split()` 함수를 이용해 들어온 `s` 값을 배열로 하나하나 나누어 담아 풀었는데 굳이 그럴필요가 없다고 느껴 수정하였다. (속도에는 아무런 영향을 미치지 못했다).

풀면서도 좋지 않은 코드라고 느낀 이유는 주석으로 표시해놓은 줄이 마음에 들지 않았기 때문이다. 자바스크립트가 느슨한 언어여서인지 **인덱스 범위를 초과한 부분에 대해서 컴파일러가 오류를 잡아주지 않는다.** 때문에 마지막 for문을 돌 때 인덱스 범위를 초과한 것(결국 `undefind`)과 비교를 하게 되는데 어떤 값이든 `undefind` 와 비교 연산을 하면 false 로 빠지게 되어 해당 문제에서는 크게 문제 될 것이 없기는 했다.

코드가 마음에 들지 않았기에 다른 여러 코드들을 보고 참고하여 다시 풀어보았다.

### 다른 사람 풀이 참고해서 푼 풀이

```js
//runtime : 132ms
var Roman = {
    I: 1,
    V: 5,
    X: 10,
    L: 50,
    C: 100,
    D: 500,
    M: 1000
};
var romanToInt = function(s) {
    var num = 0;
    for(var i = 0; i < s.length-1; i++){
        if(Roman[s[i]] < Roman[s[i+1]]){
            num -= Roman[s[i]];
        }else{
            num += Roman[s[i]];
        }
    }
    return num + Roman[s[s.length-1]];
};
```

for 문에서  `s.length-1`이기 때문에  인덱스 범위를 초과하지 않고 이전 풀이에 비해 코드를 이해하기에도 더 쉽게 짜인듯 하다.  

이 문제에서는 

---

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

---

이 부분을 어떻게 잘 해결하느냐에 있었던 것 같다. 