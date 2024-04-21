---
title: "[Algorithm] 프로그래머스 K번째수"
excerpt: "정렬 문제인 K번째수 문제를 풀어보자~"
category :
  - Algorithm
tag :
  - Algorithm
  - Sorting
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: K번째수

## 문제 링크
[K번째수](https://school.programmers.co.kr/learn/courses/30/lessons/42748)

## 풀이
정렬 문제중 난이도가 1로 몸풀기 문제로 좋았다.
내장 sort 함수와 리스트에 기본문법인 [시작수:끝수:step수]를 잘 활용하면 쉽게 풀 수 있다.
array[c[0]-1:c[1]] 에서 -1을 한 이유 index가 0부터 시작하기 때문 (c[2]-1 도 동일 이유)
지정된 부분에서 sorting 진행
 
## Code
```python
def solution(array, commands):
    answer = []
    for c in commands:
        answer.append(sorted(array[c[0]-1:c[1]])[c[2]-1])
    return answer
```


## 후기
난이도가 쉽지만 sort함수와 정렬을 어떻게 해야할지 몸풀기로 적당한 문제였다.