# thymeleaf-basic
# v1.0 3/10
# 타임리프 특징
- 서버 사이드 HTML 렌더링(SSR)
- 네츄럴 템플릿
- 스프링 통합 지원

**서버 사이드 HTML 렌더링(SSR)
- 백엔드 서버에서 HTML을 동적으로 렌더링하는 용도로 사용

**네츄럴 템플릿**
- 순수 HTML을 유지하면서 뷰 템플릿도 사용이 가능한 특징
  - 타임리프로 작성한 파일은 HTML을 유지하여서 웹 브라우저에서 파일을 직접 열어도 내용 확인이 가능
  - 서버를 통해 실행 시 동적으로 변경된 결과 확인이 가능
  - JSP를 포함한 다른 뷰 템플릿 경우, 해당 파일을 열면 소스코드와 HTML이 섞여서 확인이 어려움

**스프링 통합 지원**
- 스프링과 통합하여 지원이 가능하며 다른 기능 역시 사용이 가능하도록 지원

# 타임리프 기본 기능
**타임리프 사용 선언**
- html xmlns:th="http://www.thymeleaf.org"

**기본 표현식**
- 간단한 표현:
  - 변수 표현식: ${...}
  - 선택 변수 표현식: *{...}
  - 메시지 표현식: #{...}
  - 링크 URL 표현식: @{...}
  - 조각 표현식: ~{...}
- 리터럴
  - 텍스트: 'one text', 'Another one!',…
  - 숫자: 0, 34, 3.0, 12.3,…
  - 불린: true, false
  - 널: null
  - 리터럴 토큰: one, sometext, main,…
- 문자 연산:
  - 문자 합치기: +
  - 리터럴 대체: |The name is ${name}|
- 산술 연산:
  - Binary operators: +, -, *, /, %
  - Minus sign (unary operator): -
- 불린 연산:
  - Binary operators: and, or
  - Boolean negation (unary operator): !, not
- 비교와 동등:
  - 비교: >, <, >=, <= (gt, lt, ge, le)
  - 동등 연산: ==, != (eq, ne)
- 조건 연산:
  - If-then: (if) ? (then)
  - If-then-else: (if) ? (then) : (else)
  - Default: (value) ?: (defaultvalue)
- 특별한 토큰:
  - No-Operatio
# v1.1 3/11
# 텍스트 - text,utext
- 텍스트 출력하는 기능
- HTML의 콘텐츠에 데이터 출력할 때 th:text 사용
- HTML 콘텐츠 영역 안에서 직접 데이터 출력 시 [[...]] 사용
- th:text 사용 : span th:text="${data}"
- 컨텐츠 안에서 직접 출력 : [[${data}]]

**Escape**
- 뷰 템플릿으로 HTML 화면을 생성 할 때는 출력하는 데이터에 <,> 같은 특수 문자를 주의

**HTML 엔티티**
- 웹 브라우저는 <를 HTML 테그 시작으로 인식
- < 테그를 시작이 아닌 문자로 표현하는 방법이 HTML 엔티티
- HTML에서 사용하는 특수 문자를 HTML 엔티티로 변경하는 것을 **이스케이프**
- th:inline="none" 타임리프는 [[...]]를 해석하기 떄문에, 글자를 보여주지 않음
- 이 테그 안에서는 타임리프가 해석하지 않음

# 변수 - SpringEL
- 변수 표현식 : ${...}

**Object**

-  th:text="${user.username}" : user의 username을 프로퍼티 접근
-  th:text="${user['username']}" : user의 username을 프로퍼티 접근
-  th:text="${user.getUsername()}" : user의 getUsername을 직접 호출

**List**
- th:text="${users[0].username}" : List에서 첫번째 회원을 찾고 username 프로퍼티 접근
- th:text="${users[0]['username']}"" : List에서 첫번째 회원을 찾고 username 프로퍼티 접근
- th:text="${users[0].getUsername()}" : List에서 첫번쨰 회원을 찾고 메서드 직접 호출

**Map**
- th:text="${userMap['userA'].username}" : Map에서 UserA를 찾고, username 프로퍼팇 접근
- th:text="${userMap['userA']['username']}" : Map에서 UserA를 찾고, username 프로퍼팇 접근
- th:text="${userMap['userA'].getUsername()}" : Map에서 UserA를 찾고, 메서드 직접 호출

# 지역 변수 선언
- th:with를 사용

      th:with="first=${users[0]}" 
      th:text="${first.username}  
- first.username 호출을 통해 선언한 지역 변수를 사용

# 기본 객체들
- ${#request}
- ${#response}
- ${#session}
- ${#servletContext}
- ${#locale}

**#request**
- #request 경우 HttpServletRequest 객체가 그대로 제공되기 떄문에 조회 시 힘들게 접근해야 함

**해결법**
- HTTP 요청 파라미터 접근: param
  - ex) ${param.paramData}
- HTTP 세션 접근: session
  - ex) ${session.sessionData}
- 스프링 빈 접근: @
  - ex) ${@helloBean.hello('Spring!')}
