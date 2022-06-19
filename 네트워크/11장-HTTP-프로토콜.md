## **HTTP 프로토콜**

www에서 쓰이는 핵심 프로토콜로 문서의 전송을 위해 쓰이며, 오늘날 거의 모든 웹 애플리케이션에서 사용되고 있습니다.

HTTP 특징 

Reqeust / Response (요청/ 응답) 동작에 기반하여 서비스 제공



HTTP 1.0 특징

엄청 옛날이어서 홈페이지가 엄청 간단한 페이지였습니다.

연결 수립 , 동작, 연결 해제의 단순함이 특징 -> 하나의 URL은 하나의 TCP 연결

HTTP 1.0의 문제점

단순 동작이 반복되어 통신 부하 문제 발생



네트워크 부하가 심한 HTTP1.0

![img](https://blog.kakaocdn.net/dn/ceEGH5/btrFci7AQH1/pBvpxuKgoHKtqpFBEvHcYK/img.png)

매번 연결할 때마다 연결하고 연결 종료하고 이러한 과정을 매번 할 때마다 반복해야 되는 문제점입니다.

한번 연결했으면 끊지 말고 받아갈 거 다 받아가고 끊어야 하는데 매번 연결하고 종료해야 하는 것이 문제인데 이것을 해결한 것이 HTTP1.1 버전입니다.

![img](https://blog.kakaocdn.net/dn/dbL9bG/btrFbNUhLC0/yKQ1F3koUJips7QpdkA481/img.png)



## **HTTP 요청 프로토콜**

요청하는 방식을 정의하고 요청 프로토콜 구조

클라이언트의 정보를 담고 있는.

![img](https://blog.kakaocdn.net/dn/qXp8s/btrFbN03QuC/aMc5K12DYAYyUKKKxS0B91/img.png)HTTP프로토콜 구조

![img](https://blog.kakaocdn.net/dn/wbydt/btrE8OsTBp3/flUOQS1K2XKTAS1h6SpgqK/img.png)

첫 번째는 Request Line 

두 번째는 Header 

세 번째는 공백

네 번째는 Body인데 데이터가 없는 상황.



여기서 Request Line에 대해 알아봅시다

![img](https://blog.kakaocdn.net/dn/bzBKWM/btrE4bvUZD7/knM4my7D7kU4KW7mqlkkeK/img.png)

Reqeust Line의 경우 이렇게 구성되어 있습니다.

여기서 중요한 요청 타입에 대해 알아봅시다.



요청 타입의 경우 많은 종류가 있는데

![img](https://blog.kakaocdn.net/dn/cySGs1/btrE51Tb3tN/UwfmbUJhY8LTjnxVKI6fKK/img.png)

여기서 제일 중요한 것은 GET, POST. PUT, PATCH 등이 있습니다.

GET은 READ 작업이 필요할 때 사용되고

POST는 정보를 전송하거나(CREATE)할 때 사용됩니다.



GET 방식과 POST방식의 차이점

GET 주소창에 데이터를 포함시켜서 보내고

POST방식은 Body에 데이터를 포함시켜서 보내는 개념.



**URI**

인터넷 상에서 특정 자원을 나타내는 유일한 주소



## **HTTP 응답 프로토콜의 구조**

사용자가 볼 웹페이지를 담고 있는 응답 프로토콜 구조.

![img](https://blog.kakaocdn.net/dn/oX6U2/btrE8NOi1Yc/9luAXKtYf7pbI4BWDoBPs1/img.png)

응답 프로토콜의 경우 요청과 다른 것은 Request Line 이 Status Line으로 변경된 점.

맨 처음

Status Line입니다.

![img](https://blog.kakaocdn.net/dn/zCWyz/btrE7wyA75p/l3VQr0r6ulMHCV4WTt20sk/img.png)

이렇게 구성되어있는데 버전은 중요하지 않고 알아볼 사항은 상태 코드에 대해 알아봐야 합니다.

![img](https://blog.kakaocdn.net/dn/qhX3c/btrFbOeEFYc/RstTpAi5LRDCazYEn8Ka61/img.png)

200번대는 Client의 요청이 정상적으로 완료되었을 때(정상)

300번대는 Redirecting으로 주소를 다른 곳으로 옮겨주는 상황이 필요할 때

400번대는 Client 요청이 잘못된 정보를 요청할 때(클라이언트 잘못)

500번대는 서버가 오류가 생기거나 에러가 생기는 상황을 말합니다.(서버 잘못)



다음은 HTTP 헤더 포맷입니다.

수많은 정보를 담고 있는 HTTP 헤더입니다.

![img](https://blog.kakaocdn.net/dn/1kEP9/btrE4BnACMn/6XAnZ16Jspre0ePSZvZf5K/img.png)

![img](https://blog.kakaocdn.net/dn/dPBw7x/btrE75uSU8n/pVPbuVKH3TcglKbotcRnT0/img.png)

User-Agent를 가지고 사용자가 어떤 OS를 사용했는지 알 수 있어 컴퓨터로 접속했는지, 휴대폰으로 접속했는지 알 수 있습니다.

![img](https://blog.kakaocdn.net/dn/xSMfj/btrE5fqP3oB/ovT3MkeKvT0dLgdjq3D0Bk/img.png)