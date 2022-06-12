## **IPv4 프로토콜(3 계층)**

하는 일 : 네트워크 상에서 데이터를 교환하기 위한 프로토콜

데이터가 **정확하게 전달될 것을 보장하지는 않는다.**

데이터의 정확하고 순차적인 전달은 그보다 상위 프로토콜인 (4 계층) TCP에서 보장합니다.

여기서는 멀리 있는 곳에게 전달만 한다.!



IPv4 프로토콜의 구조

다른 네트워크의 특정 대상을 찾는 IPv4 프로토콜(20바이트)

![img](https://blog.kakaocdn.net/dn/cEICOi/btrEw8Moome/xXtzxAo0va073VsURWjhn0/img.png)

Source Address출발지 Ip주소(4바이트)

Destination Address 목적지 Ip주소(4바이트)

Version = IPv4->이니 Version 4(4비트)

IPv6도 있는데 왜 4만 오느냐 6은 아예 구조가 다르기 때문에 Version이라는 곳에는 4만 옵니다. 원래는 확장성 있게 개발하려 했으나 IPv6를 가면서 구조가 확 달라져서 확장성 있게 사용이 불가능 해졌습니다.

IHL(HeaderLength) 4비트뿐인데 최대 15 길이만 나타날 수 있는데 IPv4는 필수로 20바이트를 가지고 옵션이 붙어서 최대 60바이트 까지 사용할 수 있게 되는데 어떻게 길이를 나타내는가? -> 이것은 20바이트를 나타낸다면 4로 나누어 나타나게 됩니다. 20일 경우 -> 5 

TOS의 경우 예전에 사용했다가 지금은 사용은 안 하므로 0으로 빈 값으로 나타냅니다.

Total Length ->전체의 길이 

Identification , IP Flags, Fragment Offset은 하나의 Set입니다.

데이터가 큰 것을 보낼 때 잘게 잘게 보내게 되는데 쪼개진 애들을 알아보기 위한 값.

Identification : 쪼개진 여러 개의 패킷들이 원래는 하나의 큰 데이터였다는 것을 하기 위해 여러개의 패킷들에게 동일한 ID값을 부여하는 개념

IP Flags : 패킷을 쪼개면서 보내질 때 뒤에 쪼개진 값들이 더 있다고 알려주는 값.

Fragment Offset : 패킷을 쪼개면서 나타나는 순서에 대한 값입니다.

Protocol : 상위 프로토콜이 무엇인지 알려주는 값입니다.(TCP, UDP, ICMP(3 계층))

Header Checksum : 전송된 데이터그램의 오류를 탐지하여 정정합니다. 



## **ICMP프로토콜**

하는 일 : 네트워크 컴퓨터 위에서 돌아가는 운영체제에서 오류 메시지를 전송받는데 주로 쓰이게 됩니다.

상대방과 통신이 되나 안 되나 확인하는 프로토콜..



특정 대상과 내가 통신이 잘되는지 확인하는 **ICMP 프로토콜**

![img](https://blog.kakaocdn.net/dn/XBN4f/btrEu8zQOHK/MmGKTyCoD2kknQfqVkFDj0/img.png)

Type : 대분류의 느낌 

8-> 요청 , 0 -> 응답 

Code : 소분류.

Type Code 0. Echo Reply:요청에 대한 응답

Type Code 8. Echo: 요청

 **Type Code3.Destination Unreachable** : 목적지에 도달하지 못함

**Type Code 11.Time Exceeded** : 시간이 오래 걸려 목적지에 도달하지 못함





3 계층에 있는 icmp 프로토콜 Ipv4프로토콜 한 패킷 안에 동시에 존재할 수 있는가 ->

패킷을 만들 때 한 계층에 하나의 프로토콜만 서야 한다는 규칙은 없습니다. 각 프로토콜의 계층을 나눈 것은 그 프로토콜의 역할에 따라서 계층이 나눠진 것이에요. 그래서 ICMP는 통신을 확인하는 역할, IPv4는 멀리 찾아가기 위한 역할, Ethernet은 가까운 곳을 찾아가기 위한 역할로 나눠졌을 뿐 같은 계층에 있는 프로토콜이 겹친다고 해서 문제가 되는 건 아닙니다.



## **라우팅 테이블 및 전송 과정**

어디로 보내야 하는지 설정되어 있는 라우팅 테이블

라우팅 테이블 : 다른 네트워크 대역을 찾아가는 지도구나 라는 개념.

![img](https://blog.kakaocdn.net/dn/bhU7me/btrEwkzAq57/Uk8VF0irX1wAKenNxNHxEk/img.png)

A와 B와 통신한다고 가정해서 시작하겠습니다.

먼저 A의 라우팅 테이블(지도)에

![img](https://blog.kakaocdn.net/dn/n1qLw/btrExXJ0H8C/RVJ3Nm8hT7NuoHkcBaz2W0/img.png)

B의 네트워크 대역인 192.168.20.0/24의 값이 존재해야 통신이 가능합니다. (모르면 못 간다)

먼저 ICMP로 통신이 되는지 확인만 먼저 해보겠습니다.

![img](https://blog.kakaocdn.net/dn/YiHvM/btrEAzWBKzu/gYWB8vokmE7Nm72V1j7461/img.png)

이렇게 패킷을 감싸고 시작을 해보겠습니다. 

Eth의 목적지 주소는 MAC: ccccccc입니다. 

우리의 최종 목적지가 B라서 mac: bbbbb인 것 같지만 이더넷의 경우 가까운 곳과 통신하는 것이 목적입니다.

그리고 A의 라우팅 테이블을 볼 때 192.168.20.0/24의 네트워크 대역은 192.168.10,1 은 같은 네트워크 대역의 게이트 웨인 Mac:ccccc입니다. 

한번 그래서 A가 스위치에게 보내면 스위치는 2계 층만 확인을 하여 이더넷을 보고 MAC가 cccc로 보내게 됩니다.

이제 패킷을 받아보고 Eth를 봤을 때 Mac:ccc인 것을 보고 자신에게 왔다는 것을 확인하고 IPv4를 볼 때 이건 자신에게 보낸 것이 아니므로 자신의 라우팅 테이블을 확인하게 됩니다. 자신의 라우팅 테이블을 볼 때 

![img](https://blog.kakaocdn.net/dn/NUAYu/btrEupHY7KO/cez6QzM5npmmV2ZgiOtGa0/img.png)

192.168.30.2(라우터)로 가야 하므로

다시 이더넷의 패킷을 다시 수정해서 보내게 됩니다. 또 라우터는 확인하고 mac주소를 확인하고 Ipv4가 자신이 아니란 걸 확인하고 또 패킷을 수정하여 보내게 됩니다. 그리고 B의 네트워크 대역에 들어왔을 때 게이트웨이는 이제 Mac 주소를 bbb로 바꾸고 보내게 됩니다. 그리하여 B는 받아보고 이더넷과 Ipv4를 볼 때 자신에게 왔다는 것을 확인하고 그대로 ICMP응답을 다시 만들어 보내게 됩니다.! 위의 과정을 그대로 반복하는 개념.