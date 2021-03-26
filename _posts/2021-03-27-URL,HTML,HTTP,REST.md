---
title: "WEB기본(URI, HTTP, REST)"
date: 2021-03-24 00:00:28 -0400
draft: false
description: "[WEB]WEB기본(URI,HTTP,REST)"
categories: [WEB]
toc : true
toc_sticky : true
toc_label : 목차
---

## URI & URL
### URI(식별자)** : Uniform Resource Identifier
- 인터넷에 있는 자원을 나타내는 유일한 주소.
- 인터넷 프로토콜에 항상 붙어다니며 인터넷에서 요구되는 기본 조건이다.
- 하위개념으로 URL과 URN(이름)을 갖고 있다.
- 자원의 식별자

### URL(위치) : Uniform Resource Locator
- 네트워크 상에서 자원이 어디 있는지 알려주기 위한 규약.
- 웹 사이트 주소 뿐만 아니라 컴퓨터 네트워크 상의 자원을 모두 나타낼 수 있음.
- 자원의 위치를 나타냄.
<br>

<img src="https://media.vlpt.us/images/jch9537/post/88b0c8ac-5870-4cbc-b613-7dd39f510f31/image.png">

URL : http://opentutorials.org:3000/main
<br>
URI : http://opentutorials.org:3000/main?id=HTML&page=12

## HTTP(Hyper Text Transfer Protocol)
**Server와 Client사이에 이루어지는 요청/응답 통신규약(Application Layer 프로토콜)**
Client : 서버에 자원(HTML)을 요청(Request), GET,POST,DELETE,PUT방식으로 요청함.
<br>
Server : 클라이언트의 요청에 대한 응답(Response)을 하면 클라이언트의 web browser에서 HTML자원을 화면에 띄워줌.

**HTTP Response Format**
- 1xx : Informational
- 2xx : Successes
- 3xx : Redirection
- 4XX : Client Error
- 5XX : Server Error
<br><br> 

- HTTP는 간단하다.
- HTTP는 확장 가능하다. 
- HTTP는 Stateless하지만 HTTP쿠키는 상태를 저장하는 session을 만들도록 한다.


## REST API
웹에서 HTTP 프로토콜의 우수성을 최대한 활용하도록 하는 아키텍처<br>
1. 인터페이스 일관성 : 일관적인 인터페이스로 분리되어야 한다<br>
2. Stateless : 각 요청간 클라이언트의 컨텍스트가 서버에 저장되어서는 안됨.<br>
3. Cacheable : WWW에서와 같이 클라이언트는 응답을 캐싱할 수 있어야 한다.<br>
4. Layered System(계층화) : 클라이언트는 보통 대상 서버에 직접 연결되었는지 중간 서버를 통해 연결되었는지 알 수 없다. 중간 서버는 로드밸런싱(부하 분산) 기능이나 공유 캐시 기능을 제공함으로써 시스템 규모 확장성을 향상시킴.<br>
5. Code on demand (optional) - 자바 애플릿이나 자바스크립트의 제공을 통해 서버가 클라이언트가 실행시킬 수 있는 로직을 전송하여 기능을 확장시킬 수 있다.<br>
6. 클라이언트/서버 구조 : 아키텍처를 단순화시키고 작은 단위로 분리(decouple)함으로써 클라이언트-서버의 각 파트가 독립적으로 개선될 수 있도록 해준다.<br>