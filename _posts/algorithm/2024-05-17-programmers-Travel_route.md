---
title: "[Algorithm] 프로그래머스 여행경로"
excerpt: "알고리즘 kit 깊이/너비 우선 탐색(DFS/BFS) 여행경로"
category :
  - Algorithm
tag :
  - Algorithm
  - DFS
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 여행경로

## 문제 링크
[여행경로](https://school.programmers.co.kr/learn/courses/30/lessons/43164)

## 풀이
오랜만에 dfs를 복습할 수 있는 좋은 문제였다.
인천("ICN")이 시작점이기에 앞으로 여행지가 붙을 일은 없다.
처음에는 루트를 sorting하고 나서하면 sorting된 순서대로 경로가 생성되지 않을까 하고 도전하였지만
계속 정답과 다르게 나오거나 생성할 수 없는 경로로 나오길래 모든 가능한 후보군을 넣고 정렬할 뒤 맨앞 경로를 넣었다.


### 코드설명
나라를 방문한 경우 vis원소가 false, 모든 나라를 방문했을경우 vis list는 false로만 되어있기 때문에 dfs 탈출조건으로
다음과 같이 true 원소가 있는지를 검사하는것으로 하였다.
방문 할 수 있는 나라들일 경우 내지금 도착지점 cand[-3:] (문자열에서 끝 세글자)과 일치하는지 보고 연결한 여행경로를 다음
dfs 함수에 입력으로 넣으면서 찾아나간다.

- answer 길이가 0인 경우
    = 가능한 후보군이 없는 경우 none 출력
- answer 길이가 1 이상인 경우 
    여러가지 후보군 중 가장 사전순으로 빠른 경로를 출력


dfs 함수 뒷부분은 문자열로 sorting한 뒤(사전순 정렬) 3개씩 끊어서 출력해주는 역할을 한다.

## Code
```python
def dfs(cand, vis, tickets):
    if True in vis:
        answer = []
        final = cand[-3:]
        for idx, flag in enumerate(vis):
            if flag:
                a, b = tickets[idx]
                if final == a: 
                    vis[idx] = False
                    temp = dfs(cand + b, vis, tickets)
                    vis[idx] = True
                    if not temp == None:
                        answer.append(temp)
        answer.sort()
        if len(answer) > 0:
            return answer[0]
        else:
            return None
    else:
        return cand

def solution(tickets):
    vis = [True for i in range(len(tickets))]
    answer_str = dfs('ICN', vis, tickets)
    answer = []
    for i in range(0, len(answer_str)-1, 3):
        answer.append(answer_str[i:i+3])
    return answer
```

## 후기
처음에는 ICN 이 시작인 조건을 안보고 앞뒤로 붙일 수 있는 코드를 작성하여 실패하였다.... (역시 문제는 꼼꼼히 읽기...)
이외에도 스터디원들의 코드를 보면 중간중간 sorting을 섞어서하는 코드가 있는데 시간이 남을 경우 비교해봐야겠다.