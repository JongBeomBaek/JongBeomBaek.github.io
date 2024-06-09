---
title: "[Algorithm] 프로그래머스 광물 캐기"
excerpt: "연습문제 광물 캐기"
category :
  - Algorithm
tag :
  - Algorithm
  - Greedy
  - DFS
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 광물 캐기

## 문제 링크
[광물 캐기](https://school.programmers.co.kr/learn/courses/30/lessons/172927)

## 풀이
Greedy를 풀어본 경험이 적어 greedy 연습차원에서 해당 문제를 골라 풀려고 하였다.
하지만 나의 풀이는 도저히 순간의 최적의 선택 조건을 생각해 내지못해서 DFS로 풀었다....ㅎㅎ
스터디 원이 공유해준 greedy 알고리즘을 참고하고 분석하였는데 한가지 의문이 드는 점이 있어서 글로 남겨봤는데
혹시 이부분에 대해서 의견이 있으시다면 다양한 의견을 댓글로 남겨주시면 감사하겠습니다 :)

곡괭이마다 광물을 캐는 비용이 다르다 다이아의 경우에는 모든게 1
철 곡괭이 경우에는 다이아는 5 철과 돌은 1
돌 곡괭이 경우에는 다이아: 25, 철: 5, 돌: 1 이다.
그랬을 경우 곡괭이 개수를 잘 활용하여 순차적으로 들어오는 광물을 최소 비용으로 처리하는 방법에 대해서 찾는 문제이다.

### 코드설명
#### DFS 풀이
매순간마다 계산을 통해 곡괭이를 선택하지 않고 경우의 수를 모두 고려하여 조합으로 진행한다.
그때 리턴으로 받아온 이후의 조합중 비용이 적은 선택지(min 함수)를 넣어서 return 하는 방식이다.
혹은 end 조건으로 모든 곡괭이를 다쓴 경우 광물이 남아있더라도 비용을 return 한다. (입출력 예시 2번의 경우를 고려한 조건)

#### Greedy 풀이
******
## Code
```python
# DFS (my)
def solution(picks, minerals):
    def DFS(cost, picks, minerals):
        if picks == [0, 0, 0] or minerals == []:
            return cost
        else:
            part = minerals[:5]
            later = minerals[5:] 
            
            costs = [cost, cost, cost]
            for p in part:
                if p == "diamond":
                    costs[1] += 5
                    costs[2] += 25
                elif p == "iron":
                    costs[1] += 1
                    costs[2] += 5
                else:
                    costs[1] += 1
                    costs[2] += 1
                costs[0] += 1
            
            v = []
            if picks[2] > 0:
                picks[2] -= 1
                v.append(DFS(costs[2], picks, later))
                picks[2] += 1
            if picks[1] > 0:
                picks[1] -= 1
                v.append(DFS(costs[1], picks, later))
                picks[1] += 1
            if picks[0] > 0:
                picks[0] -= 1
                v.append(DFS(costs[0], picks, later))
                picks[0] += 1
            return min(v)
    return DFS(0, picks, minerals)

# Greedy (스터디원 코드 공유)
def solution(picks, minerals):
    num_part = len(minerals) // 5 + 1

    mineral_parts = []

    for nn in range(num_part):
        part = minerals[nn*5:(nn+1)*5]
        dd = part.count("diamond")
        ii = part.count("iron")
        ss = part.count("stone")

        mineral_parts.append([dd,ii,ss])
        
    mineral_parts = mineral_parts[:sum(picks)]
    mineral_parts.sort(reverse=True)

    answer = 0

    for part in mineral_parts:
        dd,ii,ss = part
        if picks[0] > 0:
            picks[0] -= 1
            answer += dd
            answer += ii
            answer += ss

        elif picks[1] > 0:
            picks[1] -= 1
            answer += dd*5
            answer += ii
            answer += ss

        elif picks[2] > 0:
            picks[2] -= 1
            answer += dd*25
            answer += ii*5
            answer += ss
    return answer
```

## 후기
Greedy 문제인걸 알았지만 도무지 최소조건을 생각해내지 못해 
모든 경우를 판단하는 DFS로 접근했다 다행히 효율성 체크가 없어서 문제를 통과할 수 있었다.
그래서 스터디원들의 코드를 공유해서 봤을때 다소 의문점이였던건 학교수업에서는
**순간의 선택을 탐욕적으로** 할 경우 **전체적으로 최적의** 선택이라고 하는 점이였다.
그말은 전체를 모르고 하는 선택으로 다가와서 이문제를 풀때 자체적으로 한계를 정하게 된거같다.
(제가 배운 정의가 맞다면 전체를 훑는 건 greedy라 할 수 있을까요?)
