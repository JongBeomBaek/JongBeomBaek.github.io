---
title: "[Algorithm] 프로그래머스 전화번호 목록"
excerpt: "해쉬 문제인 전화번호 목록 문제를 풀어보자~"
category :
  - Algorithm
tag :
  - Algorithm
  - Hash
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 전화번호 목록

## 문제 링크
[전화번호 목록](https://school.programmers.co.kr/learn/courses/30/lessons/42577)

## 풀이
해시 문제중 난이도가 어느정도 있는 문제에 도전을 해봤다..
3번에 도전을 하였지만 효율성 테스트에서 절반까지만 통과하고 실패하였다.
 
마지막은 스터디원에 풀이를 추가적으로 넣었다
(짧지만 강력한 코드이다)


## Code (나의 실패한 풀이들..ㅠ)
```python
# 1차 제출 > run time error
def solution(phone_book):
    answer = True
    FLAG = False
    for i in range(len(phone_book)):
        l_i = phone_book[i]
        if FLAG:
            break

        for l_j in phone_book[i+1:]:
            if len(l_i) < len(l_j):
                if l_i == l_j[:len(l_i)]:
                    answer = False
                    FLAG = True
                    break 
            else:
                if l_i[:len(l_j)] == l_j:
                    pdb.set_trace()
                    answer = False
                    FLAG = True
                    break
		return answer
# 이중 반복문만해도 통과되기는 어려워보임
```
```python
# 2차 제출 > 효율성 테스트에서 all timeout 
def solution(phone_book):
    answer = True
		phone_book_sorted = sorted(phone_book, key=lambda x: len(x))
    phone_book_comb = list(combinations(phone_book_sorted, 2))
    for (pb_i, pb_j) in phone_book_comb:
        if pb_i == pb_j[:len(pb_i)]:
            answer = False
            break
    return answer
```

```python
# 3차 제출 > 효율성 테스트에서 2/4 timeout 
def solution(phone_book):
    answer = True
    FLAG = False
		phone_book_sorted = sorted(phone_book, key=lambda x: len(x))
    for i in range(len(phone_book_sorted)):
        if FLAG:
            break
        
        l_i = phone_book_sorted[i]
        for j in range(i+1, len(phone_book_sorted)):
            l_j = phone_book_sorted[j]
            
            if len(l_i) < len(l_j) and l_i == l_j[:len(l_i)]:
                    answer = False
                    FLAG = True
                    break
		return answer
```

```python
# 다른 스터디원의 풀이
def solution(phone_book):
    phone_book.sort()

    for i, num in enumerate(phone_book):
        N = len(num)
        
        if i == len(phone_book)-1:
            break
        
        if num == phone_book[i+1][:N]:
            return False

    return True
```

## 후기
저의 코드를 보았을때 크게 다른점은 sorting을 그냥 **사전적 정의순서로 정렬** 하느냐
아니면 **길이**로 정렬하느냐였다 어찌보면 이 사소한 차이의 접근이 결과를 판가름 하는데 큰 역할을 했다.
길이로 함으로써 길이가 짧은게 긴것들에게 포함되어있느냐를 검사하면서 뒷부분을 모두 검사해야했지만
사전 순의 정렬이면 접두사가 포함된 글자끼리 모여있기 때문에 앞에 일부분만 검사하면 된다.
내장함수 정렬이 사전 순서로 정렬된다는 점을 알 수 있는 시간이였다.