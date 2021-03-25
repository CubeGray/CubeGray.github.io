---
title: "Servlet VS JSP"
date: 2021-03-25 00:00:28 -0400
draft: false
description: "[Web] Servlet VS JSP"
categories: [Web]
toc : true
toc_sticky : true
toc_label : 목차
---

## Web Application
### Web Browser
클라이언트에서 요청을 하고 전달받은 페이지를 볼 수 있는 환경(Chrome, Firefox, Safari...)

### Web Server
- 클라이언트로부터 요청받아 서버에 저장된 리소스를 클라이언트에게 전달해주는 역할. 
- 정적인 컨텐츠 담당.
- HTTP 프로토콜에 따라 웹 클라이언트와 통신함.
<br>
ex)Apache, nginx

### Web Application Server(WAS)
- 서버에서 사용자의 입력을 받아 동적으로 처리하고 그 결과를 보여주는 웹서버
- 동적인 컨텐츠 담당
- 트랜잭션, 트래픽관리, DB 커넥션 풀, 사용자 관리등 다양한 기능 제공
- 하나의 웹 서버에서 php, java 등등의 여러 어플리캐이션을 사용하거나 로드밸런싱(부하를 분산해주는 장치)을 하기위해 WEB Server와 WAS가 분리됨.

## Servlet
- 확장자 : *.java
- java기반의 웹 처리 스펙
- java기반의 코드에 HTML tag가 포함되어 있음
- 웹페이지를 동적으로 생성하기 위한 서버측 프로그램, WAS위에서 컴파일 되고 동작함.
- 주로 Controller에서 쓰임
- 요청하는 client수와 무관하게 servlet 객체는 무조건무조건 server 내부에 하나만 존재
- doGet() or doPost()와 같은 서비스 메소드들은 client 요청 수만큼 thread로 실행되어 처리
<br><br>

## JSP
- 확장자 : *.jsp
- HTAML tag에 java코드가 포함되어 있음.(EL, JSTL)
- java의 데이터 값을 브라우저 화면에 출력하게 하는 기술
- html은 자바 코드 활용 불가능
- jsp는 실제 client 에게 서비스 하게 되는 코드를 servlet으로 변환(tomcat이 자동 변환)
- 실행시 Web Contatiner가 Servlet으로 자동 변환함.
- 주로 View에서 쓰임

