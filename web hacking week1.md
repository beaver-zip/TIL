# 웹 기본 상식

**프로토콜(protocol)**

> 규격화된 상호작용에 적용되는 약속
컴퓨터 통신 프로토콜은 각 통신 주체가 교환하는 데이터를 명확히 해석하도록 문법(syntax)를 포함.
문법에 어긋날 시, 잘못 전송된 것으로 인식하여 취급을 무시함.
> 

## HTTP

**HTTP (Hyper Text Transfer Protocol)**

- HTTP란 서버와 클라이언트의 데이터 교환을 요청(Request)과 응답(Response) 형식으로 정의한 프로토콜이다.
- HTTP의 기본 메커니즘은 클라이언트가 서버에게 요청하면, 서버가 응답하는 것.
HTTP 서비스 포트에 대기 - 주로 TCP/80 or TCP/8080

> 네트워크 포트 vs 서비스 포트
네트워크 포트란 네트워크에서 서버와 클라이언트가 정보를 교환하는 추상화된 장소
서비스 포트란 네트워크 포트 중에서 특정 서비스가 점유하고 있는 포트
> 

**HTTP 메시지**

- HTTP 헤드
HTTP 헤드의 각 줄은 CRLF로 구분. 첫 줄은 시작 줄(Start-line), 나머지 줄은 헤더(Header)라고 부른다. 헤드의 끝은 CRLF 한 줄로 나타낼 수 있다. 헤더는 필드의 값으로 구성되어있고, HTTP 메시지 또는 바디의 속성을 나타낸다.
- HTTP 바디
HTTP 바디는 헤드의 끝을 나타내는 CRLF 뒤, 모든 줄을. 클라이언트나 서버에게 전송하려는 데이터가 바디에 있다.

**HTTP 요청과 HTTP 응답**

- HTTP 요청
서버에게 특정 동작을 요구하는 메시지
    
    > (시작줄)
    메소드(Method), 요청 URI(Request-URI), 그리고 HTTP 버전으로 구성
    (띄어쓰기로 구분)
    메소드: URI가 가리키는 리소스를 대상으로, 서버가 수행하길 바라는 동작을 나타냄>
    > 
    > - GET : 리소스를 가져오라는 메소드
    > - POST : 리소스로 데이터를 보내라는 메소드
    > 요청 URI : 메소드의 대상
    > HTTP 버전 : 클라이언트가 사용하는 HTTP 프로토콜의 버전
- HTTP 응답
HTTP 요청에 대한 결과를 반환하는 메시지 . 상태 정보(Status), 클라이언트에게 전송할 리소스
    
    > (시작줄)
    HTTP 버전, 상태 코드(Status Code), 처리 사유(Reason Phrase)
    (띄어쓰기로 구분)
    > 
    > - (HTTP 버전) 서버에서 사용하는 HTTP 프로토콜의 버전
    > - (상태 코드) 요청에 대한 처리 결과를 세 자릿수로 나타냄.

![https://velog.velcdn.com/images%2Fsw092311%2Fpost%2F2f9a863f-1e88-43bc-80b3-3361ff5ecbe5%2FHTTP%20%EC%9D%91%EB%8B%B5%20%EC%83%81%ED%83%9C%20%EC%BD%94%EB%93%9C.PNG](https://velog.velcdn.com/images%2Fsw092311%2Fpost%2F2f9a863f-1e88-43bc-80b3-3361ff5ecbe5%2FHTTP%20%EC%9D%91%EB%8B%B5%20%EC%83%81%ED%83%9C%20%EC%BD%94%EB%93%9C.PNG)

---

## HTTPS

- 등장 배경
TLS(Transport Layer Security) 프로토콜을 도입하여 공격자가 중간에 가로채 이용자의 계정 탈취 문제가 생김.
(TLS : 서버와 클라이언트 사이에 오가는 모든 HTTP 메시지를 암호화)
- HTTP와 HTTPS의 비교방법
웹 서버의 URL이 http:// 로 시작되면 HTTP, [https://로](https://xn--2o2b/) 시작되면 HTTPS 프로토콜을 사용한다.

---

# 웹

> 인터넷이라는 통신망을 활용해 구현된 전 지구적 정보 공간
> 
- 웹 서비스
프로트엔드 (Front-end) : 이용자의 요청을 받는 부분
백엔드 (Back-end) : 이용자의 요청을 처리하는 부분
- 웹 리소스
    
    > HTML (Hyper Text Markup Language) : 웹 문서에서 태그와 속성을 통한 구조화된 문서 작성을 지원함.CSS (Cascading Style Sheets) : 웹 문서의 생김새를 지정, 글자의 색, 모양, 배경, 이미지의 크기나 위치 등을 지정 가능JS (JavaScript) : 웹 문서의 동작을 정의
    > 

---

# 웹 브라우저

HTTP/S 로 이용자와 웹 서버의 통신을 중개, 서버로부터 받은 다양한 웹 리소스들을 가공해 효과적으로 전달함. 이요아자가 다양한 프로토콜을 알지 못해도 쉽게 사용하도록 도와줌.

## URL

Uniform Resource Locator

구조 : Scheme, Authority (User info, Host, Port), Path, Query, Fragment

![https://velog.velcdn.com/images%2Fsw092311%2Fpost%2F1edff38b-60b1-474f-87d2-11bd619db3ea%2FURL.PNG](https://velog.velcdn.com/images%2Fsw092311%2Fpost%2F1edff38b-60b1-474f-87d2-11bd619db3ea%2FURL.PNG)

웹에 있는 리소스의 위치를 표현하는 문자열
(브라우저는 URL을 통해 서버에게 요청함.)

- Domain Name
URL 중 Host의 도메인 이름을 IP로 변환하거나 IP를 도메인 이름으로 변환한다.
- 웹 렌더링
서버로부터 받은 리소스를 이용자에게 시각화하는 행위를 말한다.

## 브라우저 개발자 도구 (Devtools)

![https://velog.velcdn.com/images%2Fsw092311%2Fpost%2Fc83ab729-f6f5-4368-9a2f-e5a2351a5913%2F%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%8F%84%EA%B5%AC%EC%B0%BD.PNG](https://velog.velcdn.com/images%2Fsw092311%2Fpost%2Fc83ab729-f6f5-4368-9a2f-e5a2351a5913%2F%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%8F%84%EA%B5%AC%EC%B0%BD.PNG)

- 요소 검사 (Inspect) : 특정 요소의 개괄적인 정보를 파악하고, 이와 관련된 코드를 쉽게 찾을 수 있다.
- 디바이스 툴바 : 활용해 브라우저의 화면 비율, User-Agent를 원하는 값으로 변경 가능
- Elements : 현재 페이지를 구성하는 HTML 코드를 읽을 수 있다.
HTML 수정 : 코드를 선택한 상태로 F2를 누르거나 더블 클릭하여 수정 가능. 편리함
- Console : 프론트엔드의 자바스크립트 코드에서 발생한 메세지를 출력, 이용자가 입력한 자바스크립트 코드 실행
- Sources : 현재 페이지 구성하는 웹 리소스들을 확인
Sources: Debug : 원하는 자바스크립트 디버깅도 가능
- Network : 서버와 오가는 데이터를 확인할 수 있음. (복사 기능 존재)
- Application : 쿠키, 캐시 , 이미지, 폰트, 스타일시트 등 App 관련 리소스 조회 가능
Cookies에서는 브라우저에 저장된 쿠키 정보 확인, 수정 가능

![https://velog.velcdn.com/images%2Fsw092311%2Fpost%2Fb6b6a624-bd89-49c3-bc3c-24df220ee91c%2F%EA%B0%9C%EB%B0%9C%EC%9E%90%20%EB%8F%84%EA%B5%AC%202.PNG](https://velog.velcdn.com/images%2Fsw092311%2Fpost%2Fb6b6a624-bd89-49c3-bc3c-24df220ee91c%2F%EA%B0%9C%EB%B0%9C%EC%9E%90%20%EB%8F%84%EA%B5%AC%202.PNG)