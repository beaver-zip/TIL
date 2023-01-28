# Cookie

### 등장배경

HTTP에는 2가지 특징으로 클라이언트의 IP 주소와 User-Agent는 웹 서버가 기억할 수 없다.

> HTTP의 두가지 특징
> 
> - Connectionless : 하나의 요청에 하나의 응답을 한 후 연결을 종료하는 것을 의미
> - Stateless : 통신이 끝난 후 상태 정보를 저장하지 않는 것을 의미

### 쿠키의 구성

Key , Value 값으로 이루어져있음.(그 외에 n가지 이상의 속성이 존재 : 사이즈, 도메인, 경로 등)

### 쿠키의 역할

- 클라이언트의 정보 기록과 상태 정보를 표현하는 용도로 사용
- 클라이언트에 저장되기 때문에 저장된 쿠키를 조회, 수정 ,추가가 가능함.
- 헤더 변조도 가능한데 만료 시간이 지정이 가능하고, 그 이후에는 삭제된다.

---

# Session

### 등장배경

웹 통신에서 클라이언트가 쿠키를 변조해 서버에 요청을 보낼 수 없다는 것을 알 수 있다. 따라서 세션과 쿠키를 동시에 사용하여 다른 사람이 내 쿠키를 변조해서 사용하는 것을 방지할 수 있다.

### 세션의 역할

세션은 인증 정보를 서버에 전달한다. 그리고 해당 데이터에 접근할 수 있는 키를 만들어 클라이언트에 전달한다. 이때 키는 유추할 수 없는 랜덤 문자열을 얘기한다.

### 쿠키와 세션의 차이점

쿠키는 데이터 자체를 이용자가 저장하지만, 세션은 서버에게 있다는 차이가 있다.

> 세션 하이재킹 : 공격자가 이용자의 쿠키를 훔칠 수 있으면 세션에 해당하는 이용자의 인증 상태를 훔칠 수 있음.

---

# XSS (Cross Site Scripting)

- 공격자에 의해 작성된 스크립트가 다른 사용자에게 전달되는 기법
- 다른 사용자의 웹 브라우저 내에서 적절한 검증 없이 실행되기 때문에 사용자의 세션을 탈취하거나, 웹 사이트를 변조하거나 혹은 악의적인 사이트로 사용자를 이동시킬 수 있다.

### 공격 유형

1. Stored XSS : 가장 일반적인 유형. 단순한 게시판 or 자료실과 같이 사용자가 글을 저장할 수 있는 부분에 정상적인 평문이 아닌 스크립트 코드를 입력하는 기법

2. Reflected XSS : 공격 스크립트가 포함된 공격 URL을 사용자가 클릭할 때 악성 스크립트가 서버 사이트에 의해 HTML 문서로 반사되어 웹 브라우저에서 실행되어 서버에 흔적을 남기지 않고 공격을 수행할 수 있다.

### 보안대책

- 사용자가 입력한 문자열의 <,>,&," 등을 문자 변환 처리를 하여 &lt,&gt,&amp,&quot로 치환한다.
- HTML 태그를 허용하는 게시판에서는 지원하는 HTML 태그의 리스트를 선정한 후, 해당 태그만 허용하는 방식을 적용한다.