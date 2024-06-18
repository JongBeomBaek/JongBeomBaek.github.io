---
title: "[Algorithm] 프로그래머스 스티커 모으기(2)"
excerpt: "Summer/Winter Coding(~2018) 스티커 모으기(2)"
category :
  - Algorithm
tag :
  - Algorithm
  - DP
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 스티커 모으기(2)

## 문제 링크
[스티커 모으기(2)](https://school.programmers.co.kr/learn/courses/30/lessons/12971)

## 풀이
circular queue와 같이 원형으로 이루어진 스티커들이 있다.
하나의 스티커를 떼어 내면 양옆에 스티커는 떼어낼 수 있다.
그러한 조건으로 스티커를 떼어낼 때 합이 최대 조합이 되는 경우를 출력하는 문제이다.

### 참고하면 좋은 사이트
풀이를 보기전에 참고를 통해 혼자 풀고싶으시다면 해당 사이트를 보시는걸 추천드립니다.
- [https://school.programmers.co.kr/questions/53853]
- [https://school.programmers.co.kr/questions/24769]

### 코드설명
먼저 스티커 개수에 따라 문제를 다르게 풀었다.
- 1개일 경우
    한개 있는 값 출력
- 2개일 경우
    둘 중 최대 값 출력
- 3개 이상의 경우
    첫번째껄 선택한 경우를 고려하여 맨뒤의 원소는 문제조건으로 인해 제외하고 계산한다.
    두번째껄 선택한 경우는 뒤에 모든 원소를 포함하여 계산한다. 
    - i == 1
        이전 값(index 0) 과 비교했을때 최대값을 고른다.
    - i > 1
        (i-1) 값 자체와 (i-2) + (i) 값중 큰 값을 현재(i) 값에 최대 조합으로 넣는다.
    
이렇게 풀다보면 현재기준 선택할 수 없는 인접 스티커(i-1)의 최대 조합과 i-2의 최대 조합을 모두 고려하면서 하기때문에
답을 구할 수 있다.

여기서 궁금한 점은 그럼 첫번째랑 두번째를 나눈 경우가 무엇이냐 
문제 조건으로 마지막 혹은 첫번째 스티커를 고려할 수 있는지 여부이다.

### 유사 문제 
[도둑질](https://school.programmers.co.kr/learn/courses/30/lessons/42897) | [이전풀이](https://school.programmers.co.kr/learn/courses/30/lessons/42897)
문제를 보면 거의 풀이가 동일한걸 볼 수 있다.


## Code
```python
def solution(sticker):
    len_sticker = len(sticker)
    if len_sticker == 1:
        return sticker[0]
    elif len_sticker == 2:
        return max(sticker)
    else:
        DP = sticker[:-1].copy()
        for i in range(1, len_sticker-1):
            if i == 1:
                DP[i] = max(DP[i], DP[i-1])
            else:
                DP[i] = max((DP[i-2] + DP[i]), DP[i-1])
        answer = DP[-1]
        DP = sticker[1:].copy()
        for i in range(1, len_sticker-1):
            if i == 1:
                DP[i] = max(DP[i], DP[i-1])
            else:
                DP[i] = max((DP[i-2] + DP[i]), DP[i-1])
        return max(answer, DP[-1])
```

## 후기
문제를 보는순간 이전에 본거같은데 라는 생각이 들었다.
3월에 같이 스터디하면서 푼 도둑질 문제와 거의 동일한 문제였다. 
그럼에도 불구하고 힌트 없이 풀 수가 없었다..
DP는 확실히 취약한것 같다.