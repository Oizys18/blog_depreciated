---
layout: post
title: "HTTP와 HTTPS의 차이"
author: "Oizys18"
categories: [Web]
comments: true
tags: [Web, Basics, Frontend, HTTP, HTTPS, SSL]
---
* TOC
{:toc}
* * *
## 개요
- HTTP와 HTTPS의 차이에 대한 질문을 받았는데 보안의 이점이 있다는 점 밖에 기억해내지 못했다...
- 분명 SSL에 대해 알고있었고 Gunicorn으로 HTTPS를 사용해보기도 했는데, 대답하지 못했다는 것은 아직 확실히 체득하지 못했기 때문이라고 판단했다.
- 좀 더 정확하게 서술된 언어로 공부하고자 정리하여 글로 작성했다.  

## HTTP란? 
- `HTTP(HyperText Transfer Protocol), 초본문전송규약, 하이퍼본문전송규약`
- 웹상에서 클라이언트와 웹서버간 통신을 위한 프로토콜
- W3 상에서 정보를 주고받을 수 있는 프로토콜이다. 주로 HTML 문서를 주고받는 데에 쓰인다. 주로 TCP를 사용하고 HTTP/3 부터는 UDP를 사용하며, 80번 포트를 사용한다.
- HTTP는 클라이언트와 서버 사이에 이루어지는 요청/응답(request/response) 프로토콜이다. 예를 들면, 클라이언트인 웹 브라우저가 HTTP를 통하여 서버로부터 웹페이지(HTML)나 그림 정보를 요청하면, 서버는 이 요청에 응답하여 필요한 정보를 해당 사용자에게 전달하게 된다.

### HTTP의 단점 
- 서버에서부터 브라우저로 전송되는 정보가 암호화되지 않는다.(== 데이터 도난의 위험성이 있다.)

## HTTPS란?
- `HTTPS(Hypertext Transfer Protocol Secure), 하이퍼 텍스트 전송 프로토콜 보안`
- 간단히 말해 `HTTP`에 `SSL`을 추가한 것.

### SSL이란?
  - `SSL(Secure Socket Layer), 보안소켓계층` 
  - Netscape사에서 웹서버와 브라우저 사이의 보안을 위해 만들었다. SSL은 Certificate Authority(CA)라 불리는 서드 파티로부터 서버와 클라이언트의 인증을 하는데 사용된다.
  - 사용하여 서버와 브라우저 간에 암호화된 연결을 생성할 수 있다. 서버 브라우저의 민감한 정보 도난을 방지할 수 있다.

### HTTPS의 장점 
- `SSL` 인증서를 통한 데이터 암호화
- TLS(전송계층보안) 프로토콜을 통해 보안 유지, 데이터 무결성 보장 
- HTTP에 비해 검색엔진 최적화(SEO)에 혜택을 받는다. 
- 구글이 개발한 `가속화된 모바일 페이지(AMP)`를 만들 수 있다. 
- HTTP2.0 사용하기에 HTTP1.1 사용하는 HTTP보다 빠르다. 
  - HTTP1.1에서 동일 조건하에 HTTP가 HTTPS보다 빠르다 (SSL/TLS, 암호화 시 CPU사용 및 암호화로 인한 데이터 길이 증가)



## HTTP1.1? HTTP2.0? 
### HTTP1.1 
- 1999년 출시
- 연결당 하나의 요청과 응답을 처리
-  UI 개발자/프론트엔드개발자는 이미지 스프라이트, 도메인샤딩, CSS/JavaScript 압축, Data URI 등을 업무에 사용하였습니다.
#### 단점
  - 동시전송 문제와 다수의 리소스를 처리하기에 속도와 성능 이슈
  - HOL(Head Of Line) Blocking-특정응답지연 
  - RTT(Round Trip TIme) 증가 
  - 헤비한 Header구조

### HTTP2.0
- 성능 / 속도 월등히 개선되었다. 
- Multiplexed Streams(한 커넥션에 여러개의 메세지를 동시에 주고 받을 수 있음)
- Stream Prioritization(요청 리소스간 의존관계를 설정)
- Server Push(HTML문서상에 필요한 리소스를 클라이언트 요청없이 보내줄 수 있음)
- Header Compression(Header 정보를 HPACK압충방식을 이용하여 압축전송) 


#### 참고
- https://developers.google.com/web/fundamentals/performance/http2/?hl=ko
- https://medium.com/@shlee1353/http1-1-vs-http2-0-%EC%B0%A8%EC%9D%B4%EC%A0%90-%EA%B0%84%EB%8B%A8%ED%9E%88-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0-5727b7499b78