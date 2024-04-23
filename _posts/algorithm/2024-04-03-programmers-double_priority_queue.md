---
title: "[Algorithm] 프로그래머스 이중 우선순위 큐"
excerpt: "정렬 문제인  이중 우선순위 큐 문제를 풀어보자~"
category :
  - Algorithm
tag :
  - Algorithm
  - Heap
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 이중 우선순위 큐

## 문제 링크
[이중 우선순위 큐](https://school.programmers.co.kr/learn/courses/30/lessons/42628)

## 풀이
같은 난이도인 [디스크 컨트롤러](2024-04-03-programmers-disk_controller) 에 비해서 쉬웠다.
힙으로 정렬되어 있음으로
- 'D 1':	큐에서 최댓값을 삭제합니다. = 그냥 list pop **(맨 뒤 = 제일 큰 원소 빼기)**
- 'D -1':	큐에서 최솟값을 삭제합니다. = heap.pop **(맨 앞 = 제일 작은 원소 빼기)**
- 'I 숫자':  큐에 주어진 숫자를 삽입합니다. = heap.push

## Code
```python
import heapq

def solution(operations):
    answer = []
    for op in operations:
        if op == "D -1":
            if len(answer):
                heapq.heappop(answer)
        elif op == "D 1":
            if len(answer):
                answer.pop()
        else:
            heapq.heappush(answer,int(op[2:]))
    if len(answer) > 1:
        return [max(answer),min(answer)]
    else:
        return [0,0]
```


## 후기
파이썬 리스크에 pop함수를 잘활용하면 양방향성으로 최소 최대를 뽑는 heap 특성을 활용한 문제같다.
다만 이게 디스크 컨트롤러랑 같은 난이도인건 다소 의문이 든다.