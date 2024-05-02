---
title: "[Dev Tips] VS code 에서 탭키가 안될때"
excerpt: "vscode에서 탭키가 terminal에서 안먹힐 때 해결해보자~"
category :
    - Develop Tips
tag :
    - Develop Tips
    - VSCode
toc : true
toc_sticky: true
comments: true
---

# VS code 에서 탭키가 안될때

## 문제점
프로그래밍을 하다보면 terminal 에서 tab 키를 통해 
자동완성을 해주는 기능을 자주 사용할 것이다.
하지만 어느순간 vim에서 모드가 전환된것처럼 vscode에서 tab키를 누르면 자동완성이 아닌 **다른 것으로 넘어가는 기능으로**
당황스러운 상황을 겪어본 적이 있을 것입니다.

이경우에는 [다른 블로그](https://leeborn.tistory.com/entry/VS-Code-탭키가-작동-하지-않을때) 해당 블로그에서
자세히 설명이 나와있듯이 _포커스를 옮기는_ 기능으로 변경된 것이였다.

## 해결방법
당황하지 마시고 _**"Ctrl + M"**_ 를 동시에 눌러주면 원래 기능으로 돌아간다.

## Reference
[leeborn.tistory](https://leeborn.tistory.com/entry/VS-Code-탭키가-작동-하지-않을때)