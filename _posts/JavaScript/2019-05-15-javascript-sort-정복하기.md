---
layout: post
title: javascript sort() 정복하기
category: JavaScript
tags: JavaScript sort
comments: true
---

> 오늘 알고리즘 문제를 푸는데 sort에 대한 이해도가 많이 떨어진다는 것을 느꼈다. 그래서 자주 사용이 되는 [sort](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 메서드를 정리해본다.


sort() 메서드는 기본적으로 유니코드 값을 비교를 하게된다. mdn 문서에 따르면 자바스크립트에서 제공해주는 sort 메서드는 stable sort가 아닐 수 있다고 한다. 여기서 stable sort라는 것은 쉽게 말해 같은 유니코드 값을 가진 값들의 순서가 보장되냐 보장되지 않느냐를 말하는 것 같다. 예를 들자면 `[5, 1, 2, 3, 5]` 라는 배열을 sort 했을 때 0번째 인덱스의 `5`가 4번째 인덱스의 `5`보다 앞에 있게 정렬이 되지 않는다는 말이다. 


## 매개변수 compareFunction

매개변수로 compareFunction을 주지 않는다면 sort되는 배열의 각각의 요소들을 모두 문자로 변환 후 유니코드 값을 비교해 정렬한다고 한다. 문자 정렬에서는 문제가 되지 않지만 숫자 정렬을 하게 될 경우에는 문제가 생긴다. `[1, 2, 50, 2000, 90]` 이라는 배열을 오름차순 정렬하고자 한다면 `[1, 2, 50, 90, 2000]`을 기대할 것이다. 하지만 compareFunction을 주지않은 sort() 메서드를 사용하게 된다면 기대와 다르게 `[1, 2, 2000, 50, 90]` 으로 정렬이 된다. 이러한 문제가 생기기 때문에

```javascript
const arr = [1, 2, 50, 2000, 90];
arr.sort((a,b) =>{
    return a-b;
})

```

위처럼 매개변수로 compareFunction을 주어야 한다.

compareFunction의 반환값에 따라 정렬이 이루어지는데 
1. 반환 값이 0보다 작은 경우
    - a가 먼저 온다. **오름 차순**
2. 반환 값이 0보다 큰 경우
    - b가 먼저 온다. **내림 차순**
3. 반환 값이 0인 경우
    - 서로에 대한 변경이 없다.

이러한 compareFunction의 특징은 숫자에 대해서는 큰 문제가 생기지 않는다. 하지만 문자열인 경우 문자 사이에서 연산이 가능하지 않기 때문에 대소 비교를 해서 반환 값을 지정해주어야한다.

```javascript
const arr = ['a', 'c', 'd', 'e', 'b'];
arr.sort((a,b)=>{
    if(a<b){
        return -1;
    }
    if(a>b){
        return 1;
    }

    return 0;
})
```

객체로 이루어진 배열의 하나의 속성으로도 정렬이 가능하다. 

```javascript
const arr = [
    {
        'name': 'a'
        'age' : 20
    },
    {
        'name': 'c'
        'age' : 21
    },
    {
        'name': 'b'
        'age' : 31
    }
    ];

arr.sort((a,b)=>{
    //name으로 정렬
    if(a.name<b.name){
        return -1;
    }
    if(a.name>b.name){
        return 1;
    }
    return 0;
})
```
