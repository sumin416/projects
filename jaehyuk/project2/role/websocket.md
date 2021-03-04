# WebSocket이란? 

### 참고
[NAVER D2](https://d2.naver.com/helloworld/1336)

### 하나의 TCP 접속에 전이중 통신 채널을 제공하는 컴퓨터 통신 프로토콜

### WebSocket vs HTTP

1.  공통점
    
    1.  두 프로토콜 모두 OSI 모델의 제 7계층 Application에 위치.
    2.  두 프로토콜 모두 제 4계층의 TCP에 의존.
2.  차이점
    
    1.  WebSocket은, HTTP 포트 80 또는 HTTPS 443 위에서 동작하도록 설계되었으며, HTTP 프록시 및 중간 층을 지원하도록 설계되었으므로, HTTP 프로토콜과 호환이 된다.
    
    2.  웹소켈 프로토콜은 HTTP 풀링과 같은 반이중방식에 비해 더 낮은 부하를 사용하여 웹 브라우저와 웹 서버간 통신을 가능하게 한다.
    
    3.  서버와의 실시간 데이터 전송을 가능하게 한다.
    
    4.  대부분의 브라우저가 이 프로토콜을 지원한다.
    

### 웹 소켓의 역사

-   TCP 기반 Network Socket API를 대체할 목적으로 HTML5 사양에서 TCPConnection으로 처음 참조됨

### 프록시 경유

HTTP CONNECT 메소드로 영구적인 터널을 구성한다.

## WebSocket과 Socket.io

웹 페이지의 한계에서 벗어나 실시간으로 상호작용하는 웹 서비스를 만드는 표준 기술인 WebSocket.

웹소켓의 역사

필요한 이유 : 웹소켓이 존재하는 이유에 따라 프로젝트에 적용할 것인지 판단할 수 있다.

1.  1989 웹 역사 시작 : 사용자와의 상호작용은 웹 개발의 큰 부분차지 X
2.  이후 웹이 점점 확장되면서 상호작용을 요구
3.  전형적인 브라우저 렌더링 방식은 HTTP Request에 대한 HTTP Response를 받아서 브라우저의 화면을 깨끗하게 지우고 받은 내용을 새로 표시 : 깜빡인다.
4.  깜빡임 없이 원하는 부분만 렌더링하며 실시간 사용자와 상호작용하는 방식이 나타남 :RIA(Rich Internet Application) 기술의 발달이 촉진됨
5.  하지만 이러한 방식들 모두 기존의 메시지 교환 규칙인 HTTP를 변경하지 않고 구현한 방식이라, 복잡하고 어려운 코드로 구현해야 했다.
6.  보다 쉽게 상호작용하는 웹 페이지를 만드려면 브라우저-서버 사이에 더 자유로운 양방향 메시지 송수신(bidirectional full-duplex communication)이 필요.
7.  그래서 HTML5 표준안의 일부로 WebSocket API가 등장했다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ea916c3e-ffb4-45f5-a1ef-6e2a18f488d2/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ea916c3e-ffb4-45f5-a1ef-6e2a18f488d2/Untitled.png)

WebSocket은 소켓을 이용하여 자유롭게 데이터를 주고받을 수 있다. 즉, 기존의 요청-응답 관계 방식보다 더 쉽게 데이터를 교환할 수 있다.

WebSocket 프로토콜

-   표준 WebSocket의 API는 W3C에서 관장
-   프로토콜은 IETF(Internet Engineering Task Force)에서 관장.
-   WebSocket은 HTTP와 마찬가지로 80번 포트로 웹 서버에 연결
-   HTTP 프로토콜의 버전은 1.1이지만, Upgrade 헤더를 사용하여 웹 서버에 요청.
-   클라이언트, 서버 모두 WebSocket 기능을 지원해야 한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e6ff1f5f-acfd-452e-8c74-b8b22a66a33f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e6ff1f5f-acfd-452e-8c74-b8b22a66a33f/Untitled.png)

```jsx
if ('WebSocket' in window) {  
    var oSocket = new WebSocket(“ws://localhost:80”);

    oSocket.onmessage = function (e) { 
        console.log(e.data); 
    };

    oSocket.onopen = function (e) {
        console.log(“open”);
    };

    oSocket.onclose = function (e) {
        console.log(“close”);
    };

    oSocket.send(“message”);
    oSocket.close();
}


```

원리

1.  token을 이용한 핸드셰이킹
2.  protocol-overhead 방식으로 서로 데이터 주고받음
3.  이런 방식을 사용하여 방화벽 환경에서도 사용 가능
