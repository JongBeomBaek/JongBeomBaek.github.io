---
title: "[Dev Tips] Window 에서 AWS 접속"
excerpt: "윈도우에서 aws(.pem) 키 권한을 변경해보자"
category :
    - Develop Tips
tag :
    - Develop Tips
    - AWS
    - Window
toc : true
toc_sticky: true
comments: true
---

# Window 에서 AWS 접속
리눅스에서는 파일 권한을 _$ chmod_ 라는 명령어를 통해 편하게 변경할 수 있다. 
하지만 수년간 윈도우를 사용하였음에도 관리자 권한 실행 말고는 디테일하게 권한을 설정하는 방법을 모르고 있었다.
(사실 사용시에도 문제가 없긴하다.)

## 문제점
그러다 AWS .pem 확장자 키를 사용하여 server에 접속하려면 권한을 세부적으로 조정해주어야하는 점이 있다.
이걸 윈도우에서 바꿔주는 방법을 몰라 팀원이 공유해준 명령어를 정리해보려고 한다.

## 해결방법
윈도우에서 cmd를 켜고 pem 키가 있는 위치로 경로를 변경하고 다음 3가지 명령어를 실행하면된다.
(ec2.pem은 예시이며 사용하는 pem키에 맞춰서 변경하여 사용하시길 바랍니다.)
```shell
icacls.exe ec2.pem /reset
icacls.exe ec2.pem /grant:r %username%:(R)
icacls.exe ec2.pem /inheritance:r
```

vs code 접속방법은 다음 링크를 참고하면 된다.
[vscode에서 .pem 키로 서버(aws) 접속](https://jongbeombaek.github.io/develop%20tips/Vscode_setting_for_connect_AwsKey/#aws-접속을-위한-key-세팅)
