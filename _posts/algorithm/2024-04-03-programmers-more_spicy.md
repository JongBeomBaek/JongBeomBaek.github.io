---
title: "[Algorithm] 프로그래머스 더 맵게"
excerpt: "정렬 문제인 더 맵게 문제를 풀어보자~"
category :
  - Algorithm
tag :
  - Algorithm
  - Heap
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 더 맵게

## 문제 링크
[더 맵게](https://school.programmers.co.kr/learn/courses/30/lessons/42626)

## 풀이
heap은 알아서 sorting되면서 저장되는 자료구조이다. [heap에 대한 설명을 다룬 블로그](https://currygamedev.tistory.com/20)
그렇기 때문에 우선순위 큐(priority queue)처럼 사용하기 좋다.
파이썬에는 우선순위 큐 자료형도 있지만 heapq라는 자료형이 따로 있기 때문에 이것을 사용하여 풀었다 
### 기본 함수 설명
- heapq.heapify(list): 리스트를 heap화 시킨다. (정렬)
- heapq.heappop(list): heap list에서 앞단 원소를 뺀다.
- heapq.heappush(list, component): heap list에 원소(component)를 추가한다.

## Code
```python
import heapq

def solution(scoville, K):
    heapq.heapify(scoville)
    cnt = 0 
    while len(scoville):
        min_1 = heapq.heappop(scoville)
        if min_1 >= K:
            break
        else:
            if len(scoville): 
                min_2 = heapq.heappop(scoville)
                heapq.heappush(scoville, min_1 + (min_2 * 2))
                cnt += 1
            else:
                return -1
    return cnt
```


## 후기
heap을 사용하면 매우쉽게 풀 수 있는 문제이다.
원하는 수치가 안나오면 공식 대로 다시 heap에 넣고 하는 식이기 때문에 heap을 직관적으로 활용할 수 있는 문제 같다.