# socket.io란?

### websocket은 다가올 미래의 기술. 아직 인터넷 기업에서 시범적으로라도 써 볼 수 있는 기술이 아니다.

### Socket.io는 현재 바로 사용할 수 있는 기술.

### Socket.io는 JavaScript를 이용하여 브라우저 종류에 상관없이 시릿간 웹을 구현할 수 있도록 한 기술

### 만든사람

Guillermo Rauch

### [Socket.io](http://Socket.io)

-   WebSocket, FlashSocket, AJAX Long Polling, AJAX Multi part Streaming, IFrame, JSONP Polling을 하나의 API로 추상화한 것
-   즉, 브라우저와 웹 서버의 종류와 버전을 파악하여 가장 적합한 기술을 선택하여 사용하는 방식
-   개발자가 각 기술을 깊이 이해하지 못하거나 구현 방법을 잘 알지 못해도 사용 가능.
-   표준 기술이 아니라 Node.js의 모듈.
-   Guillermo Rauch가 CTO로 있는 LearnBoost라는 회사의 저작물
-   MIT 라이센스를 가진 오픈소스
-   Node.js가 아닌 다른 프레임워크에서 Socket.io를 사용할 수 있도록 하는 시도가 있다.

```jsx
npm install socket.io

```

```jsx
// 80 포트로 소켓을 연다
var io = require('socket.io').listen(80);

// connection이 발생할 때 핸들러를 실행한다.
io.sockets.on('connection', function (socket) {  
// 클라이언트로 news 이벤트를 보낸다.
    socket.emit('news', { hello: 'world' });

// 클라이언트에서 my other event가 발생하면 데이터를 받는다.
socket.on('my other event', function (data) {  
        console.log(data);
    });
});

```

### 여기에다가, 작성한 스크립트를 nohup등을 이용하여 백그라운드로 실행한다. nohup을 사용하면 hang-up signal이 발생해도 스크립트의 동작이 멈추지 않는다.

```jsx
nohup node ./server.js &

```

### client

```jsx
<script src="/socket.io/socket.io.js"></script>  
<script>  
// localhost로 연결한다.
var socket =  
  io.connect('<http://localhost>');

// 서버에서 news 이벤트가 일어날 때 데이터를 받는다.
socket.on('news',  
  function (data) {
    console.log(data);
  //서버에 my other event 이벤트를 보낸다.
    socket.emit('my other event', 
      { my: 'data' });
});
</script>

```
