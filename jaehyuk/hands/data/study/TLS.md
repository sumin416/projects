# TLS란?

SSL 및 TLS란?

SSL

Secure Sockets Layer (Netscape 사에서 개발)

TLS

Transport Layer Security (IETF 사에서 개발)

SSL과 TLS 모두 사용자와 웹 브라우저 간 통신을 암호화하는데 사용하는 프로토콜.

공개키와 개인키를 교환하여 보안 세션을 생성한 후 통신을 암호화한다. TLS는 SSL에서 개선된 신규 모델 프로토콜이라 생각하면 된다.

전자 상거래가 활발해지며 웹 보안이 매우 중요해지고 있기에 개인정보보호 의무조치에 의해 개인정보 전송구간에 보안서버를 적용하도록 하고 있다.

기존 SSL 및 TLS 동작방식

1.  Client Hello
    
    → 클라이언트는 서버에게 지원 가능한 (암호, 키교환, 서명, 압축) 방식을 알려준다.
    
2.  Server Hello
    
    → 서버는 클라이언트에게 지원 가능한 (암호, 키교환, 서명, 압축) 방식을 응답해준다.
    
3.  Certificate Message
    
    → 서버는 공개키(RSA 암호용)가 포함된 서버 인증서를 클라이언트에게 발송한다.
    
4.  (Optional) 서버가 클라이언트 인증서를 요구한다면, 이에 대한 요청도 함께 발송한다.
    
5.  서버의 3번의 전송이 끝나면 Server Hello Done 메시지를 전달한다.
    
6.  클라이언트는 전송받은 서버 인증서에 대해 브라우저에 내장된 신뢰기관으로부터 발급 여부를 확인한 후, 세션키로 사용될 Pre-Master Key(세션키(대칭키))를 랜덤으로 생성하고 공개키로 암호화해 서버에 전송한다 - 이때 ClientKeyExchange 메시지에 암호화된 Pre-Master Key(이후 대칭키))가 포함된다 : 처음은 비대칭 교환, 그 이후는 성능상 대칭 알고리즘을 활용하기 위해
    
7.  서버는 자신의 개인키로 클라이언트에게 전송받은 암호화된 Pre-Master Key(대칭키)를 복호화한다.
    
8.  서버와 클라이언트는 협상 과정에서 전송된 모든 메시지에 대해 (암호, 키교환, 서명, 압축)방식을 다음부터 적용할 것을 알리는 종결 메시지를 발송 후 데이터 전송단계로 이동한다. : 앞으로 모든 메시지는 대칭키를 이용해 암호화
    
9.  통신이 끝나면 세션키는 폐기한다.
    

추가 정보

SSL은 IETF에 의해 사용 중지 되었기에 대부분의 최신 브라우저는 이전 프로토콜을 지원하지 않는다.

따라서 SSL을 비활성화하고 TLS를 활성화하도록 한다.

인증서와 프로토콜은 별개이다. SSL 인증서를 TLS 인증서로 대체할 필요는 없다.

프로토콜은 인증서가 아니라, 서버 구성에 따라 결정되므로 SSL 및 TLS와 함께 사용할 인증서라고 하는 것이 더 정확하다.

SSL과 TLS는 단순히 클라이언트-서버간 Handshake를 나타내는 것이 아니고, 암호화 자체를 수행하지 않는다. 절차를 진행하는 것

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d3095f9f-adaf-42ce-b6c2-b3ec539264db/Untitled.png](https://github.com/JaeHyukSim/projects/blob/jaehyuk/hands/jaehyuk/hands/data/img/%EA%B3%B5%EA%B0%9C%ED%82%A4%EC%95%94%ED%98%B8%ED%99%94.PNG)

[SSL Handshake](https://darksoulstory.tistory.com/57)
