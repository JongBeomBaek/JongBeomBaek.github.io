---
title: "[Algorithm] 프로그래머스 괄호 회전하기"
excerpt: "월간 코드 챌린지 도전! 괄호 회전하기 문제"
category :
  - Algorithm
tag :
  - Algorithm
  - Stack
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 괄호 회전하기

## 문제 링크
[괄호 회전하기](https://school.programmers.co.kr/learn/courses/30/lessons/76502)

## 풀이
아마 학부시절 계산기 구현하다보면 stack 자료구조를 사용 했던 기억이 다들 있으실 것이라고 생각한다. 
- 괄호를 여는 연산은 스택에 쌓기
- 괄호를 닫는 연사는 스택에서 원소를 빼와 비교함
- 스택에 남아있는 원소가 있는지 확인(테스트 케이스 13번) 있으면 괄호가 닫힌게 아님

## Code
```python
def solution(s):
    answer = 0
    stack = []
    
    for i in range(len(s)):
        s_q =  s[i:] + s[:i]
        FLAG = True
        for s_  in s_q:
            if s_ == ')':
                if len(stack) > 0:
                    f = stack.pop()
                    if f != '(':
                        FLAG = False
                        break
                else:
                    FLAG = False
                    break
            elif s_ == '}':
                if len(stack) > 0:
                    f = stack.pop()
                    if f != '{':
                        FLAG = False
                        break
                else:
                    FLAG = False
                    break
            elif s_ == ']':
                if len(stack) > 0:
                    f = stack.pop()
                    if f != '[':
                        FLAG = False
                        break
                else:
                    FLAG = False
                    break
            else:
                stack.append(s_)
        #len(stack) > test 13 괄호가 온전히 다 닫혀있으면 stack 길이가 0
        if FLAG and len(stack) == 0:
            answer += 1
    
    return answer
```

## 후기
자료구조 수업을 들으면서 계산기를 만들어본 사람들은 쉽게 풀었을 문제라고 생각 되어진다.