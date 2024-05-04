---
title: "[Algorithm] 프로그래머스 짝지어 제거하기"
excerpt: "2017 팁스타운 짝지어 제거하기 문제"
category :
  - Algorithm
tag :
  - Algorithm
  - Stack
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 짝지어 제거하기

## 문제 링크
[짝지어 제거하기](https://school.programmers.co.kr/learn/courses/30/lessons/12973)

## 풀이
생각 없이 문제 설명을 보고 설명과 같이 구현하느라 시간초과가 났다.
하지만 생각해보니 알파벳 쌍이면 사라지는 꼴이 이전 계산기를 구현할때 괄호를 처리하는 **스택(stack)** 자료구조 특성을 활용하면 될것으로 보여졌다.
아래 풀이 코드는 스택을 통해 푼 코드이다.

### 코드설명
- 스택이 비어있을때
    string s에 있는 원소를 push
- 스택이 비어있지 않은 경우
    - 스택 최상단과 push하려는 string s의 원소가 동일한 경우 *제거*
    - 동일 하지 않은 경우 push

### stack을 사용한 이전 풀이
[프로그래머스 괄호 회전하기](https://jongbeombaek.github.io/algorithm/programmers-bracket_rotation/)

## Code
```python
def solution(s):
    stack = []
    it = 0    
    while it < len(s):
        if len(stack) == 0:
            stack.append(s[it])
        else:
            top = stack.pop()
            if not (top == s[it]):
                stack.append(top)
                stack.append(s[it])
        it += 1
    if len(stack) > 0:
        return 0
    else:
        return 1
```

## 후기
이전과 비슷하게 풀이설명에 현혹되서 그대로 구현하다가 시간초과가 났다.
이후에 거기서 최적화를 하느라 계속 시간복잡도가 n^2이여서 시간초과를 해결할 수가 없었는데 고민해보니 stack의 구조면 쉽게 시간복잡도 n으로 풀릴 수 있을거 같았다.
앞으로는.. 문제처럼 따라하여 코드를 구현하여 시간소비하는 바보같은 행동을 안하도록 해야겠다...ㅎㅎ (이번이 2번째)