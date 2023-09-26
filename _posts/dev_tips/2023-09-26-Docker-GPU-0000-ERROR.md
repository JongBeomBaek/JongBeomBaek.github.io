---
title: "[Dev Tips] Docker GPU[0000] ERROR"
excerpt: "Nvidia Docker Error를 해결해보자~"
category :
    - tips
tag :
    - tips
toc : true
toc_sticky: true
comments: true
---

# Docker GPU[0000] ERROR

딥러닝 도커(Nvidia-docker)를 하다보면
![image](/assets/images/23_4/docker_error.png)

__docker: Error response from daemon: could not select device driver "" with capabilities: [[gpu]].__
__ERRO[0000] error waiting for container: context canceled__

이런 에러를 많이 접하게 되실텐데요. [](/_posts/tips/2023-09-18-solve_graphic_card_collision_problem.md)
 
그래픽 카드 드라이버가 깨져서 이런문제가 같이 일어나는걸 보실 수 있습니다.
 
당황하지마시고 터미널에 다음명령어를 차례대로 입력해 주시면 됩니다ㅎㅎ

--------------
### Shell command
```shell
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
 
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
 
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
 
sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
 
sudo systemctl restart docker
```
--------------
### Reference
[Github Issue Link](https://github.com/NVIDIA/nvidia-docker/issues/1034)