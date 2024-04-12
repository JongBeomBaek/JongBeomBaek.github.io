---
title: "[Algorithm] 프로그래머스 완주하지 못한 선수"
excerpt: "해쉬 문제인 완주하지 못한 선수 문제를 풀어보자~"
category :
  - Algorithm
tag :
  - Algorithm
  - Hash
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 완주하지 못한 선수

## 문제 링크
[완주하지 못한 선수](https://school.programmers.co.kr/learn/courses/30/lessons/42576)

## 풀이
난이도를 높여서 다음 문제에 도전하였다.
확실히 오랜만에 저에게는 버거운 문제를 풀다보니 처음 제출당시에는 **timeout이** 발생하였다.
1차 제출당시에 for 문으로 n, remove 함수 n (확실하지는 않지만 n) 그래서 **n^2 에 시간 복잡도**가 나온것 같다.
2번째 제출 sort 함수 n log n  for문 n 최대 n log n 의 복잡도

## Code
```python
# 1차 제출 > 효율성 테스트에서 timeout 뜸
def solution(participant, completion):
    answer = ''
		for c in completion:
        participant.remove(c)
    answer = participant[0]		
		return answer
```
```python
# 2차 제출 (full search를 줄임)
def solution(participant, completion):
    answer = ''
    participant = sorted(participant)
    completion = sorted(completion)
    
    for i in range(len(completion)):
        if participant[i] != completion[i]:
            answer = participant[i]
            break
    
    if answer == '':
        answer = participant[-1]
```

## 후기
파이썬에서 생각없이 사용하던 sort와 같은 함수의 시간복잡도를 알아보는 시간이였다. 