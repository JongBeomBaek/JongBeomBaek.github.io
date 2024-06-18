---
title: "[Algorithm] 프로그래머스 합승 택시 요금"
excerpt: "2021 KAKAO blind recruitment 합승 택시 요금"
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

# 프로그래머스: 합승 택시 요금

## 문제 링크
[합승 택시 요금](https://school.programmers.co.kr/learn/courses/30/lessons/72413)

## 풀이
해당 문제를 보면서 두 알고리즘의 조합이 떠올랐다.
최단거리를 구하는 다익스트라,
노드를 거쳐갔을때 비용을 알 수 있는 플로이드 와샬 알고리즘이다.
이전에 푼 문제들을 링크를 남겨놓았으니 참고하시길 바랍니다.


### 참고하면 좋을 문제
다익스트라: [가장 먼 노드](https://jongbeombaek.github.io/algorithm/programmers-Furthest_node/)
플로이드 와샬: [순위](https://jongbeombaek.github.io/algorithm/programmers-Ranking/)

### 코드설명
- 첫번째 while 문
    다익스트라 알고리즘으로 시작하는 s 노드에서 다른 모든 노드들의 최단 거리비용을 알 수 있다. 
    다만 이전 [가장 먼 노드](https://jongbeombaek.github.io/algorithm/programmers-Furthest_node/) 문제와 다른점은
    edge에 비용이 동일하지 않음으로 이후의 나온 조합이 최단거리일 수있다.
    - if 문 
        비용이 입력되지 않은 경우로 값을 업데이트합니다.
    - else 문
        이후 나온 경로이지만 edge가 동일한 값이 아님으로 최단거리 일 수있다.
        그 경우 값을 업데이트한다.
- 두번째 while 문
    이문제는 

## Code
```python
import heapq

def solution(n, s, a, b, fares):
    G = [[] for _ in range(n)]
    for c, d, f in fares:
        G[c-1].append([f, d-1])
        G[d-1].append([f, c-1])
    
    cost_map = [[-1, []] for _ in range(n)]
    cost_map[s-1] = [0, [s-1]]
    que = [[0, s-1, [s-1]]]
    while que:
        cur_cost, cur_node, route = heapq.heappop(que)
        for cost, nxt_node in G[cur_node]:
            if cost_map[nxt_node][0] == -1:
                cost_map[nxt_node][0] = cur_cost + cost 
                cost_map[nxt_node][1] = route + [nxt_node]
                heapq.heappush(que, [cur_cost + cost, nxt_node, route + [nxt_node]])
            else:
                if cur_cost + cost < cost_map[nxt_node][0]:
                    cost_map[nxt_node][0] = cur_cost + cost 
                    cost_map[nxt_node][1] = route + [nxt_node]
                    heapq.heappush(que, [cur_cost + cost, nxt_node, route + [nxt_node]])
    
    answer = cost_map[a-1][0] + cost_map[b-1][0]
    for i in range(n):
        if i == s-1:
            continue
        
        pre_cost = cost_map[i][0]
        cost_map2 = [[-1, []] for _ in range(n)]
        cost_map2[s-1] = cost_map[i]
        cost_map2[i] = [0, [i]]
        que = [[0, i, [i]]]
        while que:
            cur_cost, cur_node, route = heapq.heappop(que)
            for cost, nxt_node in G[cur_node]:
                if cost_map2[nxt_node][0] == -1:
                    cost_map2[nxt_node][0] = cur_cost + cost 
                    cost_map2[nxt_node][1] = route + [nxt_node]
                    heapq.heappush(que, [cur_cost + cost, nxt_node, route + [nxt_node]])
                else:
                    if cur_cost + cost < cost_map2[nxt_node][0]:
                        cost_map2[nxt_node][0] = cur_cost + cost 
                        cost_map2[nxt_node][1] = route + [nxt_node]
                        heapq.heappush(que, [cur_cost + cost, nxt_node, route + [nxt_node]])
        
        if cost_map2[a-1][0] == -1 or cost_map2[b-1][0] == -1:
            continue
        
        all_cost = pre_cost + cost_map2[a-1][0] + cost_map2[b-1][0]
        if all_cost < answer:
            answer = all_cost
    return answer
```

## 후기
해당 알고리즘에 반복문이 많아 효율성에서 통과하지 않을 줄 알았는데 다행이 통과하였다.
내 알고리즘의 시간복잡도가 궁금하여 Chat GPT한테 물어봤다.
결론부터 말하자면 *O(n⋅(n+m)logn)* 라고 한다.
### Chat GPT 시간 복잡도
The given code solves a shortest path problem in a weighted undirected graph. To compute the time complexity, let's break down the main components of the code:

1. Graph Construction:
```python
G = [[] for _ in range(n)]
for c, d, f in fares:
    G[c-1].append([f, d-1])
    G[d-1].append([f, c-1])
```
Constructing the adjacency list takes *O(m)* time, where *m* is the number of edges.

2. Dijkstra's Algorithm Implementation:
The code uses a modified Dijkstra's algorithm to compute the shortest paths from a source node *s* to all other nodes.
```python
cost_map = [[-1, []] for _ in range(n)]
cost_map[s-1] = [0, [s-1]]
que = [[0, s-1, [s-1]]]
while que:
    cur_cost, cur_node, route = heapq.heappop(que)
    for cost, nxt_node in G[cur_node]:
        if cost_map[nxt_node][0] == -1:
            cost_map[nxt_node][0] = cur_cost + cost 
            cost_map[nxt_node][1] = route + [nxt_node]
            heapq.heappush(que, [cur_cost + cost, nxt_node, route + [nxt_node]])
        else:
            if cur_cost + cost < cost_map[nxt_node][0]:
                cost_map[nxt_node][0] = cur_cost + cost 
                cost_map[nxt_node][1] = route + [nxt_node]
                heapq.heappush(que, [cur_cost + cost, nxt_node, route + [nxt_node]])
```
For a graph with *n* nodes and *m* edges, the time complexity of Dijkstra's algorithm using a priority queue (min-heap) is *O((n+m)logn)*.

3. Iterating Over Intermediate Nodes:
The code iterates over each node *i* (excluding the source node *s*) to consider it as an intermediate point and recalculates the shortest paths using Dijkstra's algorithm again.

```python
for i in range(n):
    if i == s-1:
        continue
    
    pre_cost = cost_map[i][0]
    cost_map2 = [[-1, []] for _ in range(n)]
    cost_map2[s-1] = cost_map[i]
    cost_map2[i] = [0, [i]]
    que = [[0, i, [i]]]
    while que:
        cur_cost, cur_node, route = heapq.heappop(que)
        for cost, nxt_node in G[cur_node]:
            if cost_map2[nxt_node][0] == -1:
                cost_map2[nxt_node][0] = cur_cost + cost 
                cost_map2[nxt_node][1] = route + [nxt_node]
                heapq.heappush(que, [cur_cost + cost, nxt_node, route + [nxt_node]])
            else:
                if cur_cost + cost < cost_map2[nxt_node][0]:
                    cost_map2[nxt_node][0] = cur_cost + cost 
                    cost_map2[nxt_node][1] = route + [nxt_node]
                    heapq.heappush(que, [cur_cost + cost, nxt_node, route + [nxt_node]])
    
    if cost_map2[a-1][0] == -1 or cost_map2[b-1][0] == -1:
        continue
    
    all_cost = pre_cost + cost_map2[a-1][0] + cost_map2[b-1][0]
    if all_cost < answer:
        answer = all_cost
```
Here, Dijkstra's algorithm is run *n−1* times (once for each possible intermediate node).

4. Overall Time Complexity:
- Constructing the graph: *O(m)*
- Initial run of Dijkstra's algorithm: *O((n+m)logn)*
- Iterating over each node and running Dijkstra's algorithm *n−1* times: *(n−1)⋅O((n+m)logn)*

Thus, the total time complexity is: *O(m)+O((n+m)logn)+(n−1)⋅O((n+m)logn)=O(n⋅(n+m)logn)*
Therefore, the overall time complexity of the given code is *O(n⋅(n+m)logn)*.