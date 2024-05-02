---
title: "[Algorithm] 프로그래머스 이진 변환 반복하기"
excerpt: "월간 코드 챌린지 도전! 이진 변환 반복하기 문제"
category :
  - Algorithm
tag :
  - Algorithm
  - String
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 이진 변환 반복하기

## 문제 링크
[이진 변환 반복하기](https://school.programmers.co.kr/learn/courses/30/lessons/70129)

## 풀이
문자열 함수를 잘 다룰 줄 알면 쉽게 풀 수 있는 문제이다.
### 문자열 함수 설명
- split(STR) 문자열에서 STR 문자열이 있을경우 그걸 기준으로 쪼개서 리스트로 반환해준다.
    ex) str = "110010101001"	
    str.split('0') = ["11", '1', '1', '1', '1']
- 'STR'.join(list) 리스트에 담긴 문자열들을 중간에 STR을 넣으면서 합친다.
    ex) str_list =  ["11", '1', '1', '1', '1']
    '/'.join(str_list) = "11/1/1/1/1"
### 이진수 십진수 변환 방법
- bin(num) 십진수 -> 이진수 변경
    ex) bin(6) = "0b110"
- int(binary_num, 2) 이진수 -> 십진수 변경
    ex) int('0b110', 2) = 6
해당 함수들을 이해하였다면 쉽게 코드를 이해할 수 있을 것이다.

## Code
```python
def solution(s):
    zero_cnt = 0
    it = 0
    nxt_s = s
    while nxt_s != '1':
        zero_cnt += len(''.join(nxt_s.split('1')))
        nxt_s = bin(len(''.join(nxt_s.split('0'))))[2:]
        it += 1
    return [it, zero_cnt]
```

## 후기
파이썬이여서 비교적 쉽게 풀 수 있는 문제였던거같다. (파이썬은 내장함수가 워낙 강력한 것들이 많아서..ㅎㅎ)
그래도 binary 에서 십진수로 변환 하는 과정을 복습해서 좋은 시간이였다.