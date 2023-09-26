---
layout: post
titile: "Ubuntu 16.04 & 18.04 LTS NVIDIA 그래픽 카드 충돌 문제 해결하기"
category :
    - tips
tag :
    - tips
toc : true
toc_sticky: true
comments: true

---

# Ubuntu 16.04 & 18.04 LTS NVIDIA 그래픽 카드 충돌 문제 해결하기~


리눅스를 사용하다보면 대부분의 사람들이 한번쯤을 겪을 만한 

__그래픽카드 드라이버 충돌__ 에 대해서 말씀 드릴려고합니다 ㅎㅎ

요즘 환경설정을 다시 구축하다보니 저와 제가 속해있는 팀에 팀원들도 자주 그래픽 카드가 충돌하는 문제를 겪곤하는데요

__제가 알고있는 이유는 윈도우 업데이트처럼 시스템파일들이 업데이트 되거나 환경설정을 통한 커널 정보가 바뀌게 되면 driver에서 등록된 커널정보와 맞지 않아 깨지는 현상으로 매우 자연스럽게 일어나는 현상으로 알고 있습니다.(업데이트가 보통 재부팅때 반영됨으로 재부팅시에 주로 드라이버가 깨짐)__

그외에도 os를 만드신 토발즈께서도 말씀하셨듯이 사실 nvidia와 리눅스에 호환은 좋지 못합니다 ㅠㅠ..

해당 명령어를 치면
```
nvidia-smi
```

![image](/assets/images/23_4/nvidia_smi.png)

다음과 같이 그래픽카드 정보를 알 수 있는데요
간혹가다 환경설정관련해서 설치하다보면 충돌하는 문제가 생깁니다

예를 들어 cuda 를 설치하다보면
재부팅시 무한 로그인 이 된다거나

```shell
nvidia-smi
```

명령어를 치면

nvidia-smi cannot connect to driver 블라블라 ~ 이런식으로 나오는 경우가 있습니다
이럴경우 그래픽 드라이버를 다시 설치해주어야하는데요
그런데 이전에 있던걸 다시 지우고 설치하는걸 추천드립니다

----------------------

그럼 지우는 것부터 시작해 봅시다.
터미널을 열어봅시다 __(Ctrl + Alt + T)__
만약 무한 부팅 상황이시면 __(Ctrl + Alt + F1) Command Line Mode__ 로 바꾸시면 됩니다 
(아니면 ssh로 접속하셔도 됩니다 ㅎㅎ)


이제 아래의 명령어들을 타이핑 하시면 됩니다.

```shell
sudo nvidia-uninstall
sudo apt-get remove --purge nvidia*
sudo apt autoremove
sudo apt autoclean
```

자이제 다시 설치해 보겠습니다

----------------------

Nvidia graphic driver가 있는 파일로 이동합니다
그리고 다음과 같이 명령어를 실행해 줍니다

```shell
sudo service lightdm stop (16.04만 해당함 18.04는 이부분안하셔도 됩니다!) 
./NVIDIA-Linux-x86_64-440.82.run
```

위에는 저의 그래픽 카드의 맞는 버전(-x86_64-440.82)입니다.
독자님 그래픽 카드에 맞게 사이트에 들어가셔서 다운받은 뒤 명령어만 다르게 하여 설치해주시면 됩니다.

```shell
sudo service lightdm start #(16.04만 해당함 18.04는 이부분안하셔도 됩니다!)
```
를 하시면 그래픽카드가 설치되어 화면 비율이 맞는 모습을 보실 수 있으실 겁니다.

이상으로 마치겠습니다 ㅎㅎㅎ 읽어주셔서 감사합니다.

#nvidia #graphic_card #ubuntu
