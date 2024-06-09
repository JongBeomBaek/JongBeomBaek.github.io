---
title: "[Algorithm] 프로그래머스 연속 펄스 부분 수열의 합"
excerpt: "연습문제 연속 펄스 부분 수열의 합"
category :
  - Algorithm
tag :
  - Algorithm
  - DP
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 연속 펄스 부분 수열의 합

## 문제 링크
[연속 펄스 부분 수열의 합](https://school.programmers.co.kr/learn/courses/30/lessons/161988)

## 풀이
처음에는 문제를 이해는데 너무 어려웠다..(나만 그런줄 알았는데 스터디원들도 똑같이 이해하기 어려웠다고함...ㅋㅋㅋㅋ)
문제 설명을 해보자면 수열이 있는데 펄스 수열은 [1, -1, 1, ..] or [-1, 1, 1, ..] 로 이루어진 수열이다 두수열의 곲으로 이루어진 수열을
연속 펄스 *수열은 수열과 펄스 수열을 곱한 것* 이라고 보면된다.
그중 일부분인 부분집합 수열을 **연속펄스 부분수열** 이라고 생각하면된다.

### 코드설명
먼저 펄스수열이 두가지 임으로 두종류의 펄스 수열을 구한다.
그래서 cur_val에 다음 값을 더한 것 (경우 1)과 다음값 그자체(경우2)와 비교했을때 더 큰 값을 
cur_val 에 업데이트한다.
- 다음값 + cur_val이 경우 (1)
- 다음값 그 자체가 더 큰 경우 (2) 
그 매 순간 순간마다 cur_val은 업데이트 될때 값이 두 선택지중에 최선임으로 그값이 max값인지 확인한다.
쉽게 요약하자면
**최대값 찾기에서 부분 집합의 합이 현재 값 자체보다 큰지 작은지로 현재값이 정해지는 조건만 추가된것 이라고 보면 된다.**

## Code
```python
def solution(sequence):
    answer = sequence[0]
    seq_len = len(sequence)
    p_seq_con = [(-1 if i % 2 else 1) * sequence[i] for i in range(seq_len)]
    p_seq_inv = [(1 if i % 2 else -1) * sequence[i] for i in range(seq_len)]
    cur_val = [0, 0]

    for i in range(seq_len):
        cur_val[0] += p_seq_con[i]
        cur_val[1] += p_seq_inv[i]
        
        if cur_val[0] < p_seq_con[i]:
            cur_val[0] = p_seq_con[i]
        if cur_val[1] < p_seq_inv[i]:
            cur_val[1] = p_seq_inv[i]
        if max(cur_val) > answer:
            answer =  max(cur_val)
    return answer
```

## 후기
사실 두 펄스는 절대값으로 보면 같기 때문에 그걸 고려해서 하나만 만들어서 해보려고 했다.
하지만 예외를 찾지못해서 편하게 두개로 나누어서 풀었다.