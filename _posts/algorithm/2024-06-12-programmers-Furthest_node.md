---
title: "[Algorithm] 프로그래머스 가장 먼 노드"
excerpt: "코딩테스트 연습 가장 먼 노드"
category :
  - Algorithm
tag :
  - Algorithm
  - Graph
  - PiroirtyQueue
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 가장 먼 노드

## 문제 링크
[가장 먼 노드](https://school.programmers.co.kr/learn/courses/30/lessons/49189)

## 풀이
문제를 보면서 느낀건 이전에 네비게이션 수업에서 배운 다익스트라 알고리즘이 생각이 났다.
다익스트라는 시작점을 정하면 시작점으로부터 다른 모든 노드들의 최단거리 비용을 계산할 수 있는 알고리즘이다.
최단거리에서 기본인 알고리즘으로 공부해두면 다른 개념을 익힐때나 활용할때 유용할 것 같다.

### 코드설명
먼저 맵을 만들기 위해 그래프 G를 선언하고 입력으로 주어진 정보로 맵을 만든다.
시작점인 1번(여기서는 코드 편의상 0번)으로 부터 시작하여 인접한 노드들은 queue에 넣어가며 모든 노드의 최소값들을 계산한다.
동작방식은 너비우선탐색을 생각하면 편하다.
(간선의 길이가 동일한 경우에는 priority queue에서 이후에 나오는 경로가 최단거리일 수 없다.)
- if 문
    최대 값이 되는 경우 최대값을 업데이트한다.
- elif 문
    최대 값과 같은 값을 갖는 노드 개수를 센다.
    최대 괄호문 조건과 priority queue로로인해 동작 성립
- 마지막 for 문
    이후 while문에서 중심이되는 노드 기준으로 주변에 연결된 노드들을 queue에 삽입한다.

## Code
```python
import heapq

def solution(n, edge):
    answer = 0
    G = [[50000, []] for _ in range(n)]
    max_cost_num = [0, 0] #cost & # node
    for e in edge:
        G[e[0] - 1][1].append(e[1] - 1)
        G[e[1] - 1][1].append(e[0] - 1)
    
    que = [[0, 0]] # cost & node index
    G[0][0] = 0
    heapq.heapify(que)
    while que:
        cost, node_idx = heapq.heappop(que)
        if cost > max_cost_num[0]:
            max_cost_num[0] = cost
            max_cost_num[1] = 1
        elif cost == max_cost_num[0]:
            max_cost_num[1] += 1
        for node in G[node_idx][1]:
            if (cost + 1) < G[node][0]:
                G[node][0] = cost + 1
                heapq.heappush(que, [cost + 1, node])
    
    return max_cost_num[1]
```

## 후기
이전에 공부해둔 다익스트라 알고리즘을 알았기에 쉽게 풀 수 있었다.