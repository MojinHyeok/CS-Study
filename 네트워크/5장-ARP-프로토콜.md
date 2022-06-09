ARP 프로토콜

ARP 프로토콜은 같은 네트워크 대역에서 통신을 하기 위해 필요한 MAC 주소를 IP주소를 이용해서 알아오는 프로토콜.



IP주소를 이용해 MAC 주소를 알아오는 ARP 프로토콜.



![img](https://blog.kakaocdn.net/dn/mZ8hD/btrEnvujXDi/3b6HvUDFvWbsLnoZEkUJ8K/img.png)

Source Hardware Address 출발지의 물리적인 주소(MAC주소) 6바이트 

Source Protocol Address 프로토콜 Address 일반적으로 IPv4를 듯합니다. 4바이트

Destination Hardware Address 목적지에 Mac주소가 들어가고

Destination Protocol Address 목적지에 IPv4가 들어옵니다.

이더넷 프로토콜만 목적지만 먼저 오고 나머지 프로토콜의 경우 출발지가 먼저 들어옵니다.

Hardware type 2 계층에서 사용하는 프로토콜을 뜻합니다.(대부분이 이더넷 프로토콜로 뜻합니다.) 

Protocol type 프로토콜 Address의 타입을 뜻합니다. 대부분 IPv4를 뜻함.

Hardware Address length Mac 주소의 길이 6바이트

Protocol Address length IPv4 주소의 길이 4바이트.

Opcode Operation Code -> 어떻게 동작하는지 나타내는 코드 

ARP 프로토콜은 IP주소를 입력하면 Mac 주소를 알아오는 프로토콜 임으로, 프로토콜은 일반적으로 누군가 요청을 하면 응답이 나타납니다.

Opcode의 경우 물어보는지 응답을 하는지 나타내는 코드입니다.

물어보는 경우 1 응답의 경우 2로 세팅을 하는 의미입니다.



이제는 한 번 ARP를 이용하여 어떻게 상대방의 MAC 주소를 알아오는지 한번 봐보겠습니다.

![img](https://blog.kakaocdn.net/dn/bbYPOd/btrEoKYHoLP/96kzGh04aKmt1K3No3kjmk/img.png)

하나의 네트워크 대역으로 가정해봅니다.

같은 LAN대역 

현재는 Mac: aaaa가 Mac :cccc와 통신하고 싶은 상황을 가정해봅니다.

먼저 A 컴퓨터가 상대방에게 요청을 하게 됩니다. ARP 요청 프로토콜을 만들어 보내게 됩니다. 이걸 보낼 때 **캡슐화해서** 보내게 됩니다. ARP의 경우 3 계층이기 때문에 2 계층인 이더넷 프로토콜을 붙여서 보내게 됩니다.

이때는 Opcode를 1로 하여 요청을 하여 보내게 됩니다. 이때 목적지 주소중 Mac 주소는 모르기 때문에 빈 값으로 보내게 됩니다. 여기서 이더넷의 목적지 주소는 **브로드캐스트로(모두에게 보내는 것)**하여 모두에게(같은 네트워크) 보내게 됩니다. 

여기서 모두가 받았을 때 2 계층도 까보고 3 계층도 까 봤을 때 , 3 계층의 경우 목적지 주소로 IPv4가 오기 때문에

자신의 IP랑 비교해서 자신이라면 ARP응답으로 다시 보내고 아니라면 패킷을 버리게 됩니다.

그래서 보낼 때 자신의 출발지 mac주소 ip주소 목적지 mac주소 ip주소를 다 알고 있기 때문에 모두 기입 후 이번에는 다 알고 있기 때문에 굳이 브로드캐스트를 할 필요 없이 바로 A에게 보낼 수 있게 됩니다.



그리고 A가 응답을 받았을 때 ARP 캐시 테이블에 C의 IP주소와 Mac 주소를 기입하여 기억하게 합니다.