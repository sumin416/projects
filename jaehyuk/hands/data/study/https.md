
### Hyper Text Transfer Protocol Secure

### HTTP의 약점인, 서버로부터 브라우저로 전송되는 정보가 암호화되지 않는다는 것을 해결

### SSL (보안 소켓 계층)을 활용

### SSL

서버와 브라우저 사이에 안전하게 암호화된 연결을 만들어주고, 서버와 브라우저가 민감한 정보를 주고받을 때 이것이 도난당하는 것을 막아준다.

HTTPS는 SSL프로토콜 위에서 돌아가는 프로토콜

### TLS (전송 계층 보안)을 활용

### TLS

데이서 무결성을 제공하여 데이터가 전송 중에 수정되거나 손상되는 것을 방지하고 사용자가 자신이 의도하는 웹 사이트와 통신하고 있음을 입증하는 인증 기능.

### 검색엔진 최적화.(SEO)

### AMP(Accelerated Mobile Pages) - 가속화된 모바일 페이지를 만들 때 HTTPS를 써야만 한다.

### AMP

모바일 기기에서 훨씬 빠르게 컨텐츠를 로딩하기 위한 방법 - 구글이 만듦

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dea1f05d-b78f-44c9-8a00-0ecbba9b506f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dea1f05d-b78f-44c9-8a00-0ecbba9b506f/Untitled.png)

### TCP/IP 포트는 443

### 공개키 암호화 방식

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/25432de6-f2bc-412a-9b2b-227a6e717859/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/25432de6-f2bc-412a-9b2b-227a6e717859/Untitled.png)

### 공개키 저장소

CA ( Certificate Authority)

민간기업이지만 아무나 운영할 수 없고 신뢰성이 검증된 기업만 CA를 운영할 수 있다.

### 과정

1.  애플리케이션 서버(A)를 만드는 기업은 HTTPS를 적용하기 위해서 공개키와 개인키를 만든다.
2.  신뢰할 수 있는 CA기업을 선택하고 그 기업에 내 공개키를 관리해달라고 계약하고 돈을 지불한다.
3.  계약을 완료한 CA기업은 또 CA기업만의 공개키와 개인키가 있다. CA기업은 CA기업의 이름과 A서버의 공개키, 공개키 암호화 방법 등의 정보를 담은 인증서를 만들고, 해당 인증서를 CA 기업의 개인키로 암호화해서 A서버에게 제공한다.
4.  A서버는 암호화된 인증서를 갖게 된다. 이제, A서버는 A서버의 공개키로 암호화된 HTTPS요청이 아닌 요청이 오면, 이 암호화된 인증서를 클라이언트에게 준다.
5.  이제 클라이언트는 데이터를 요청할 때 HTTPS요청이 아니기 때문에 데이터가 아니라 CA기업이 A서버의 정보를 CA기업의 개인키로 암호화한 인증서를 받게 된다.
6.  *세계적으로 신뢰할 수 있는 CA 기업의 공개키는 브라우저가 이미 알고 있다!!!!
7.  브라우저가 CA기업 리스트를 쭉 탐색하면서 인증서에 있으면, CA기업의 공개키를 알고 있으므로 브라우저가 해독하여 A 서버의 공개키를 얻는다.
8.  A서버와 통신할 때 클라이언트는 A서버의 공개키로 암호화하여 Request를 보낸다.
9.  *신뢰할 수 없는 CA기업을 통해 인증서를 받으면 -주의 요함, 안전하지 않은 사이트-알람 발생

### SSL 디지털 인증서 사용의 이점

-   통신 내용이 공격자에게 노출되는 것을 막는다 (이건 굳이 인증서가 필요한가)
-   클라이언트가 접속하려는 서버가 신뢰할 수 있는 서버인지 판단할 수 있다(이거다! 서버로 보내는 데이터 자체는 암호화되지만, 보내려는 서버 자체가 안전한지를 판단하려면 세계적으로 신뢰할 수 있는 제3자가 판단을 도와주어야만 한다)
-   통신 내용의 악의적인 변경을 방지할 수 있다

[](https://opentutorials.org/course/228/4894)[https://opentutorials.org/course/228/4894](https://opentutorials.org/course/228/4894)

[](https://jeong-pro.tistory.com/89)[https://jeong-pro.tistory.com/89](https://jeong-pro.tistory.com/89)
