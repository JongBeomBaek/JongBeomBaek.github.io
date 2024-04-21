---
title: "[Algorithm] 프로그래머스 H-Index"
excerpt: "정렬 문제인 H-Index 문제를 풀어보자~"
category :
  - Algorithm
tag :
  - Algorithm
  - Sorting
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: H-Index

## 문제 링크
[H-Index](https://school.programmers.co.kr/learn/courses/30/lessons/42747)

## 풀이
난이도를 높여서 그렇게 높은건 아니지만 2 난이도에 정렬 문제를 풀어보려고 한다.
H-Index 라는 것인데 연구하는사람들이라면 아는 내용이다 설명하지면 N번 인용된 논문이 N개 이상있으면
H-Index 는 N인 것이다.
 
처음에는 먼저 정렬을 한뒤 인용수 낮은 논문으로 하나씩 인덱싱해서 낮은 논문의 인용수를 출력으로 하려고 했다.
하지만 H-index를 잘이해하고 있다면 어디가 이상한지 눈치 챘을텐데 [666666, 77777] 이렇게 해도 H-index는 2이라는 점이다
예시 문제로 적은 수가 입력으로 들어와 착각한 것이였다.
 
그래서 최소 인용수를 높여가보면서 그 이상이 되는걸 숫자를 세는식으로 하여 통과하였다.

## Code
```python
def solution(citations):
    citations.sort()
    N = len(citations)
    H_index = 0
    min_cit_idx = 0
    for h in range(1, N+1):
        if citations[min_cit_idx] < h:
            while N > min_cit_idx:
                if citations[min_cit_idx] < h:
                    min_cit_idx += 1
                else:
                    break
        if (N - min_cit_idx) >=  h:
            H_index = h
        else:
            break
    return H_index
```


## 후기
나이를 먹은 건지.. 밤에 졸려서 잘못이해한건지 그렇게 어려운건 아님에도 틀렸다
해당 [Hint](https://school.programmers.co.kr/questions/75471)를 보고 바로
눈치채고 풀 수 있었지만 도움없이 다음에는 풀어보려고 한다.

