---
title: "[Dev Tips] VS Code ProxyJump"
excerpt: "VS Code ProxyJump: ssh를 우회해서 접속해보자!"
category :
    - Develop Tips
tag :
    - Develop Tips, SSH, VS-Code, ProxyJump
toc : true
toc_sticky: true
comments: true
---

# VS Code ProxyJump
안녕하세요 오랜만에 글을 올리게 되었네요ㅎㅎ 
 
## 문제발생
최근에 제가 학교에서 이용하던 vpn 서비스가 port와 host상관없이 이용가능했는데
보안정책 및 디버깅을 통해 할당한 포트와 호스트만 접속할 수 있게 되었습니다....
(왜 열일하셔서.. 피곤하게 하시는지..)
 
그래서 vim으로 editor를 바꿔야하나 고민을 하던 중
최근에 vs code에서 proxyjump라는 기능을 알게 되었습니다 ㅎㅎ 잡담은 여기까지하고 본론으로 넘어가죠

## vscode ssh 배경지식
vscode를 통해 ssh 원격 접속으로 집에서하는것처럼 끊김없이 code edit을 할 수 있었습니다
그에 대한 설정값은  __[home folder]/.ssh/config__ 폴더에 정보가 저장되어있는데요
([home folder]는 이글을 읽는 여러분들마다 다르겠죠?)
 
여기에 들어가보면 다음과 같이 정보가 적혀있습니다
![img1](/assets/images/23_4/vscode_proxyjump_1.png)

__Host:__ 별칭
__User:__ 접속하려는 컴퓨터의 id 
__HostName:__ 주소 (집주소처럼 위치를 나타내는거겠죠? 번호로 구성되어있지만 ddns를 해놓으면 사람이 읽기편하게 바꿀수있습니다 예를들어 구글과 네이버를 숫자를 입력해서 들어가는게 아닌 naver.com, google.com을 입력해서 들어갈 수 있듯이요 ㅎㅎ)
__Port:__ 집 을 들어가는 문 (집을 들어가는데 여러개의 문이 있지만 통신 규격에따라  문을 따고 들어가야합니다 보통 ssh는 22번을 따릅니다 하지만 라우터나 공유기와같이 중간에서 관리해주는 장치가 있으면 port fowarding을 통해서 컴퓨터마다 구별을 합니다)

이렇게 정보가 구성되어있다면
![img1](/assets/images/23_4/vscode_proxyjump_2.png)

이렇게 왼쪽 배너에 생기고 클릭하여 접속할 수 있습니다

기존적인 설명은 여기까지고 저희가 하려는 걸 설명드릴게요

## 해결방법

지금 문제가되는건 해당되는 저 hostnamer과 port에 따른 할당된 컴퓨터만 접속이 가능하다는 점입니다
코로나로인해 재택을 많이하지만 회사나 학교에서 vpn서비스를 이용한다 했을때 한 컴퓨터를 접속하는 계정만 받았다면 다른컴퓨터를 접속하려면 다른아이디로 접속하거나 신청하는 등 귀찮은 일이 필요하게 되죠..
 
또한 __사실상 터미널로 ssh로 A컴퓨터에 접속하면 B 그리고 같은 내부방에 컴퓨터를 갈 수 있습니다__
(저도 이런점때매 vim으로 갈아타야하나 진지하게 고민했죠..)
 
그치만 vscode도 이런거  알았는지 기능을 제공해줍니다 방법은 매우간단한데요!!
 
집컴을 local로하고 vpn등으로 접속가능한 컴퓨터를 A라고하겠습니다
그리고 저희가 최종적으로 접속할 컴퓨터를 B라고하겠습니다
local > B로 직접적으로 가는건 불가능하지만 터미널로 접속해들어가면 local > A > B가 가능하죠
 
그걸 하기 위해서는 다음과 같이 config파일에 작성해주면됩니다 매우 쉬운데요
![img1](/assets/images/23_4/vscode_proxyjump_3.png)

이렇게 B컴퓨터도 정보에 맞게 입력을 하고
ProxyJump라는 새로운 정보를 기입해주어야하는데요 
이게무엇이냐면 __computer_A를 접속한뒤에 B로 접속하여 위에서 터미널처럼 한것처럼 우회해서 접속하는것 입니다.__

이렇게 해서 접속을 하게되면
![img1](/assets/images/23_4/vscode_proxyjump_4.png)


A컴퓨터의 접속하기 위한 비밀번호를 치는 창이 나오고
![img1](/assets/images/23_4/vscode_proxyjump_5.png)


최종 목표인 B컴퓨터에 접속하기 위한 비밀번호 창이 나옵니다
이렇게 두개를 입력하여 접속하게 된다면
 
기존에 ssh를 하는 방법처럼 자유롭게 사용할 수 있습니다 ㅎㅎㅎ
 
긴글 읽어주시느라 감사합니다 행복한 하루되세요~