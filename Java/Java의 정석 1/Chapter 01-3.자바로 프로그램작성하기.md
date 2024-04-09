Java의 정석 1
===========

# Chapter 01 자바를 시작하기 전에

## 1. 자바(Java Programming Language)

### 1.1 자바란?

### 1.2 자바의 역사

### 1.3 자바언어의 특징

### 1.4 JVM(Java Virtual Machine)



***

## 2. 자바개발환경 구축하기

### 2.1 자바 개발도구(JDK)설치하기

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

