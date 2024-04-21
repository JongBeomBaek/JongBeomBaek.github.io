---
title: "[Algorithm] 프로그래머스 가장 큰 수"
excerpt: "정렬 문제인 가장 큰 수 문제를 풀어보자~"
category :
  - Algorithm
tag :
  - Algorithm
  - Sorting
toc : true
toc_sticky: true
comments: true
---

# 프로그래머스: 가장 큰 수

## 문제 링크
[가장 큰 수](https://school.programmers.co.kr/learn/courses/30/lessons/42746)

## 풀이
처음에는 접근을 문자열로 변환하고 sorting하면 사전순으로 나열했지만
2번째 테스트 케이스에서 [3, 30, 34] > [34,30,3] 으로 정렬이 되어 답이 될 수 없었다.
그래서 이참에 직접 sorting을 짜보는걸 오랜만에 해보자는 마음으로 merge sort를 직접짜봤다.
다통과하는데 계속 case 11번이 통과못하는데 [0,0,0] -> 000으로 오답으로 처리된 것이다.
마지막에 테스트 케이스 11번을 통과못한 경우는 약간 억까 당한 느낌이... 든다..

## Code
```python
def compare_str_num(a, b): 
    if a+b <= b+a:
        return True
    else:
        return False
    
def merge_sort(arr):
    LEN = len(arr)
    if LEN <= 1:
        return arr
    elif LEN == 2:
        if compare_str_num(arr[0], arr[1]):
            arr.reverse()
        return arr
    else:
        m = (0 + LEN) // 2
        f_it = 0
        b_it = 0
        F_list = merge_sort(arr[0:m])
        B_list = merge_sort(arr[m:])
        temp_list = []
        while f_it < len(F_list) and b_it < len(B_list):
            if compare_str_num(F_list[f_it], B_list[b_it]):
                temp_list.append(B_list[b_it])
                b_it += 1
            else:
                temp_list.append(F_list[f_it])
                f_it += 1
        if f_it < len(F_list):
            temp_list += F_list[f_it:]
        if b_it < len(B_list):
            temp_list += B_list[b_it:]
        return temp_list    

def solution(numbers):
    numbers_str = list(map(str, numbers))
    # return ''.join(merge_sort(numbers_str)) # [0,0,0] -> 000이 오답임 case 11번 경우
    return str(int(''.join(merge_sort(numbers_str))))
```


## 후기
문제의도에 맞게 푼것 인지는 잘 모르겠지만 merge sort를 상기시켜 구현해보는 좋은 경험을 해본 것 같다.
 
3을 최대길이에 맞춰 3333으로 해서 sort 내장 함수를 써보는 풀이법을 적용해보려고 했으나 
몇 케이스테이스에서 통과를 못해서 
아마 [34, 3444] > [[3444, 34], [3444, 3444]] 이런게 문제가 될것으로 보인다.
더이상 생각하기 귀찮아서 그냥 merge sort 구현으로 풀었다.

```python
# 53.3점 짜리 풀이
def solution(numbers):
    numbers_str = list(map(str, numbers))
    max_len = len(str(max(numbers)))
    str_list = []
    for n_str in numbers_str:
        for_sort = n_str + n_str[-1]*(max_len - len(n_str))
        str_list.append([for_sort, n_str])
    
    str_list.sort(reverse=True)
    ans =''
    for s in str_list:
        ans += s[1]
    
    return ans
```
