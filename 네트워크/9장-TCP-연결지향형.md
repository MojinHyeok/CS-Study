## **연결 지향형 TCP 프로토콜**

연결을 지향하기 때문에 UDP보다는 상대적으로 안전한 프로토콜입니다.

전송 제어 프로토콜(Transmission Control Protocol, TCP)은 인터넷에 연결된 컴퓨터에서 실행되는 프로그램 간에 통신을 **안정적으로, 순서대로, 에러 없이** 교환할 수 있게 한다.

TCP는 연결 지향형이기 때문에 비연결 지향형인 UDP보다 안전하지만 느리다는 점이 있습니다.



안전한 연결을 지향하는 TCP 프로토콜

![img](https://blog.kakaocdn.net/dn/bnfHQq/btrE77evCeU/QNYEOOMtldJHXNeVuEBqQ1/img.png)

안전한 연결을 지향하기 때문에 상대적으로 UDP보다 구조가 복잡하다.

Source Port 출발지 주소

Destination Port 목적지 주소

Sequence Number : 보안의 용도로 사용(아래에서 설명)

Acknowledgment Number : 보안의 용도로사용 (아래에서 설명)

Window : 나의 사용 공간이 얼마만큼 남아 있는지 상대방에게 알려주는 용도.



TCP 플래그 : 

U :Urgent Flag 급한 데이터라는 것을 알리는 용도.(Urgent Pointer와 세트)

A: Ack Flag 승인 비트 -> 물어본 것에 대한 응답 용도로 사용.(중요) 

P: Push Flag 데이터 밀어 넣기 용도

R : 초기화 비트 -> 상대방과 연결되어 있는 상태에서 추가적으로 요구가 필요한 상황에서 에러가 발생하여 초기화하는 용도

S : Syn비트 동기화 비트 -> 상대방과 연결을 시작할 때 무조건 사용하는 플래그 서로 연결을 시작하면서 동기화가 시작되는 개념(제일 중요)★★

F : Fin 종료 비트 -> 연결을 끊을 때 사용되는 플래그 



## **TCP를 이용한 통신과정.(TCP 3 Way Handshake)**

연결 수립과정

TCP를 이용한 데이터 통신을 할 때 프로세스와 프로세스를 연결하기 위해 가장 먼저 수행되는 과정.

항상 요청은 클라이언트가 서버에게 먼저 보냅니다.! 서버가 요청 보내는 건 클라이언트가 무엇을 할지 알 수없어서 불가능.!

\1. 클라이언트가 서버에게 요청 패킷을 보내고

\2. 서버가 클라이언트의 요청을 받아들이는 패킷을 보내고

\3. 클라이언트는 이를 최종적으로 수락하는 패킷을 보낸다.

**위의 3개의 과정을 3 Way Handshake라고 부른다.**



**연결 수립을 하기 위한 통신**

![img](https://blog.kakaocdn.net/dn/bnfaA5/btrE76moelb/1hJ6sMSbXr5bg8yNBZrLC1/img.png)

TCP 3Way Handshake

Syn 비트 -> 동기화 시작

Ack -> 승인 비트 (응답) 

여기서 S는 Sequence Number입니다.

여기서 A는 Acknowledgment Number입니다.

①Flag: Syn 

S:100 A:0 -> 보안의 개념

플래그의 경우 이제 동기화를 시작한다는 Syn값과 시퀀스와 Ack를 세팅해서 보냅니다.

S:100 A:0은 클라이언트가 랜덤으로 설정하여 보내는 값입니다. 

②받은 웹서버는 

Flag: Syn + Ack

S:2000 A:101로 세팅하여 보냅니다.

웹서버의 경우 동기화를 S:100 A:0을 토대로 동기화를 진행합니다.

A:번호의 경우 받은 S에서 +1 을해서 보냅니다.

S는 자기가 랜덤으로 값을 설정해서 보내게 됩니다.

③Flag:Ack

S:101 A:2001

여기서 A는 받은 S값의 플러스 1 을해서 보내게 됩니다.

이제 S는 이제 처음 받은 값이 아니라 보내게 되는 값임으로 그대로 보내면 됩니다. 동기화가 되었다고 생각하기 때문에.



## **TCP를 이용한 통신과정**

데이터 송수신 과정

TCP를 이용한 데이터 통신을 할 때 단순히 TCP 패킷만을 캡슐화해서 통신하는 것이 아닌 페이로드를 포함한 패킷을 주고받을 때의 일정한 규칙 

연결 한 이후의 과정

\1. 보낸 쪽에서 또 보낼 때는 SEQ번호가 ACK 번호가 그대로다

\2. 받는 쪽에서 SEQ번호는 받은 ACK번호가 된다.

\3. 받는 쪽에서 ACK번호는 받은 SEQ번호 + 데이터의 크기.



데이터 송수신 과정.

HTTP나 FTP와 같은 각종 데이터를 포함한 통신

![img](https://blog.kakaocdn.net/dn/cwyzyG/btrE5RKkhTU/4soEMtOxTCL2taEMfLGSW0/img.png)

①Flag : PSH + ACK

S:101 A: 2001

동기화는 이전에 했으므로 ACK만 통신한다.

보낼 때 데이터는 클라이언트는 요청 데이터는 100 크기의 데이터와 함께 보내게 됩니다.

②Flag: PSH + ACK

클라이언트에서 데이터를 100크기의 데이터와 함께 보냈음으로 A101에서 100 플러스하여 보내줍니다

그리고 서버는 클라이언트에게 500 크기의 데이터와 함께 보냅니다.

S:2001 A201

③Flag: ACK

S:201 A:2501

여기서는 클라이언트는 잘 받았다는 의미와 500의 데이터를 받았으니 A에 S에 500을 더하고 보내게 됩니다.