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

### 3.2 자주 발생하는 에러와 해결방법

### 3.3 자바프로그램의 실행과정

### 3.4 주석(comment)

### 3.5 이 책으로 공부하는 방법

***

