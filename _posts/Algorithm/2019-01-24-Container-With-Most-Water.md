---
layout: post
title: 006_Container With Most Water
category: Algorithm
tags: algorithm medium leetcode
comments: true


---

# 006_Longest Common Prefix

### 문제

[문제 링크](https://leetcode.com/problems/container-with-most-water/)

Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n*vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

 

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

 

**Example:**

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

------

### 내 풀이

```js
//runtime : 748ms
var maxArea = function(height) {
    var max = 0;
    for(let i = 0 ; i < height.length-1; i++){
        for(let j = i+1; j < height.length; j++){
            var w = j-i;
            var h;
            if(height[i]<height[j]){
                h = height[i];
            }else{
                h = height[j];
            }
            if(max < w*h){
                max = w*h;
            }
        }
    }
    return max;
};
```

더 쉬운 방법이 있을 것 같긴 했는데 내 머리의 한계는 여기까지였다... 

```
  1 2 3 4 5 6
1 x o o o o o
2 x x o o o o
3 x x x o o o
4 x x x x o o
5 x x x x x o
6 x x x x x x
```

길이가 6인 배열이 들어왔다면 위와 같이 `o` 표시 한 부분의 넓이들을 모두 구하게 된다.

시간복잡도는 O(n^2)이다. 때문에 런타임도 748ms 가 나왔다. 후에 솔루션을 보고 다시 풀어보았다.



### Solution 참고 풀이

```js
//runtime : 76ms
var maxArea = function(height) {
    var maxarea = 0;
    var fIdx = 0;
    var lIdx = height.length-1;
    while(fIdx < lIdx){
        maxarea = Math.max(maxarea, Math.min(height[fIdx], height[lIdx])*(lIdx-fIdx));
        if(height[fIdx] < height[lIdx]){
            fIdx++;
        }else{
            lIdx--;
        }
    }
    return maxarea;
};
```

처음엔 이 방법에 대해 이해가 전혀 가지 않았다. 하지만 노력끝에 이해했다..! [이 글](https://leetcode.com/problems/container-with-most-water/discuss/6099/Yet-another-way-to-see-what-happens-in-the-O(n)-algorithm) 을 참고해서 이해하니 이해하기 쉬웠다.

설명을 하자면 첫번째 인덱스와 마지막 인덱스에서 부터 넓이를 찾아가는 것이다. 직사각형을 형성해야 하는게 조건이므로 사각형의 높이는 두 인덱스의 값 중 작은 값을 따르게 된다. 넓이를 구해 `maxarea`와 비교해 큰 값을 다시 `maxarea` 에 저장한다. 

```
  1 2 3 4 5 6
1 x ------- o
2 x x
3 x x x 
4 x x x x
5 x x x x x
6 x x x x x x
```

세로가 왼쪽 줄, 가로가 오른쪽 줄 이라고 가정을 해보자. 처음 시작은 `(1,6)`이다. 첫번째 줄이 마지막 줄보다 작다면 중간의 값들은 계산할 필요가 없어진다.(`------` 표시한 부분). 이유는 첫번째 줄이 높이가 되므로 이미 나올수 있는 최대 값이 나온셈이다. 따라서 첫 번째 줄을 생략한다. (코드에서는 `fIdx++;`)

```
  1 2 3 4 5 6
1 x ------- o
2 x x       o
3 x x x     |
4 x x x x   |
5 x x x x x |
6 x x x x x x
```

다음으로 넘어와 `(2,6)`이다. 이번엔 마지막 줄이 두번째 줄 보다 작다고 해보자. 동일한 이유로 마지막 줄과 나머지 줄들과의 나올 수 있는 값들 중 최대 값이 나왔으므로 생략. 마지막 줄을 제외 한다.(`lIdx--;`).

```
//끝까지 탐색했을 때
  1 2 3 4 5 6
1 x ------- o
2 x x - o o o
3 x x x o | |
4 x x x x | |
5 x x x x x |
6 x x x x x x
```

이와 같은 방법으로 끝까지 탐색(`while(fIdx <lIdx)`)하면 된다.