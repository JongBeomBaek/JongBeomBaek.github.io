---
title: "[Dev Tips] Vscode에서 AWS 서버 접속방법"
excerpt: "vscode에서 원격으로 AWS 접속할때 세팅을 익혀보자"
category :
    - Develop Tips
tag :
    - Develop Tips
    - AWS
    - VSCode
toc : true
toc_sticky: true
comments: true
---

# Vs code에서 AWS 서버 접속

vs code 를 통해 원격 접속은 인터넷에 찾아보면 쉽게 할 수 있다.
하지만 AWS를 사용할경우 .pem 키를 통해 인증을 해야한다.

## 문제점
Vs code를 통해 AWS 서버를 접속하려고 하지만 .pem를 사용하려는 세팅방법을 모른다.

## 해결방법
### VScode에서 접속하는 방법(참고)
config file에서 다음값들을 설정한다.
- Host: 서버 별칭을 지정하는것이다.
- HostName: 각각 집주소가 있드시 접속하려는 컴퓨터의 IP address를 입력해주어야한다.
- User: 접속할때 유저가 다양하게 있을 수도 있고 기본유저 세팅을 다들 했음으로 User ID를 입력해주어야한다.
- port: 보통 ssh 접속은 22번인데 공유기와 같이 IP address 안에서 local 망으로 묶인 경우 port forwarding으로 설정한 port 번호를 입력해주어야한다.

### AWS 접속을 위한 key 세팅
이번 포스팅에서 중요한건 AWS를 접속하기 위한 방법이다
"**IdentityFile**" 이다 이 부분에 .pem 확장자를 가진 파일 경로를 입력해주어야 인증받아 접속할 수 있다.
```shell
Host __Nick_Name__
    HostName __IP_Address__
    User __User_ID__
    port __Port_Number__ #(default: 22)
    IdentityFile __Pem_Key_Path__
```
