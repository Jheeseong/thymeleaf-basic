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
