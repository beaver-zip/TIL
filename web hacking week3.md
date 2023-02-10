## CSRF
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


---

## SQL Injection
- 사용자 입력 데이터가 SQL Query에 포함되어 의도되지 않은 Query문이 실행되는 취약점.
- SQL Injection을 방지하기 위해서는 사용자 데이터가 SQL Query로써 동작하지 못하도록 해야한다.
 

### 목적
1. 정보 탈취 (기밀성 침해)
2. 정보 수정/삭제 (무결성 침해)

-> 결국 기존에 권한이 없는 DB 정보에 접근하는 것이 공통점이다. 이러한 공격을 위해서 다음 과정을 거쳐 공격을 수행하게 된다.

### 진행 과정
1. SQL Injection 취약점 발견
 - HTTP Response Status Code를 통해 오류가 발생하는지 확인
 - DBMS의 오류 메시지를 통해 취약점 가능성 확인
 - 웹 어플리케이션에서 변조된 SQL구문이 실행된 데이터가 반환되는지 확인

2. 구문 예측 / DBMS 정보 획득
 - 사용자의 입력 데이터를 처리하는 구문을 예측한다. (Query문 예측)
 - DBMS의 정보를 획득하여 Exploit 작성을 위한 정보를 획득한다.

3. Exploit 작성
 - 사용할 공격 기법을 선정합니다.
 - WAF와 같이 SQL Injection를 방어하는 로직 등이 존재할 경우 우회 가능성을 판단한다.

4. 정보 탈취 및 수정/삭제
 - 시스템 테이블 등을 이용해 DB의 정보를 획득하고, 저장된 데이터를 탈취하거나 수정/삭제 하여 공격
 

### SQL Injection 취약점이 발생시 공격법
<br>

**Logic**

 and, or 와 같은 Logic을 이용한 공격이다.
 and 연산자는 첫 번째 피연산자가 True일 경우에만 두 번째 피연산자를 연산한다는 특징,
 그리고 or 연산자는 첫 번째 피연산자가 False일 경우에만 두 번째 피연산자를 연산한다는 특징을
 활용해 SQL Injection 공격을 수행할 수 있다.

**Union**

 양쪽의 결과를 결합해주는 Union 명령어를 이용한 공격이다.
 왼쪽의 결과가 화면에 나온다면, 오른쪽에 공격자가 임의의 Query를 생성하고 이 결과가 결합되면서 같이 화면에 나오는 점을 이용해 SQL Injection 공격을 수행할 수 있다.

**Subquery**

  Select절, From절, Where절에 사용되는 SubQuery를 사용해 SQL Injection 공격을 수행한다.

<br>

### SQL Injection 취약점이 발생했을 때 상황별 접근법
<br>


**Error Based**

 임의로 에러를 발생시켜 정보를 획득하는 공격 기법이다. SQL Injection이 발생했을 때 결과가 나오지는 않지만 Query문에 Error가 발생했을 때 공격자에게 이 Error가 노출되는 상황에 사용이 가능하다.
 (Syntax Error가 아니라 Runtime중에 발생하는 Error가 필요하다.)

**Blind**

 DB 조회 후 결과를 공격자가 직접 확인할 수 없는 상황에서 사용되는 SQL Injection 공격기법이다.
 1. 데이터를 비교해 참/거짓을 구분한다.
 2. 참/거짓의 결과에 따른 특별한 응답을 생성한다.
 