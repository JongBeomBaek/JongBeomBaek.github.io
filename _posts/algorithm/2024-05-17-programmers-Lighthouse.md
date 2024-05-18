---
title: "[Algorithm] 프로그래머스 등대"
excerpt: "연습문제 등대"
category :
  - Algorithm
tag :
  - Algorithm
  - DP
  - DFS
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 등대

## 문제 링크
[등대](https://school.programmers.co.kr/learn/courses/30/lessons/12973)

## 풀이
처음에는 Tree임을 활용한 문제로 보여서 최대한 트리의 특성을 활용하려고 하였다
구조가 트리이기는 하지만 root가 어디인지 중요하지도 않고 DP + DFS 문제였다.
해당 문제가 트리 구조인 이유: [프로그래머스 질문](https://school.programmers.co.kr/questions/39516)
n개 노드 n-1이하의 link **모든 노드가 다 연결되어있음!**


### 코드설명
이코드의 핵심은 DP = [[0,1] for _ in range(n)] 이부분이라고 볼 수 있다.
- 내가 불을 끈 경우
    이웃한 노드들 중 하나는 켜야함
- 내가 불을 켠 경우
    이웃이 켜도되고 꺼도된다.
    그 중 최소값은?
이러면서 DP를 밑에서부터 쌓아올리는 구조라고 보면된다 (피보나치 수열처럼)

### sys.setrecursionlimit()
dfs를 하다보면 recursive 구조를 활용하게 된다. 하지만 간혹 깊이 관련 에러를 마주한 경험이 있을 것이다.
해당 함수는 제한을 원하는대로 조정할 수 있는 함수이다.

### defaultdict
dictionary를 만들다보면 list같은경우를 만들때 key값에서 list를 생성하고 있다면 append하고 하는 형태로 
if-else문을 활용할 수 없게 만든다 하지만 defaultdict(자료형)을 할경우 기본으로 새로운 키에 값을 넣을경우에는
해당 자료형으로 생성되는 자료구조라고 보면된다.

## Code
```python
import sys
from collections import defaultdict

sys.setrecursionlimit(10**6)

def solution(n, lighthouse):
    link = defaultdict(list)
    for a,b in lighthouse:
        link[a-1].append(b-1)
        link[b-1].append(a-1)
    visit = [False for _ in range(n)]
    DP = [[0,1] for _ in range(n)] # index 0 = Turn off | index 1 = Turn on

    def dfs(idx, visit, link):
        visit[idx] = True
        for nxt_idx in link[idx]:
            if not visit[nxt_idx]:
                dfs(nxt_idx, visit, link)
                DP[idx][1] += min(DP[nxt_idx][0], DP[nxt_idx][1])
                DP[idx][0] += DP[nxt_idx][1]
    dfs(0, visit, link)
    return min(DP[0][0], DP[0][1])
```

## 후기
아직 DP 구조를 만드는거에 대해서 부족함을 느끼는 문제였다.
(해당 문제는 같이 코딩연습을 하는 친구의 코드를 참고함)
이외에도 defaultdict, sys.setrecursionlimit 와 같이 유용한 함수도 알게 되어서 좋은 시간이였다.