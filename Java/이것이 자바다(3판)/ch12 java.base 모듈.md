# ch12 java.base 모듈

## 12.1 API 도큐먼트

- API(Application Programming Interface) 도큐먼트

  > 자바 표준 모듈에서 제공하는 라이브러리를 사용하기 위한 방법을 기술

---

## 12.2 java.base 모듈

- 모든 모듈이 의존하는 기본 모듈로, 모듈 중 유일하게 requires하지 않아도 사용할 수 있다.
- java.lang: 자바 언어의 기본 클래스를 제공
  - Object: 자바 클래스의 최상위 클래스로 사용
    - System: 키보드로부터 데이터 입력, 모니터(콘솔)로 출력, 프로세스 종료, 진행 시간 읽기, 시스템 속성(프로퍼티) 읽기
    - String: 문자열을 저장 및 조작
    - StringBuilder: 효율적인 문자열 조작 기능이 필요할 때 사용
    - Character, Boolean: 기본 타입의 값 포장, 문자열을 기본 타입으로 변환
    - Number
      - Byte, Short, Integer, Float, Double: 상동
    - Math: 수학 계산이 필요할 때 사용
    - Class: 클래스의 메타 정보(이름, 구성 멤버) 등 조
- java.util: 자료 구조와 관련된 컬렉션 클래스를 제공
  - StringTokenizer: 구분자로 연결된 문자열을 분리할 때 사용
- java.text: 날짜 및 숫자를 원하는 형태의 문자열로 만들어 주는 포맷 클래스를 제공
- java.time: 날짜 및 시간을 조작하거나 연산하는 클래스를 제공
- java.io: 입출력 스트림 클래스를 제공
- java.nio: 데이터 저장을 위한 Buffer 및 새로운 입출력 클래스 제공

---

## 12.3 Object 클래스

- 자바의 모든 클래스의 부모 클래스
- 주요 메소드
  - ```boolean equals(Object obj)``` : 객체의 번지를 비교하고 결과를 리턴
  - ```int hashCode()``` : 객체의 해시코드를 리턴
  - ```String toString()``` : 객체 문자 정보를 리턴

#### 12.3.1 객체 동등 비교

- ```boolean equals(Object obj)```
  - 일반적으로 재정의해서 동등 비교용으로 사용된다.(내부 데이터 비교)


#### 12.3.2 객체 해시코드

- ```int hashCode()```
  - 일반적으로 재정의해서 새로운 정수값을 리턴하도록 한다.(내부 데이터가 같으면 같은 정수값 리턴)

#### 12.3.3 객체 문자 정보

- ```String toString()```
  - 객체의 문자 정보를 리턴하도록 재정의하기도 한다.(Date, String 클래스 등등)

#### 12.3.4 레코드 선언

- 레코드(record): 데이터 전달을 위한 DTO(Data Transfer Object)를 작성할 때 반복적으로 사용되는 코드를 줄이기 위해 사용
  - 필드는 private final로 선언
  - 필드명과 동일한 메소드명의 Getter 생성
  - 동등 비교를 위한 hashCode(), equals() 메소드 재정의
  - 클래스명[필드명=필드값, ...] 출력하는 toString() 메소드 재정의

#### 12.3.5 롬복 사용하기

- 롬복(Lombok): 자동 코드 생성 라이브러리(JDK에 포함된 표준 라이브러리가 아니다.)

  > 레코드와 유사하지만 필드가 final이 아니다.
  >
  > getXxx(or isXxx) 이름의 Getter와 setXxx 이름의 Setter 생성한다.

---

## 12.4 System 클래스

- 정적 필드
  - out: 콘솔(모니터)에 문자 출력
  - err: 콘솔(모니터)에 에러 내용 출력
  - in: 키보드 입력
- 정적 메소드
  - exit(int status): 프로세스 종료
  - currentTimeMillis(): 현재 시간을 밀리초 단위의 long 값으로 리턴
  - nanoTime(): 현재 시간을 나노초 단위의 long 값으로 리턴
  - getProperty(): 운영체제와 사용자 정보 제공
  - getenv(): 운영체제의 환경 변수 정보 제공

#### 12.4.1 콘솔 출력

- 정적 필드 out, err

- ```java
  public static final PrintStream out = null;
  public static final PrintStream err = null;
  // out = new PrintStream(new BufferedOutputStream(new FileOutputStream(FileDescriptor.out)));
  // err = new PrintStream(new BufferedOutputStream(new FileOutputStream(FileDescriptor.err)));
  ```



#### 12.4.2 키보드 입력

- 정적 필드 in

  - read() 메소드를 호출하면 입력된 키의 코드값을 int 타입으로 얻을 수 있다.

- ```java
  public static final InputStream in = null;
  // in = new FileInputStream(FileDescriptor.in);



#### 12.4.3 프로세스 종료

- 프로세스(process): 운영체제가 실행 중인 프로그램을 관리하는 도구
- ```System.exit(int status)```
  - status = 0: 정상 종료
  - status = 1or -1: 비정상 종료

#### 12.4.4 진행 시간 읽기

- ```long currentTimeMillis()``` : $1/1000$ 초 단위로 진행된 시간을 리턴
- ```long nanoTime()``` : $1/10^9$ 초 단위로 진행된 시간을 리턴

#### 12.4.5 시스템 프로퍼티 읽기

- 시스템 프로퍼티(System Property): 자바 프로그램이 시작될 때 자동 설정되는 시스템의 속성
  - 속성 이름(key) : 값(value)
    - java.specification.version : 17 (자바 스펙 버전)
    - java.home : C:\Java\jdk (JDK 디렉토리 경로)
    - os.name : Windows 10 (운영체제)
    - user.name : jeusk (사용자 이름)
    - user.home : C:\Users\jeusk (사용자 홈 디렉토리 경로)
    - user.dir : C:\java\ThisIsJava_3E\thisisjava (현재 디렉토리 경로)

---

## 12.5 문자열 클래스

#### 12.5.1 String 클래스

- String 클래스: 문자열을 저장하고 조작할 때 사용

  ```java
  // 기본 문자셋으로 byte 배열을 디코딩해서 String 객체로 생성
  String str = new String(byte[] bytes);
  // 특정 문자셋으로 byte 배열을 디코딩해서 String 객체로 생성
  String str = new String(byte[] bytes, String charsetName);
  ```

  

#### 12.5.2 StringBuilder 클래스

- StringBuilder 클래스: 효율적인 문자열 조작 기능이 필요할 때 사용
  - StringBuilder append(기본값 | 문자열) : 문자열을 끝에 추가
  - StringBuilder insert(위치, 기본값 | 문자열) : 문자열을 지정 위치에 추가
  - StringBuilder delete(시작 위치, 끝 위치) : 문자열 일부를 삭제
  - StringBuilder replace(시작 위치, 끝 위치, 문자열) : 문자열 일부를 대체
  - String toString() : 완성된 문자열을 리턴


#### 12.5.3 StringTokenizer 클래스

- StringTokenizer 클래스: 구분자로 연결된 문자열을 분리할 때 사용
  - int countTokens() : 분리할 수 있는 문자열의 총 수
  - boolean hasMoreTokens() : 남아 있는 문자열이 있는지 여부
  - String nextToken() : 문자열을 하나씩 가져옴


---

## 12.6 포장 클래스

#### 12.6.1 박싱과 언박싱

- 박싱(boxing): 기본 타입의 값을 포장 객체로 만드는 과정
- 언박싱(unboxing): 포장 객체에서 기본 타입의 값을 얻어내는 과정

#### 12.6.2 문자열을 기본 타입 값으로 변환

- parse+기본타입

#### 12.6.3 포장 값 비교

- boolean, char, byte, short, int는 ==와 != 연산자로 객체 번지 비교 가능
  - char: \u0000 ~ \u007f
  - byte, short, int: -128 ~ 127
  - 위의 범위 포장 객체는 캐싱되어 새로운 객체를 생성하지 않고 동일한 참조를 갖는다.

---

## 12.7 수학 클래스

- Math 클래스가 제공하는 주요 메소드
  - abs(x) : x의 절대값
  - ceil(x) : x의 올림값
  - floor(x) : x의 버림값
  - max(x, y) : x, y의 최대값
  - min(x, y) : x, y의 최소값
  - random() : 0이상 1미만의 랜덤값
    - Random() 객체 : 현재 시간을 이용해서 종자값을 자동 설정한다.
    - Random(long seed) 객체 : 주어진 종자값을 사용한다.
      - boolean nextBoolean() : boolean 타입의 난수를 리턴
      - double nextDouble() : double 타입의 난수를 리턴(0.0이상 1.0미만)
      - int nextInt() : int 타입의 난수를 리턴($-2^{32}$이상 $2^{32}$미만)
      - int nextInt(int n) int 타입의 난수를 리턴(0이상 n미만)
  - round(x) : x의 반올림값

---

## 12.8 날짜와 시간 클래스

- Date 클래스: 날짜 정보를 전달하기 위해 사용
- Calendar 클래스: 다양한 시간대별로 날짜와 시간을 얻을 때 사용
- LocalDateTime 클래스: 날짜와 시간을 조작할 때 사용

#### 12.8.1 Date 클래스

- Date 클래스: 날짜를 표현하는 클래스로 객체 간에 날짜 정보를 주고받을 때 사용된다.
  - toString() 메소드: 날짜를 문자열로 얻는다.

#### 12.8.2 Calendar 클래스

- Calendar 클래스: 달력을 표현하는 추상 클래스
  - getInstance() 메소드: 컴퓨터에 설정되어 있는 시간대(TimeZone)를 기준으로 Calendar 하위 객체를 얻을 수 있다.
    - get() 메소드: Calendar가 제공하는 날짜와 시간에 대한 정보를 얻을 수 있다.
- TimeZone 클래스
  - getTimeZone(String) 메소드: String 지역ID 정보 리턴
  - getAvailableIDs() 메소드: 위 메소드와 같은 시간대 ID들 리턴

#### 12.8.3 날짜와 시간 조작

#### 12.8.4 날짜와 시간 비교

---

## 12.9 형식 클래스

#### 12.9.1 DecimalFormat

#### 12.9.2 SimpleDateFormat

---

## 12.10 정규 표현식 클래스

#### 12.10.1 정규 표현식 작성 방법

#### 12.10.2 Pattern 클래스로 검증

---

## 12.11 리플렉션

#### 12.11.1 패키지와 타입 정보 얻기

#### 12.11.2 멤버 정보 얻기

#### 12.11.3 리소스 경로 얻기

---

## 12.12 어노테이션

#### 12.12.1 어노테이션 타입 정의와 적용

#### 12.12.2 어노테이션 적용 대상

#### 12.12.3 어노테이션 유지 정책

#### 12.12.4 어노테이션 설정 정보 이용

---

