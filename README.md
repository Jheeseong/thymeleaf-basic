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

# v1.2 3/12
# 유틸리티 객체와 날짜

**타임리프 유틸리티 객체들**
- #message : 메시지, 국제화 처리
- #uris : URI 이스케이프 지원
- #dates : java.util.Date 서식 지원
- #calendars : java.util.Calendar 서식 지원
- #temporals : 자바8 날짜 서식 지원
- #numbers : 숫자 서식 지원
- #strings : 문자 관련 편의 기능
- #objects : 객체 관련 기능 제공
- #bools : boolean 관련 기능 제공
- #arrays : 배열 관련 기능 제공
- #lists , #sets , #maps : 컬렉션 관련 기능 제공
- #ids : 아이디 처리 관련 기능 제공, 뒤에서 설명

# URL 링크
- 타임리프에서 URL을 생성할 때 @(...) 문법 사용
- ex) th:gref="@{/hello}"
- 쿼리 파라미터
  - ()에 있는 부분은 쿼리파라미터로 처리
  - ex) th:href="@{/hello(param1=${param1}, param2=${param2})}"
- 경로 변수
  - URL 경로상에 변수가 있으면 ()부분은 경로 변수로 처리
  - ex) th:href="@{/hello/{param1}/{param2}(param1=${param1}, param2=${param2})}"
- 경로 변수 + 쿼리 파라미터
  - 경로 변수와 쿼리 파라미터를 함꼐 사용
  - ex)  th:href="@{/hello/{param1}(param1=${param1}, param2=${param2})}"

# 리터럴
- 소수 코드 상에 고정된 값, ex) "hello", 10, 20
- 문자 리터럴은 항상 '(작은 따옴표)가 필수
- 띄어쓰기는 하나의 의미있는 문자여서 인식되지 않음 ex) th"text="hello world"는 인식되지 않음

**리터럴 대체**
- '(작은 따옴표) 대신 |(리터럴 대체 문법)를 사용한다면 가능
  - ex) th:text="|hello ${data}|"

# 연산
- 비교 연산 : HTML 엔티티 사용하는 부분을 조심
  - >(gt), <(lt), >=(ge), <=(le), !(not), ==(eq), !=(neq, ne)
- 조건식 : 자바의 조건식과 유사
- Elvis 연산자 : 조건식의 편의 버전
- No-Operation : _ 인 경우 타임리프가 실행되지 않는 것처럼 동작하며 이를 사용하여 HTML의 내용 그대로 활용이 가능

# v1.3 3/13
# 속성 값 설정
**타임리프 태그 속성**
- 타임리프는 HTML 태그에 th:* 속성을 지정하는 방식으로 동작
- th:attrappend : 속성 값의 뒤에 값을 추가
- th:attrprepend : 속성 값의 앞에 값을 추가
- th:classappend : class 속성에 자연스럽게 추가

**checked 처리**
- HTML에서는 checked="false" 처리 시에도 checked 속성이 있기 떄문에 checked 처리가 됨
- 이와 달리 타임리프의 th:checked는 값이 false인 경우 checked 속성 자체를 제거

# 반복
- th:each 문법을 사용
  - ex) th:each="user : ${users}
- 반복 시 오른쪽 컬렉션($(user))의 값을 하나씩 꺼내어 왼족 변수(user)에 담아서 태그 반복
- th:each 는 List, 배열, Iterable, Enumeration을 구현한 모든 객체 반복에 사용 가능, map도 사용 가능하나 변수에 답기는 값은 map.Entry

**반복 상태 유지**
-  th:each="user, userStat : ${users}"
- 반복의 두번쨰 파라미터를 설정하여 반복의 상태 확인이 가능 
- 두번째 파라미터는 생략이 가능한데, 생략 시 지정한 변수명(user) + stat 가 됨

**반복 상태 유지 기능**
- index : 0부터 시작하는 값
- count : 1부터 시작하는 값
- size : 전체 사이즈
- even , odd : 홀수, 짝수 여부( boolean )
- first , last :처음, 마지막 여부( boolean )
- current : 현재 객체

# 조건부 평가
- if, unless
  - ex) th:if="${user.age lt 20}", th:unless="${user.age ge 20}"
- 타임리프는 해당 조건이 맞지 않을 시 태그 자체를 랭더링 X
- 조건이 false 인 경우 span 부분을 랜더링하지 않고 삭제
- switch
  - * 은 만족하는 조건이 없을 경우 사용하는 디폴트

# v1.4 3/14
# 주석
- 표준 HTML 주석
  - <!-- -->
  - 타임리프가 렌더링 하지 않고, 그대로 남겨둠
- 타임리프 파서 주석
  - <!--* */-->
  - 타임리프가 렌더링에서 주석 부분을 제거
- 타임리프 프로토타입 주석
  - <!--/*/ /*/-->
  - HTML 파일을 웹 브라우저에서 확인해 볼 때 HTML 주석으로 인식하여 렌더링 X
  - 타임리프 렌더링 한 경우 보이는 기능

# 블록
- th:block
- 타임리프 특성 상 HTML 태그안에 속성으로 기능 정의 후 사용하는데, 애매한 경우 사용
- 블록은 렌더링 시 제거
- ex) 

      <th:block th:each="user : ${users}">
       <div>
       사용자 이름1 <span th:text="${user.username}"></span>
       사용자 나이1 <span th:text="${user.age}"></span>
       </div> <div>
       요약 <span th:text="${user.username} + ' / ' + ${user.age}"></span>
       </div>
      </th:block>
      
# 자바스크립트 인라인
- th:inline="javascript"
- **텍스트 렌더링**
  - 인라인 사용 전 -> var username = userA;
  - 인라인 사용 후 -> var username = "userA";
  - 인라인 사용 전으로 적용 시 변수명 그대로 사용하여 오류가 발생
  - 인라인 사용 시 문자 타입의 경우 "를 포함해줌으로 오류 해결이 가능하며 이스케이프 처리도 함
- **자바스크립트 내추럴 템플릿**
  - var username2 = /*[[${user.username}]]*/ "test username";
  - 인라인 사용 전 var username2 = /* userA */ "test username";
  - 인라인 사용 후 var username2 = "userA";
- **객체**
  - 객체를 JSON으로 자동 변환
  - var user = [[${user}]];
  - 인라인 사용 전 var user = BasicController.User(username=userA, age=10);
  - 인라인 사용 후 var user = {"username":"userA","age":10};
- **자바스크립트 인라인 each**
- [# th:each="user, stat : ${users}"]
  - 결과 : var user1 = {"username":"userA","age":10}; var user2 = {"username":"userB","age":20}; ....

# v1.5 3/15
# 탬플릿 조각
- 공통 영역 부분(상단, 하단, 좌측 카테고리 등)을 코드를 복사하여 사용하지 않고 템플릿 조각으로 가져와 사용
- template/fragment/footer.html 안의 th:fragment="copy"
  - 다른 곳에 포함되는 코드 조각
- template/fragment/fragmentMain.html 안의 th:insert="~{template/fragment/footer :: copy}"
  - footer 템플릿 안에 있는 th:fragment="copy" 부분을 템플릿 조각으로 가져와 사용한다는 의미

**th:insert**
- 현재 태그(div)내부에 추가

**th:replace**
- 현재 태그(div)를 대체

**파라미터 사용**
-  th:replace="~{template/fragment/footer :: copyParam ('데이터1', '데이터2')}"
-  fragment의 파라미터를 받아서 동적으로 렌더링

# 템플러 레이아웃
- 코드 조각을 레이아웃에 넘겨서 사용하는 방법
- 예를 들어 HEAD 에 공통으로사용하는 정보들을 한 곳에 모아두고 사용하지만, 각페이지마다 필요한 정보를 더 추가해서 사용도 가
- th:replace="template/layout/base :: common_header(~{::title},~{::link})"
  - ::title은 현재 페이지의 title 태그들을 전달
  - ::link는 현재 페이지의 link 태그들을 전달
- 공통 부분은 유지되고 타이틀,링크들이 교체 및 포함 된 것이 확인 가능

# 템플릿 레이아웃 확장
- HEAD 뿐만 아니라 html 전체에 적용이 가능
- th:fragment 속성이 정의된 html을 기본으로 하고 필요한 내용을 전달해서 일부분을 변경
