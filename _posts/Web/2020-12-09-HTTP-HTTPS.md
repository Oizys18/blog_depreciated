---
layout: post
title: "[웹기본] HTTP와 HTTPS의 차이"
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
