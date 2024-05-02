---
title: "[Algorithm] 프로그래머스 n^2 배열 자르기"
excerpt: "월간 코드 챌린지 도전! n^2 배열 자르기 문제"
category :
  - Algorithm
tag :
  - Algorithm
  - String
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: n^2 배열 자르기

## 문제 링크
[n^2 배열 자르기](https://school.programmers.co.kr/learn/courses/30/lessons/87390)

## 풀이
처음에는 그림이 너무 잘그려져있길래 그림따라 전체 배열을 만들고 뽑아내는 형태로 구현하느라 시간 초과가 났다.
이후에는 규칙을 따라 일부분만 고

### 규칙 설명
- 1 2 3 4 ... N 1행이라면 다음행은
- 2 2 3 4 ... N 그 다음행은
- 3 3 3 4 ... N 이제 다들 규칙을 찾았을 것이라고 생각한다
n행 일경우에는 앞부분이 n이 n개 있고 n+1부터 N까지 뒤에 있다는 점이다.

하지만 다음 밑에와 같은 예외케이스를 고려하지 못해 2, 15~20에 테스트 케이스를 통과하지 못했다.

### 예외케이스 설명
[2, 15~20 테스트 케이스 예시](https://school.programmers.co.kr/questions/55575)
- solution(3, 3, 4)
- answer = [2, 2]
__left right가 같은 행에__ 있을 경우를 고려하지 않은 것이다. 

## Code
```python
def solution(n, left, right):
    answer = []
    make_row = [i for i in range(1, n+1)]
    l_r, l_c = left // n, left % n
    r_r, r_c = right // n, right % n
    for i in range(l_r+1, r_r+2):
        temp = [i] * i
        temp += make_row[i:]
        if (l_r + 1) == i:
            if (r_r + 1) == i:
                answer += temp[l_c:r_c+1]
            else:
                answer += temp[l_c:] # 이것만 할경우 test 2, 15~20 통과 못함
        elif (r_r + 1) == i:
            answer += temp[:r_c+1]
        else:
            answer += temp
    return answer
```

## 후기
그림에 현혹되서 그대로 구현하다가 시간초과가 났는데 그렇게 난이도가 높은 문제는 아닌것으로 보인다.
다만 혼자 예외케이스를 생각하는 능력을 길러야할 것 같다.