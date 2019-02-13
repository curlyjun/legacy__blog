---
layout: post
title: hash table 정리
category: 자료구조
tags: 자료구조
comments: true
---

# 해시 테이블(hash table)

![](/assets/images/post_img/hashtable.jpg)

### pseudo code

1. **data** 가 들어온다면, value로 **data**를 갖고 next = null인 객체(연결리스트)로 생성
2. 배열(해시 테이블) 생성
3. 데이터를 해쉬 함수에 넣어 나온 값인 인덱스에 연결리스트로 데이터 저장
4. 인덱스에 값이 있다면 기존에 있던 연결리스트와 연결

