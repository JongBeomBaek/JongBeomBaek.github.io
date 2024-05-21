---
title: "[Algorithm] 프로그래머스 최고의 집합"
excerpt: "연습문제 최고의 집합"
category :
  - Algorithm
tag :
  - Algorithm
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 최고의 집합

## 문제 링크
[최고의 집합](https://school.programmers.co.kr/learn/courses/30/lessons/12938)

## 풀이
이문제를 본 순간 떠오른 수식은 _**n^2 > (n-1)(n+1) = n^2 - 1**_ 가 떠올랐다.
그로인해 n으로 나뉘어 질 수 있으면 n으로 나누고 나머지를 뒤에서부터 하나씩 더해가는 식으로 풀었더니 다맞았다.


### 코드설명
// 연산자 = 몫
%  연산자 = 나머지
몫을 n 개 리스트에 넣고 뒤에서부터 나머지를 하나씩 빼서 더해준다.

## Code
```python
def solution(n, s):
    div = s // n
    rem = s % n 
    if div == 0:
        return [-1]
    else:
        answer = [div] * n
        for i in range(-1, -(rem+1), -1):
            answer[i] += 1
        return answer
```

## 후기
등대와 같이 어려운 문제를 풀다가 힐링 할 수 있는 문제였다.
