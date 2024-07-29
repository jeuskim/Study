# Part 01 웹의 동작 원리와 서블릿

# Chapter 02 HTTP 프로토콜과 요청 방식

## 2.1 HTTP 개요

- HTTP(HyperText Transfer Protocol)

  > 웹에서 클라이언트인 브라우저와 서버가 통신할 때 사용하는 통신 규약

#### 2.1.1 프로토콜 개념

- 프로토콜 지정

  > 통신에 참여한 주체들이 합의한 메시지의 형식을 지정

- 프로토콜 변경

  - XML이나 JSON은 전달하려는 데이터와 데이터에 대한 메타데이터가 함께 전달되기 때문에 데이터를 좀 더 쉽고 명확하게 처리할 수 있다.

#### 2.1.2 HTTP 개념

- 웹 클라이언트와 웹 서버
  - 웹 클라이언트: 일반적으로 브라우저를 의미한다.
  - 웹 서버: 제우스(JEUS), 웹로직(WebLogic), 웹스피어(WebSphere)
  
- HTTP 특징
  - 비연결성(connectionless)
  
    > 브라우저가 서버에 특정 문서를 요청하는 순간, 잠깐 서버와 연결됐다가 서버로부터 응답이 전송된 후 곧바로 끊어지는 것을 의미한다.
  
  - 무상태(stateless)
  
    > 웹 서버가 웹 클라이언트의 상태 정보를 유지하지 않는 것을 의미한다.
    >
    > 상태 정보: 브라우저가 서버에게 요청을 전달하면서 함께 전달된 데이터를 의미한다.

#### 2.1.3 HTTP 요청 프로토콜

- HTTP 요청 URL(Uniform Resource Locator)

  > 사용자가 버튼을 누르거나 하이퍼링크를 클릭하는 순간 브라우저는 HTTP 요청 URL을 서버에 전달한다.
  >
  > 브라우저: HTTP 요청 프로토콜을 웹 서버에 전달하고, 웹 서버가 전송한 HTTP 응답 프로토콜을 처리한다.

  - http: // localhost : 8080 / BoardWeb / board / login.html
    - 프로토콜(http:) : 서버에 파일을 요청할 때 사용한 프로토콜
    - 프로토콜 구분자(//) : 프로토콜과 호스트 이름을 구분하는 구분자
    - 호스트(도메인)(localhost) : 웹 서버가 설치된 컴퓨터(호스트)
    - 포트(8080) : 호스트 컴퓨터에서 8080 포트를 사용하는 서버
    - 웹 애플리케이션(BoardWeb) : 8080 포트를 사용하는 서버에서 실행되는 BoardWeb이라는 웹 애플리케이션
    - 디렉터리(board) : BoardWeb 애플리케이션의 board 디렉토리
    - 파일(login.html) : board 디렉토리에 있는 login.html 파일

- HTTP 요청 프로토콜 구조

  - start-line

    > 요청과 관련된 세 가지 핵심 정보가 포함된다.
    >
    > 예: GET BoardWeb/board/login.html HTTP/1.1

    - 요청 방식

      > GET(조회), POST(등록), PUT(수정), DELETE(삭제) 등

    - 요청 URI(Uniform Resource Identifier)

      > URL에서 포트 번호 이후의 문자열을 의미한다.

    - 프로토콜/버전

      > 일반적으로 웹에서 사용하는 HTTP 프로토콜은 1.1 버전을 사용한다.

  - message-header

    > 키(key):값(value) 형태로 정보가 설정되는 브라우저와 관련된 정보

    - 키(key)
      - Host : 요청하려는 서버 호스트 이름과 포트 번호
      - User-agent : 브라우저의 이름과 버전 정보
      - Accept : 브라우저가 처리할 수 있는 MIME Type 목록
      - Accept-charset : 브라우저가 처리할 수 있는 문자열 인코딩 목록
      - Accept-language : 브라우저가 처리할 수 있는 언어 목록
      - Accept-encoding : 브라우저가 처리할 수 있는 압축 방식
      - Cookie : key-value 형태의 쿠키 정보

  - message-body

    > 사용자가 입력한 정보들이 설정

#### 2.1.4 HTTP 응답 프로토콜

- status-line

  - 프로토콜/버전

    > HTTP 요청과 마찬가지로 HTTP/1.1 버전을 사용한다.

  - 상태 코드(status code)

    - 200 : 정상적인 처리
    - 403 : 브라우저가 요청한 파일에 접근할 수 없음
    - 404 : 브라우저가 요청한 파일이 서버에 존재하지 않음
    - 405 : 브라우저가 요청한 방식(method)을 서버에서 지원하지 않음
    - 500 : 브라우저가 요청한 기능을 서버가 처리하는 과정에서 예외(Exception) 발생함

  - 상태 메시지(status text)

    > 상태 코드의 의미를 쉽게 설명하기 위한 간단한 메시지다.

    - 200 : OK
    - 403 : Forbidden
    - 404 : Not Found
    - 405 : Method Not Allowed
    - 500 : Internal Server Error

- message-header

  > 서버가 브라우저에게 응답으로 전송하는 문서의 정보가 설정된다.

- message-body

  > 브라우저가 요청한 실질적인 문서가 포함된다.

#### 2.1.5 GET/POST 요청 방식

- GET 요청

  > 서버에 전달한 URI 뒤에 물음표(?)를 추가하고 키(key) = 값(value) 형태로 사용자가 입력한 정보를 전달하는데, 만약 입력한 정보가 여러 개일 경우에는 &로 연결한다.
  > 이를 쿼리 문자열(query string)이라고 한다.

- POST 요청

  > 쿼리 문자열이 요청 URI가 아닌 message-body에 포함되어 전달되어 브라우저 URI에 사용자가 입력한 정보가 노출되지 않는다.

---

## 2.2 사용자 요청과 서블릿

#### 2.2.1 서블릿 작성

> 브라우저: HTML을 통해 서버에 요청을 전달
>
> 서버: 요청과 함께 사용자가 전달한 정보를 추출하여 요청된 기능을 처리
>
> 서블릿: 서버에서 사용자의 요청을 처리하는 대표적인 자바 기술

```java
// LoginServlet.java
package com.ssamz.web.user;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class LoginServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    public LoginServlet() {
        System.out.println("===> LoginServlet 생성");
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8");
        response.setCharacterEncoding("UTF-8");
        System.out.println("---> GET 방식의 요청 처리");
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8");
        response.setCharacterEncoding("UTF-8");
        System.out.println("---> POST 방식의 요청 처리");
    }
}

```



#### 2.2.2 web.xml 수정

> 웹 애플리케이션 전체 환경을 기술하는 매우 중요한 환경설정 파일

```xml
<!-- web.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <display-name>BoardWeb</display-name>

    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>com.ssamz.web.filter.CharacterEncodingFilter</filter-class>
    </filter>

    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <servlet>
        <servlet-name>loginProcess</servlet-name>
        <servlet-class>com.ssamz.web.user.LoginServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>loginProcess</servlet-name>
        <url-pattern>/loginProcess</url-pattern>
    </servlet-mapping>
</web-app>

```



```java
// CharacterEncodingFilter.java
package com.ssamz.web.filter;

import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

public class CharacterEncodingFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        // Initialization code if needed
    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        request.setCharacterEncoding("UTF-8");
        response.setContentType("text/html; charset=UTF-8");
        response.setCharacterEncoding("UTF-8");
        chain.doFilter(request, response);
    }

    @Override
    public void destroy() {
        // Cleanup code if needed
    }
}

```



#### 2.2.3 요청 처리 방식

- POST 요청 처리
- GET 요청 처리

---

## Tip

#### IntelliJ Server Console 한글 출력

- File > Settings > Editor > File Encodings > Global Encoding, Project Encoding, Default encoding for properties files를 'UTF-8'로 설정
- Run > Edit Configurations > Tomcat 설정 > Server 탭 > VM options 필드에
  ```-Dfile.encoding=UTF-8``` 내용 추가
- Help > Edit Custom VM Options  필드에
  ```-Dfile.encoding=UTF-8``` 내용 추가
- Tomcat의 'bin' 디렉토리 내에 'setenv.bat' 파일을 생성 후
  ```set "JAVA_OPTS=%JAVA_OPTS% -Dfile.encoding=UTF-8"``` 내용 추가
- Tomcat Server 종료 및 IntelliJ 종료 후 재시작
