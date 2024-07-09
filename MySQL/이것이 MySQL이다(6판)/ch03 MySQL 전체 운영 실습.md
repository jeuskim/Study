# Part 01 MySQL 설치 및 DB 구축과정 미리 실습하기

# Chapter 03 MySQL 전체 운영 실습

## 3.1 요구사항 분석과 시스템 설계 그리고 모델링

#### 3.1.1 정보시스템 구축 절차 요약

- 분석, 설계, 구현, 시험, 유지보수
  - 분석: 시스템 분석 또는 요구사항 분석이라고 부르며 무엇을(What) 할 것인지 결정한다.
  - 설계: 시스템 설계 또는 프로그램 설계라고 부르며 어떻게(How) 할 것인지 결정한다.

#### 3.1.2 데이터베이스 모델링과 필수 용어

- 데이터베이스 모델링: 현실세계에서 사용되는 데이터를 MySQL에 어떻게 옮겨 놓을 것인지를 결정하는 과정
  - 데이터: 정보는 있으나 아직 체계화 되지 못한 단편적인 정보
  - 테이블: 데이터를 입력하기 위해, 표 형태로 표현한 것
  - 데이터베이스(DB): 테이블이 저장되는 저장소(원통 모양)
  - DBMS(DataBase Management System): DB를 관리하는 시스템 또는 소프트웨어(예: MySQL)
  - 열(= 칼럼, = 필드): 각 테이블의 세로줄
  - 열 이름: 각 열을 구분하기 위한 이름(테이블 내에서 중복 불가)
  - 데이터 형식: 열의 데이터 형식
  - 행(= 로우, = 레코드): 각 테이블의 가로줄로 실질적인 데이터를 말한다.
  - 기본 키(Primary Key) 열: 각 행을 구분하는 유일한 열(중복 불가, 빈칸 불가)
  - 외래 키(Foreign Key) 필드: 두 테이블의 관계를 맺어주는 키
  - SQL(Structured Query Language): 사람과 DBMS가 소통하기 위한 언어

---

## 3.2 MySQL을 이용한 데이터베이스 구축 절차

- 쿼리 창: 쿼리(SQL)을 직접 입력하는 곳
- 쿼리 실행 버튼: 쿼리 창에 입력된 쿼리문을 실행한다.
- 쿼리 결과: 쿼리 창에 SQL을 입력하고 <쿼리 실행>을 클릭하면 결과 목록이 출력된다.
- 결과 메시지 창: 쿼리가 정상 실행되거나 오류가 발생한 경우 그 결과 메시지가 나온다.
- 데이터 개수: 쿼리의 수행 결과로 몇 건의 데이터가 조회되었는지 개수를 보여준다.
- 쿼리 수행 시간(초): SQL을 수행해서 결과가 나오기까지 소요된 시간(초)을 보여준다.
- 서버 관리 창: 서버의 상태, 데이터 가져오기/내보내기 등의 MySQL을 관리하기 위한 기능을 제공한다.
- 데이터베이스 목록 창: MySQL 내부에 존재하는 데이터베이스의 목록과 그 내부 테이블 등을 보여준다.

#### 3.2.1 데이터베이스 생성

- ```CREATE SCHEMA `DB Name` ;```

#### 3.2.2 테이블 생성

- ```CREATE TABLE `DB Name`.`Table Name` (`Column Name` Datatype, ..., PRIMARY KEY (`Column Name`)) ;```

#### 3.2.3 데이터 입력

- ```INSERT INTO `DB Name`.`Table Name` (`Column Name`, ...) VALUES (`Data Value`, ...) ;```

#### 3.2.4 데이터 활용

- ```SELECT ColumnName FROM TableName [WHERE Condition];```
- ```DROP TABLE `Table Name` ;```

---

## 3.3 테이블 외의 데이터베이스 개체의 활용

```mysql
CREATE TABLE indexTBL (first_name varchar(14), last_name varchar(16), hire_date date);
INSERT INTO indexTBL
	SELECT first_name, last_name, hire_date
	FROM employees.employees
	LIMIT 500;
SELECT * FROM indexTBL;

CREATE TABLE `shopdb`.`memberTBL` (
	`memberID` CHAR(8) NOT NULL,
    `memberName` CHAR(5) NOT NULL,
    `memberAddress` CHAR(20) NULL,
    PRIMARY KEY (`memberID`));

CREATE TABLE `shopdb`.`productTBL` (
	`productName` CHAR(4) NOT NULL,
	`cost` INT NOT NULL,
	`makeDate DATE,
    `company` CHAR(5),
	`amount` INT NOT NULL,
	PRIMARY KEY (`productName`));
```



#### 3.3.1 인덱스

- 인덱스(Index): 책의 제일 뒤에 붙어 있는 '찾아보기'(또는 색인)와 같은 개념이다.

- 데이터베이스 튜닝('Tuning'): 데이터베이스 성능을 향상시키거나 응답하는 시간을 단축시키는 것을 말한다.

  > 쿼리의 응답을 줄이기 위해서 가장 집중적으로 보는 부분 중 하나가 인덱스이다.

  ```mysql
  CREATE INDEX idx_indexTBL_firstname ON indexTBL(first_name);
  ```

  

#### 3.3.2 뷰

- 뷰(View): 테이블과 동일하게 보이지만, 실제 데이터를 가지고 있지 않은 가상 테이블(진짜 테이블에 링크된 개념)

  > 중요한 정보를 빼고 테이블을 다시 생성하지 않아도 그런 효과를 볼 수 있다.

  ```mysql
  CREATE VIEW uv_memberTBL
  AS
  	SELECT memberName, memberAddress FROM memberTBL ;
  ```

  

#### 3.3.3 스토어드 프로시저

- 스토어드 프로시저(Stored Procedure): MySQL에서 제공해주는 프로그래밍 기능을 말한다.(SQL문을 하나로 묶어서 편리하게 사용하는 기능)

  > DELIMITER는 '구분 문자'를 의미한다.(세미 콜론 대체)

  ```mysql
  DELIMITER //
  CREATE PROCEDURE myProc()
  BEGIN
  	SELECT * FROM memberTBL WHERE memberName = '당탕이' ;
  	SELECT * FROM productTBL WHERE productName = '냉장고' ;
  END //
  DELIMITER ;
  ```

  

#### 3.3.4 트리거

- 트리거(Trigger): 테이블에 부착되어서 테이블에 INSERT, UPDATE, DELETE 작업이 발생되면 실행되는 코드를 말한다.

  ```mysql
  CREATE TABLE deletedMemberTBL (
  	memberID CHAR(8),
      memberName CHAR(5),
      memberAddress CHAR(20),
      deletedDate DATE	-- 삭제한 날짜
  );
  
  DELIMITER //
  CREATE TRIGGER trg_deletedMemberTBL	-- 트리거 이름
  	AFTER DELETE	-- 삭제 후에 작동하게 지정
  	ON memberTBL	-- 트리거를 부착할 테이블
  	FOR EACH ROW	-- 각 행마다 적용시킴
  BEGIN
  	-- OLD 테이블의 내용을 백업 테이블에 삽입
  	INSERT INTO deletedMemberTBL
  		VALUES (OLD.memberID, OLD.memberName, OLD.memberAddress, CURDATE() );
  END //
  DELIMITER ;
  ```

  

---

## 3.4 데이터베이스 백업 및 관리

#### 3.4.1 백업과 복원

- 백업(Backup): 현재의 데이터베이스를 다른 매체에 보관하는 작업을 말한다.

- 복원: 데이터베이스에 문제가 발생했을 때 다른 매체에 백업된 데이터를 이용해서 원상태로 돌려놓는 작업을 말한다.

- DBA(DataBase Administrator = 데이터베이스 관리자): 백업, 복원을 담당한다.

  ```cmd
  mysqldump.exe --defaults-file="c:\users"
  ```

  

---

## 3.5 MySQL과 응용 프로그램의 연결

---

