---
layout: post
title: 005_Longest Common Prefix*
category: Algorithm
tags: algorithm easy leetcode
comments: true

---

# 005_Longest Common Prefix

### 문제

[문제 링크](https://leetcode.com/problems/longest-common-prefix/)

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```
Input: ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

**Note:**

All given inputs are in lowercase letters `a-z`.

------

### 내 풀이(풀지 못해 다른 사람 코드 참조함.)

```js
//runtime : 96ms
var longestCommonPrefix = function(strs) {
    if(strs.length === 0){
        return "";
    }
    return strs.reduce(function(prev,next){
        var i = 0;
        while(prev[i] === next[i] && prev[i] && next[i]){
            i++;
        }
        return prev.slice(0,i);
    })
};
```

easy문제를 풀지 못해 다른 사람 코드를 참조하게 될지는 몰랐다.. 나중에 한번 더 풀어봐야겠다.

`reduce()`를 이용해서 배열의 요소들을 같지 않은 문자열이 나올 때까지 `while문`을 돌려 확인 후 같은 부분까지 return해주어 다음 요소과 또 비교하는 방식이다. 

