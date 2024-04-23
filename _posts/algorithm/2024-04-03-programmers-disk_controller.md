---
title: "[Algorithm] 프로그래머스 디스크 컨트롤러"
excerpt: "정렬 문제인  디스크 컨트롤러 문제를 풀어보자~"
category :
  - Algorithm
tag :
  - Algorithm
  - Heap
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 디스크 컨트롤러

## 문제 링크
[디스크 컨트롤러](https://school.programmers.co.kr/learn/courses/30/lessons/42627)

## 풀이
앞에서 문제로 푼 [더 맵게](2024-04-03-programmers-more_spicy.md) 에서 힙에 대한 내용을 다뤄
힙에 대한 설명은 생략하도록 하겠다.
이문제는 고려해야할 요소들이 좀 많아서 처음에 어렵게 느껴질 수 있다.
시작시간이 마냥 작은거 위주로 하기에는 나머지가 버리는 시간이 늘어나는 점이 있기에 
**시작시간이 빠르면서, 수행길이가 짧은** 순서로 나열해야하고 현재시간이 지난 시점에서는 *수행길이가 짧은 작업* 먼저 하여
__*다른 작업에 대기시간을 줄여주는데 중점*__ 을 두어야한다
첫 시작은 제일 빨리 시작하는 정렬된 jobs 리스트에서 0번 index를 가져온다.
작업을 수행하고 현재시간은 시작+수행시간을 넣어 시작한다. 
 
while 안에서는 현재시간보다 이전에 시작해야할 작업을 담는다. 
- 있다면 (if): 수행시간이 작은 일을 수행한다.
- 만약 없다 (else): 그중에서 시작시점이 가장 빠른 작업을 처리한다.

## Code
```python
import heapq

def solution(jobs):
    N = len(jobs)
    jobs = sorted(jobs, key=lambda x: (x[0], x[1]))
    idx = [i for i in range(1,N)]
    st, cost = jobs[0]
    cur_time = st + cost

    while len(idx):
        workin = []
        for i, id in enumerate(idx):
            st, c = jobs[id]
            if st < cur_time:
                heapq.heappush(workin, (c, st, i))
            else:
                break
        
        if len(workin):
            c_w, st_w, i = heapq.heappop(workin)
            cost += c_w + max(0, cur_time - st_w)
            cur_time += c_w
            idx.pop(i)
        else:
            st_, c_ = jobs[idx[0]]
            cost += c_
            cur_time = st_ + c_
            idx.pop(0)

    return cost // N
```


## 후기
우선순위가 처음에 정렬된 기준으로 사용되는게 아니라 
상황에 따라 우선순위를 바꿔주어야하는 점에서 다소 어려웠던 문제같다.