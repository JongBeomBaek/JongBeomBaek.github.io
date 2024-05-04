---
title: "[Algorithm] 프로그래머스 야근 지수"
excerpt: "연습문제 야근 지수 문제"
category :
  - Algorithm
tag :
  - Algorithm
  - Heap
  - PriorityQueue
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 야근 지수

## 문제 링크
[야근 지수](https://school.programmers.co.kr/learn/courses/30/lessons/12927)

## 풀이
제곱으로 지수를 나타내는것을 최소화 하기 위해서는 works 리스트에서 가장 큰 수를 줄여주는게 전체 야근 지수를 줄이는 조건이라고 생각하여 풀었다.
그로인해 최대 수를 출력하면서 처리하는 자료구조 Heap(= Priority Queue)을 사용하였다.

### 코드설명
- works 리스트를 음수로 변경하는 이유
    heapq 라이브러리는 최소값을 우선순위로 하는 정렬이 되기 때문에 반대로 큰 일을 pop하여 줄여주기 위해서는 반대로 음수처리하였다.
- N 번 반복문
    *반복문이 돌면서 일의 수치가 높은걸 가져와 1 줄여주고 다시 heap에 넣는다.*
    위 과정을 반복하게 되면 배열에 모든 원소들이 큰 것 우선순위로 줄어들어 지수가 작은 최적의 결과에 도달할 것이다.

### for - else 문
같이 코딩 스터디하는 지인분이 **for문을 break하지 않고 다 돌았을 경우** else 문으로 빠질 수 있다는 python에 모르던 문법을 알려줘서 이번에 한번 사용해봤다.


## Code
```python
import heapq

def solution(n, works):
    answer = 0
    works = [-w for w in works]
    heapq.heapify(works)
    for i in range(n):
        c = heapq.heappop(works)
        if c == 0:
            break
        heapq.heappush(works, (c + 1))
    else:
        for w in works:
            answer += (w**2)
    return answer
```

## 후기
오랜만에 1트에 통과한 문제이다. 
계속 자잘한 실수 및 예외 케이스를 고려하지 못하고 틀리는 경우가 많았는데
접근을 잘하여 한번에 통과할 수 있어서 뿌듯하다.