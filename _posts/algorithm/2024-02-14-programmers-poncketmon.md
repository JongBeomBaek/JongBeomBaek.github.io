---
title: "[Algorithm] 프로그래머스 폰켓몬"
excerpt: "해쉬 문제인 폰켓몬 문제를 풀어보자~"
category :
  - Algorithm
tag :
  - Algorithm
  - Hash
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 폰켓몬

## 문제 링크
[폰켓몬](https://school.programmers.co.kr/learn/courses/30/lessons/1845)

## 풀이
이 문제 카테고리는 해시에 속해있다.
하지만 문제의도와는 다르게 규칙이 있어보여서 해시를 사용하지 않고 문제를 풀었다... (출제자님 죄송합니다..)
답은 여러개가 될 수 있으니 저의 풀이를 공유드리도록 하겠습니다.
 
**"최대한 많은 종류의 폰켓몬을 포함해서 N/2마리를 선택하려 합니다."**라는 조건을 활용하여
답에 최대 조건을 정합니다
set의 특성을 활용하여 중복된 수를 없앱니다
최대 조건이 set으로 중복수를 제거한 값보다 작을경우 이를 정답으로 사용합니다.

## Code
```python
def solution(nums):
    answer = 0
    max_permute = len(nums)//2
    answer = len(set(nums))
    
    if max_permute < answer:
        answer = max_permute
        
    return answer
```

## 후기
오랜만에 글을 올려보내요.
대학원 생활이 끝난 뒤로도 오랜 시간동안 글을 안올려서 죄송합니다.
앞으로도 계속 꾸준히 글 올리도록하겠습니다. :)