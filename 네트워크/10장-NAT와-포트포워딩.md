## NAT와 포트 포워딩

NAT은 IP 패킷의 TCP/UDP 포트 숫자와 소스 및 목적지의 IP 주소 등을 재기록하면서 라우터를 통해 네트워크 트래픽을 주고받는 기술을 말합니다.

NAT를 이용하는 이유는 대개 사설 네트워크에 속한 여러 개의 호스트가 하나의 공인 IP 주소를 사용하여 인터넷에 접속하기 위함입니다.



실제 일반적인 네트워크의 모습

사설 IP와 공인 IP

![img](https://blog.kakaocdn.net/dn/bSP8xN/btrE9Rh2piw/pCxcJkm8jPe9kcrKD5mcG0/img.png)

인터넷 세상에서 바라본 모습(마치 공유기끼리만 통신하는 모습)

![img](https://blog.kakaocdn.net/dn/nxoC4/btrE5SWLjfk/Jmv09s8IhD77AqLOMbMl01/img.png)









## **포트 포워딩**

패킷이 라우터나 방화벽과 같은 네트워크 장비를 가로지르는 동안 **특정 IP 주소와 포트 번호의 통신 요청을 특정 다른 IP와 포트 번호로 넘겨주는** 네트워크 주소 변환(NAT)의 응용입니다.

![img](https://blog.kakaocdn.net/dn/c0c8Sa/btrE5RXUHv4/GEgG0wJ3dOueJef8hxc5Vk/img.png)

특정 IP의 특정 포트로 온 요청을 포트 포워딩 서로 공유기끼리 설정을 해야 이 기술이 사용 가능합니다.

원래는 공인 IP1에서의 사설 컴퓨터들은 공인 IP2의 웹서버의 존재 유무를 모르지만 포트 포워딩을 통해 존재유무를 알게 되어 접속이 가능합니다.