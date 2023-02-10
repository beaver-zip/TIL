### CSRF
- Cross Site Request Forgery의 약자로, 공격자가 악의적으로 사용자의 의도와 다르게 다른사이트에서 HTTP Request를 보내는 공격
- 공격자는 CSRF를 통해 Cookie/Session을 가져야만 사용할 수 있는 기능에 대해 Request를 보낼 수 있다.

 
### CSRF의 최소 조건
1. 해당 Web 페이지가 Cookie를 사용한 인증 방식이여야 한다. (Cookie에 Session값을 저장하는 것도 결국 Cookie를 사용한 방식이기 때문에 가능하다.)
2. 공격자가 사전에 알 수 없는 파라미터가 있으면 안된다. (자동입력방지문자, 패스워드 변경기능에서 기존 패스워드와 같은 항목이 이에 해당된다.)

### 예시
아래 코드에 대해서 사용자가 실행하게되면 CSRF 취약점이 발생한다.
```html
<img src='/sendmoney?to=slolee&amount=1337'>
<img src=about: onerror="fetch('/sendmoney?to=slolee&amount=1337')">
<link rel="stylesheet" href="/sendmoney?to=slolee&amount=1337">
```

CSRF의 경우 포인트는 XSS와 매우 유사하다. 그러나 사용자에게 그 포인트가 발생했을 때 동작하는 방식에 차이가 있다. XSS는 악성 Script가 실행되지만, CSRF는 서버에게 원하지 않는 HTTP Request를 보내게 된다.

따라서 포인트를 찾기 위한 방법과 여러 우회방법은 XSS에 대한 자료를 참고하자.

### CSRF 방어
Session을 Cookie 대신 커스텀 헤더를 사용해 사용자를 인증한다.
공격자가 예측할 수 없는 파라미터를 추가하고, 그에 대해 검증함으로써 CSRF 공격을 방어할 수 있다.