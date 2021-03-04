
## 나는 이 프로젝트를 왜 할까??

-   이용자에게 이미지뿐 아니라 다양한 확장 파일 공유 서비스도 제공해주고 싶었기 때문.
    
    → 이전 프로젝트에서 image의 업로드 및 다운로드 기능이 있는 review 서버를 개발했습니다. 이때 다른 확장자 파일이나 대용량 파일을 전송하는 방법과 그 성능에 대한 문제를 해결하고 이용자에게 보다 좋은 기능을 제공해주고 싶어서.
    
-   구글 크롬 확장 어플리케이션과 android app을 활용하면 이용자에게 보다 좋은 파일 공유 경험을 가지게 할 수 있을 것이라 생각함.
    

## 프로젝트 각오

이 프로젝트를 설명할 때 자신감 뿜뿜!

팀원들 발목을 잡지 않겠다. 내 역할은 반드시 책임지고, 도와줄 수 있는 역량 만들기!

## 팀명

태양광전구

## 담당 프로님

-   권태성

## 교육프로님

-   황현승

## 담당교수님

-   한기철

## 팀원

-   구민진(팀장)
-   심재혁
-   권세진
-   이병훈
-   남우진

## 회의 일부 발췌

→ 기존의 파일 공유는 메일이나 USB등으로 했다. 이러한 파일 공유는 사용자 입장에서 불편하다. 그래서 sendAnywhere를 사용해봤는데 훨씬 편하다. 이 애플리케이션은 구글 크롬 애플리케이션도 지원하는데, 파일 공유보다는 단순 웹 사이트 이미지 링크 공유만 가능했다.(이미지를 우클릭 하는 방식) 그래서

우리가 하고자 하는것

일시적으로만 파일 공유가 가능하니까, 이걸 다이렉트로 파일을 공유할 수 있게 하면 어떨까?(구글 크롬 애플리케이션에서의 다이렉트 공유)

즉, 휴대폰-웹 브라우저간 파일을 주고받는 방식으로.

그렇다면 알아야 할 것 (핵심)

-   어떻게 파일을 공유하나?
    
    → 이것에 대해 잘 알기 위해 [socket.io](http://socket.io), FTP, WebSocket, HTTP와 같은 Protocol을 잘 찾아보자
   
        
-   구글 크롬 애플리케이션에 어떻게 적용하나?
    
### 성능 향상에 대해 생각해보면?

UDT + UDP network socket을 활용하면? UDP + Checksum + Sliding Window

거기에다가 병력, 압축전송기능을 추가적으로 구현함으로써 성능 향상이 가능할까?

## 왜 node js??

1.  express.js를 사용하면 mvc 패턴을 이용할 수 있다
    
2.  싱글 스레드 기반으로, 매 요청마다 쓰레드를 이용하지 않으므로(여러 요청이 들어올 때)
    
    -   메모리 절약
    -   속도 향상(쓰레드 기반의 컨텍스트 스위칭 발생을 줄임 - overhead)
    -   확장성 향상(아직 잘 이해가 안댐)
3.  시스템 커널에 보조 스레드가 많다(libuv) 이걸 이용하여 Nonblocking I/O처리
    
4.  그러나, 복잡하고 메모리를 많이쓰는, 즉 Main Thread를 오래 점유하는 request가 많이 오는 상황에는 적합하지 않다.(연산의 복잡도가 클 경우)
    
5.  그렇다면 파일 공유 서버는?? - http로 cloud storage 공유일 경우, http request가 분할되어 온다. 이때 파일의 read 및 write는 I/O처리이므로, Main Thread 자원을 이용하지 않는다. 따라서 성능 하락을 가져오지 않고 오히려 여러 요청, 여러 파일의 partition 처리에 유리할 것이라 생각이 든다. 그리고 이러한 대용량 stream은, 부분적으로 I/O가 가능하므로 메모리를 크게 차지하지 않게 설계할 수 있다.
    
    [[NodeJS] Stream의 개념과 Stream2의 차이](https://programmingsummaries.tistory.com/363)
    
6.  여차하면 프론트엔드 개발자의 핼프를 받을 수 있다(?)
    

## 왜 spring??

1.  Java라는 언어에 익숙하다.
2.  Library, Framework에 익숙하다.
3.  안정적이고 레퍼런스가 많다.
4.  버그와 같은 면에서의 안정성도 높다
5.  따라서 빠르게 아키텍처를 싸고 로직부분에만 신경쓸 수 있을 것 같다.
6.  정형화된 Pattern, 우리의 강력한 IoC/DI 컨테이너
7.  설정이 복잡하다(단점)

사실, nodejs와 spring을 실제로 비교해서 써 본 적이 없으므로, 이런 내용들이 정확한지 잘 모르곘다.

Node.js가 Spring MVC보다 성능상 우위에 있다라고 말하기 위해서 몇가지 전제사항

1.  다중처리를 동시에 처리하도록 요구된다.
    
2.  많은 I/O 작업을 수행한다.
    
3.  단순한 CPU 작업만을 진행한다.
    

BitTorrant : 서버는 단순히 파일을 가진 peer 목록 리스트만 가지고 있다. 이것을 클라이언트가 받아서 파일을 가진 peer에게 직접 p2p 다이렉트 전송을 요청할 수 있는것(by client application)

따라서, 우리 프로젝트 기능에 넣으려면, 서버는 단순히 보안 번호나 QR을 통해 파일 공유자들을 지정하고, 해당 공유자들끼리 p2p 파일 공유를 시도한다.(by 우리가 만든 client application - 모바일, 웹)

## 결론
### node.js 사용하는 것이 좋을 것 같다.
1. non-blocking I/O : 우리 프로젝트의 큰 줄기인 두가지 기능은 첫째. 디바이스의 선택한 일부 폴더를 본인과 권한을 부여받은 지인들이 공유하는 것, 둘째. 파일을 전송하는 것이다. 특히 대용량 파일을 전송할 수 있도록 설계하려고 하는데, 이때 socket에 의해 전송되는 데이터가 안정성을 위해 분할된 패킷으로 전송되고, 트래픽이 존재할 것으로 가정하여 많은 I/O가 생길 것이라 생각한다. 따라서 nonblocking I/O를 가지고, singlethread로 context switching overhead가 없는 node.js를 이용하는 것이 옳다고 판단하였다.
2. socket.io를 node.js에서 활용할 수 있기 때문이다. spring에서도 websocket이 있지만, socket.io처럼 브라우저와 웹 사이의 전이중 통신 방식에서 websocket외에도 가장 적합한 기술을 선택해 주는 방법이 효과적이라 생각하였다.


## 계획서

[(SSAFY)필드 프로젝트 계획서_태양광전구_ver0.01.docx](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f5b8bd47-2121-4918-b3fc-f7a18cee0a96/(SSAFY)____ver0.01.docx)

## 정리 페이지

[프로젝트 계획서](https://www.notion.so/3de007888cb44d38b5200fdfa80ea1fa)

[크로스 플랫폼 개발이란?](https://www.notion.so/5577c79bcdfa405fa7743223f2b29974)

[Node.js란?](https://www.notion.so/Node-js-cffa9c989c2c4f8d875e7830dc4e7bf7)

[FTP의 원리는?](https://www.notion.so/FTP-9325f7d055764c7093f6869a9dd90f2f)

[웹하드란?](https://www.notion.so/07273d51d4b7488ab055e90417c16294)

[RTT란?](https://www.notion.so/RTT-1dba48d1f42b43c6b604199f76483cdd)

[QR이란?](https://www.notion.so/QR-ec6520cc753345ff8db7974c70ef4d84)

[socket이란?](https://www.notion.so/socket-129a30772a3f4d67b9ac5ac4322198b2)

[websocket이란?](https://github.com/JaeHyukSim/projects/blob/jaehyuk/project2/jaehyuk/project2/role/websocket.md)

[socket.io란?](https://www.notion.so/socket-io-8b96bc2b98994911b03ffba31c669819)

## TODO LIST

-   [x] 크로스 플랫폼 개발이란?
-   [x] Node.js란?
-   [ ] 구글 크롬 확장 어플리케이션 개발 방법은?
-   [x] Socket.IO란?
-   [ ] WebRTC와 socket.io의 차이점
-   [ ] 네이티브 앱, 웹 앱, 하이브리드 앱이란?
-   [ ] Flutter?
-   [ ] 크로스플랫폼 프레임워크
-   [ ] PageCall이 무엇일까
-   [ ] WebSocket이란?
-   [ ] WebRTC의 DataChannel은?
-   [ ] FCM이란?
-   [ ] FTP의 원리는?
-   [x] 웹하드란?
-   [x] RTT란?
-   [x] QR이란?
-   [x] websocket이란?
-   [ ] 방화벽이란?
-   [ ] Protocol OverHead방식이란?

## 추가

http의 content-type이 multipart form-data

[회의록 - 20210226 - 1차](https://www.notion.so/20210226-1-38868af2056e4eebab5b2e0d5262216c)

[회의록 with 권태성멘토님 2021-03-03](https://www.notion.so/with-2021-03-03-6a6df9a121fd4c21af78e4088063088b)
