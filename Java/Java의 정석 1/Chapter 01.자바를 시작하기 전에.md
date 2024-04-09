Java의 정석 1
===========

# Chapter 01 자바를 시작하기 전에

## 1. 자바(Java Programming Language)

### 1.1 자바란?

자바는 썬 마이크로시스템즈(Sun Microsystems)에서 개발하여 1996년 1월에 공식적으로 발표한 객체지향 프로그래밍 언어이다.   

자바의 가장 중요한 특징은 운영체제(Operating System, 플랫폼)에 독립적이라는 것이다.   

### 1.2 자바의 역사

가전제품에 탑재될 소프트웨어를 만들기 위해 C++을 확장해서 사용하려 했지만 부족하다는 것을 깨닫고 C++의 장점을 도입하고 단점을 보완한 새로운 언어를 개발해 탄생한 언어이다.   

자바로 작성된 애플릿(Applet)은 보안상의 이유로 최신 웹브라우져에서 더 이상 지원하지 않게 되고 서버 쪽 프로그래밍을 위한 서블릿(Servlet)과 JSP(Java Server Pages)가 많이 사용되고 있다.

### 1.3 자바언어의 특징

1. 운영체제에 독립적이다.
   - 자바 응용프로그램은 운영체제나 하드웨어가 아닌 JVM하고만 통신하고 JVM이 자바 응용프로그램으로부터 전달받은 명령을 해당 운영체제가 이해할 수 있도록 변환하여 전달한다. 따라서 JVM은 운영체제에 종속적이다.
2. 객체지향언어이다.
3. 비교적 배우기 쉽다.
4. 자동 메모리 관리(Garbage Collection)
5. 네트워크와 분산처리를 지원한다.
   - 다양한 네트워크 프로그래밍 라이브러리(Java API)를 통해 비교적 짧은 시간에 네트워크 관련 프로그램을 쉽게 개발할 수 있도록 지원한다.
6. 멀티쓰레드를 지원한다.
   - 자바에서 개발되는 멀티쓰레드 프로그램은 관련된 라이브러리(Java API)가 제공되므로 구현이 쉽고 여러 쓰레드에 대한 스케줄링(scheduling)을 자바 인터프리터가 담당하게 된다.
7. 동적 로딩(Dynamic Loading)을 지원한다.
   - 실행 시에 모든 클래스가 로딩되지 않고 필요한 시점에 클래스를 로딩하여 사용할 수 있다는 장점이 있다.

### 1.4 JVM(Java Virtual Machine)

![JVM](https://github.com/jeuskim/Study/assets/165736497/ddc67d71-24ed-4b20-87a3-33928deed60f)



***

## 2. 자바개발환경 구축하기

### 2.1 자바 개발도구(JDK)설치하기

- JRE(Java Runtime Environment) : 자바실행환경(자바로 작성된 응용프로그램이 실행되기 위한 최소환경)
  - = JVM + 클래스라이브러리(Java API)
- JDK(Java Development Kit) : 자바개발도구
  - = JRE + 개발에 필요한 실행파일(javac.exe 등)
    - JDK의 bin디렉토리에 있는 주요 실행파일
      - javac.exe : 자바 컴파일러(자바소스코드를 바이트코드로 컴파일한다.)
        javac Hello.java
      - java.exe : 자바 인터프리터(컴파일러가 생성한 바이트코드를 해석하고 실행한다.)
        java Hello
      - javap.exe : 자바 역어셈블러(컴파일된 클래스파일을 원래의 소스로 변환한다.)
        javap Hello > Hello.java
      - javadoc.exe : 자동문서생성기(소스파일에 있는 주석을 이용하여 Java API문서와 같은 형식의 문서를 자동으로 생성한다.)
        javadoc Hello.java
      - jar.exe : 압축프로그램(클래스파일과 프로그램의 실행에 관련된 파일을 하나의 jar파일(.jar)로 압축하거나 압축해제한다.)
        jar cvf Hello.jar Hello1.class Hello2.class(압축할 때)
        jar xvf Hello.jar(압축 풀 때)

### 2.2 Java API문서 설치하기



***

## 3. 자바로 프로그램작성하기

### 3.1 Hello.java

- Java 애플리케이션은 main메서드의 호출로 시작해서 main메서드의 첫 문장부터 마지막 문장까지 수행을 마치면 종료된다.
  따라서 하나의 Java 애플리케이션에는 main메서드를 포함한 클래스가 반드시 하나는 있어야 한다.
- public class가 있는 경우, 소스파일의 이름은 반드시 public class의 이름과 일치해야 한다.
  만약 public class가 없는 경우, 소스파일의 이름은 아무 class의 이름으로 해도 무관하다.
  이 때 하나의 소스파일에 둘 이상의 public class가 존재하면 안된다.



### 3.2 자주 발생하는 에러와 해결방법

1. cannot find symbol 또는 cannot reslove symbol
   - 변수 또는 메서드의 이름을 잘못 사용한 경우에 발생한다.

2. ';' expected
   - 문장의 끝에 ';'이 없다는 뜻이다.

3. Exception in thread "main" java.lang.NoSuchMethodError: main
   - 클래스 내에 main메서드가 존재하지 않거나 메서드의 선언부에 오타가 존재하는 경우에 발생한다.

4. Exception in thread "main" java.lang.NoClassDefFoundError: Hello
   - 'Hello라는 클래스를 찾을 수 없다'는 뜻이다. 클래스파일이 생성되었는지 확인한다.
     클래스파일이 존재하는데도 동일한 메시지가 나타난다면 클래스패스의 설정이 바르게 되었는지 다시 확인한다.

5. illegal start of expression
   - 문장에 문법적 오류가 있다는 뜻이다.

6. class, interface, or enum expected
   - '키워드 class나 interface 또는 enum이 없다.'는 의미로 보통 괄호 '{' 또는 '}'의 개수가 일치 하지 않는 경우에 발생한다.



### 3.3 자바프로그램의 실행과정

내부적인 진행 순서

1. 프로그램의 실행에 필요한 클래스(*.class파일)를 로드한다.
2. 클래스파일을 검사한다.(파일형식, 악성코드 체크)
3. 지정된 클래스(Hello)에서 main(String[] args)를 호출한다.

main메서드의 첫 줄부터 코드가 실행되기 시작하며 마지막 코드까지 모두 실행되면 프로그램이 종료되고, 프로그램에서 사용했던 자원들은 모두 반환된다.



### 3.4 주석(comment)

- ctrl + shift + L : 단축키 전체 목록보기
- ctrl + =/- : 확대/축소
- ctrl + D : 한 줄 삭제
- ctrl + alt + shift + up/down : 행 단위 위로/아래로 복사
- alt + shift + A : 멀티컬럼 편집
- alt + up/down : 행 단위 위로/아래로 이동
- ctrl + i : 자동 들여쓰기
- ctrl + / : 한 줄 주석(토글)
- ctrl + space : 자동완성



### 3.5 이 책으로 공부하는 방법

- 1장 ~ 5장 : 프로그래밍의 기본
- 6장 ~ 9장 : 자바의 기본
  - 6장 : 객체지향 개념의 핵심(복습을 자주 할 것)
  - 7장 : 객체지향 개념의 핵심인 다형성(polymorphism)(복습을 자주 할 것)
- 10장 ~ 16장 : 자바의 응용
  - 11, 12, 15장은 필수

***

