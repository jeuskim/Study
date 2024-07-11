# Part 02 MySQL 기본

# Chapter 06 SQL 기본

## 6.1 SELECT문

```mysql
-- MySQL 8.0 SELECT 구문 형식
SELECT
	[ALL | DISTINCT | DISTINCTROW]
		[HIGH_PRIORITY]
		[STRAIGHT_JOIN]
		[SQL_SMALL_RESULT] [SQL_BIG_RESULT] [SQL_BUFFER_RESULT]
		[SQL_NO_CACHE] [SQL_CALC_FOUND_ROWS]
	select_expr [, select_expr ...]
	[FROM table_references]
    	[PARTITION partition_list]
    [WHERE where_condition]
    [GROUP BY {col_name | expr | position}, ... [WITH ROLLUP]]
    [HAVING where_condition]
    [WINDOW window_name AS (window_spec)
    	[, window_name AS (window_spec)] ...]
    [ORDER BY {col_name | expr | position}
    	[ASC | DESC], ... [WITH ROLLUP]]
    [LIMIT {[offset,] row_count | row_count OFFSET offset}]
    [INTO OUTFILE 'file_name'
    	[CHARACTER SET charset_name]
    	export_options | INTO DUMPFILE 'file_name' | INTO var_name [, var_name]]
    [FOR {UPDATE | SHARE} [OF tbl_name [, tbl_name] ...] [NOWAIT | SKIP LOCKED] | LOCK IN SHARE MODE]]
```



#### 6.1.1 원하는 데이터를 가져와 주는 기본적인 <SELECT...FROM>

```mysql
SELECT select_expr
	[FROM table_references]
	[WHERE where_condition]
	[GROUP BY {col_name | expr | position}]
	[HAVING where_condition]
	[ORDER BY {col_name | expr | position}]
```

- USE 구문

  ```USE 데이터베이스_이름;``` : 현재 사용하는 데이터베이스를 지정

- SELECT와 FROM

  ```mysql
  SHOW DATABASES;	-- 현재 서버에 어떤 데이터베이스가 있는지 조회
  USE employees;	-- employees 데이터베이스 지정
  SHOW TABLE STATUS;	-- SHOW TABLES;	현재의 데이터베이스에 있는 테이블의 정보 조회
  DESC employees;	-- DESCRIBE employees;	employees 테이블의 열이 무엇이 있는지 조회
  SELECT first_name, gender FROM employees;	-- 최종적으로 데이터 조회
  -- SELECT first_name AS 이름, gender AS '성별' FROM employees;
  -- 별칭을 붙이면 열 이름을 별칭으로 보여준다.
  ```

- select_expr

  - DATE_FORMAT

    ```mysql
    SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d')
    		AS PUBLISHED_DATE
    	FROM BOOK
    	WHERE CATEGORY = '인문'
    		AND YEAR(PUBLISHED_DATE) = 2021
    	ORDER BY PUBLISHED_DATE;
    ```

  

- CREATE TABLE ... SELECT : 테이블 복사

  ```mysql
  CRATE TABLE 새로운테이블 (SELECT 복사할열 FROM 기존테이블)
  ```

  > PK나 FK 등의 제약조건은 복사되지 않는다.



#### 6.1.2 특정한 조건의 데이터만 조회하는 <SELECT...FROM...WHERE>

- DISTINCT : 중복된 것은 하나만 남김

  ```mysql
  -- [ALL | DISTINCT | DISTINCTROW]
  SELECT DISTINCT addr FROM usertbl;
  ```

  

- WHERE : 조회하는 결과에 특정한 조건을 줘서 원하는 데이터만 보고 싶을 때 사용

    ```mysql
    -- [WHERE where_condition]
    SELECT 필드이름 FROM 테이블이름 WHERE 조건식;
    ```
    
    - 조건식(where_condition)
    
        - 서브쿼리(SubQuery, 하위쿼리) : 쿼리문 안에 또 쿼리문이 들어 있는 것
        - 조건 연산자(=, <, >, <=, >=, <>, != 등)와 관계 연산자(NOT, AND, OR 등)의 사용
        - BETWEEN...AND... : 연속적인(Continuous) 값
        - IN(...) : 이산적인(Discrete) 값
        - LIKE... : 문자열의 내용 검색
        - % : 무엇이든 허용(여러 글자)
        - _ : 무엇이든 허용(한 글자)
        - ANY/ALL/SOME
        - ANY, SOME : 문자열의 OR
        - ALL : 문자열의 AND
    
        
    
- ORDER BY : 원하는 순서대로 정렬하여 출력(기본: 오름차순(ASC), 내림차순(DESC))

  ```mysql
  -- [ORDER BY {col_name | expr | position} [ASC | DESC], ... [WITH ROLLUP]]
  SELECT name, height	FROM usertbl ORDER BY name	ASC;	-- 오름차순
  SELECT name, mDate	FROM usertbl ORDER BY mDate	DESC;	-- 내림차순
  ```
  



- LIMIT : 출력하는 개수를 제한

  ```mysql
  -- [LIMIT {[offset,] row_count | row_count OFFSET offset}]
  LIMIT 5;	-- LIMIT 0, 5;		-- LIMIT 5 OFFSET 0;
  ```

  

#### 6.1.3 GROUP BY 및 HAVING 그리고 집계 함수

- GROUP BY : 같은 값들을 그룹으로 묶어주는 역할

  ```mysql
  SELECT userID, SUM(amount) FROM buytbl GROUP BY userID;
  ```

  - select_expr
    - 집계 함수(집합 함수)
      - AVG(...) : 평균을 구한다.
      - MIN(...) : 최소값을 구한다.
      - MAX(...) : 최대값을 구한다.
      - COUNT(...) : 행의 개수를 센다.
      - COUNT(DISTINCT ...) : 행의 개수를 센다(중복은 1개만 인정).
      - STDEV(...) : 표준편차를 구한다.
      - VAR_SAMP(...) : 분산을 구한다.



- HAVING : 집계 함수에 대해 특정한 조건을 줘서 원하는 데이터만 보고 싶을 때 사용

  ```mysql
  SELECT userID AS '사용자',
  		SUM(price * amount) AS '총구매액'
  	FROM buytbl
  	GROUP BY userID
  	HAING SUM(price * amount) > 1000;
  -- 만약 GROUP BY를 없이 HAVING을 쓰고 싶으면 select_expr이 집계 함수로만 이루어져 있어야 한다.
  ```

  - WITH ROLLUP : 총합 또는 중간 합계가 필요할 때 사용

    ```mysql
    SELECT num, groupName, SUM(price * amount) AS '비용'
    	FROM buytbl
    	GROUP BY groupName, num
    	WITH ROLLUP;
    ```

    

#### 6.1.4 SQL의 분류

- DML(Data Manipulation Language: 데이터 조작 언어)

  > 데이터를 조작(선택, 삽입, 수정, 삭제)하는 데 사용되는 언어

  - SELECT, INSERT, UPDATE, DELETE, 트랜잭션(Transaction)이 발생하는 SQL

- DDL(Data Definition Language: 데이터 정의 언어)

  > 데이터베이스, 테이블, 뷰, 인덱스 등의 데이터베이스 개체를 생성/삭제/변경하는 역할

  - CREATE, DROP, ALTER

    > 트랜잭션을 발생시키지 않아서 되돌리(ROLLBACK)이나 적용(COMMIT)을 시키지 못하고 실행 즉시 MySQL에 적용된다.

- DCL(Data Control Language: 데이터 제어 언어)

  > 사용자에게 어떤 권한을 부여하거나 빼앗을 때 주로 사용하는 구문

  - GRANT, REVOKE, DENY 등

---

## 6.2 데이터의 변경을 위한 SQL문

#### 6.2.1 데이터의 삽입 : INSERT

- INSERT : 테이블에 데이터를 삽입하는 명령어

  ```mysql
  INSERT [INTO] 테이블[(열1, 열2, ...)] VALUES (값1, 값2, ...)
  ```

  > 생략한 열에는 NULL 값이 들어간다.
  >
  > 여러 개의 행을 한꺼번에 입력할 때 (값1, 값2, ...), (값3, 값4, ...), ...; 이런식으로 입력할 수도 있다.

- 자동으로 증가하는 AUTO_INCREMENT

  - 테이블의 속성이 AUTO_INCREMENT로 지정되어 있을 때 : NULL 값을 지정하면 자동으로 값이 입력된다.

    > AUTO_INCREMENT는 PRIMARY KEY 또는 UNIQUE로 지정하고 숫자 형식의 데이터 형만 가능하다.

  - 가장 최근에 삽입된 AUTO_INCREMENT 필드의 값을 반환하는 함수

    ```mysql
    SELECT LAST_INSERT_ID();
    ```

  - AUTO_INCREMENT 입력값을 100부터 입력되도록 변경할 때

    ```MYSQL
    ALTER TABLE testTbl2 AUTO_INCREMENT = 100;
    ```

  - AUTO_INCREMENT 증가값을 1에서 3으로 변경

    ```mysql
    SET @@auto_increment_increment = 3;
    ```

- 대량의 샘플 데이터 생성

  ```mysql
  INSERT INTO 테이블이름 (열 이름1, 열 이름2, ...)
  	SELECT문;
  
  CREATE TABLE testTbl4 (
      id INT, Fname VARCHAR(50), Lname VARCHAR(50)
  );
  INSERT INTO testTbl4
  	SELECT emp_no, first_name, last_name
  		FROM employees.employees;
  
  CREATE TABLE testTbl5 (
  	SELECT emp_no, first_name, last_name
      	FROM employees.employees;
  );
  ```

  

#### 6.2.2 데이터의 수정 : UPDATE

- UPDATE : 기존에 입력되어 있는 값을 변경

  ```MYSQL
  UPDATE 테이블이름
  	SET 열1 = 값1, 열2 = 값2 ...
  	WHERE 조건 ;
  -- WHERE절이 생략되면 테이블 전체의 행이 변경
  ```

  

#### 6.2.3 데이터의 삭제 : DELETE FROM

- DELETE : 행 단위로 기존에 입력되어 있는 값을 삭제

  ```mysql
  DELETE FROM 테이블이름
  	WHERE 조건
  	LIMIT 개수;
  -- WHERE절이 생략되면 테이블 전체 데이터를 삭제
  ```

- DELETE, DROP, TRUNCATE

  ```mysql
  DELETE FROM bigTbl1;	-- 트랜잭션 로그를 기록하고 삭제
  DROP TABLE bigTbl2;		-- 테이블 자체를 삭제
  TRUNCATE TABLE bitTbl3;	-- 테이블의 구조를 남기고 내용을 삭제
  ```

  

#### 6.2.4 조건부 데이터 입력, 변경

- INSERT IGNORE : PK 중복이더라도 오류를 발생시키지 않고 무시하고 넘어간다.

- ON DUPLICATE KEY UPDATE : PK가 중복되지 않으면 일반 INSERT가 되고, PK가 중복이면 그 뒤의 UDPATE문이 수행된다.

  ```mysql
  INSERT IGNORE memberTBL VALUES('BBK', '비비코', '미국');
  INSERT INTO memberTBL VALUES('BBK', '비비코', '미국')
  	ON DUPLICATE KEY UPDATE name = '비비코', addr = '미국';
  ```

  

---

## 6.3 WITH절과 CTE

#### 6.3.1 WITH절과 CTE 개요

- WITH절 : CTE를 표현하기 위한 구문
  - CTE(Common Table Expression) : 기존의 뷰, 파생 테이블, 임시 테이블 등으로 사용되던 것을 대신한다.
    - 비재귀적(Non-Recursive) CTE
    - 재귀적(Recursive) CTE

#### 6.3.2 비재귀적 CTE

- 비재귀적 CTE

  ```mysql
  WITH CTE_테이블이름(열 이름)
  AS (
  	<쿼리문>
  )
  SELECT 열 이름 FROM CTE_테이블이름 ;
  ```

- 예

  ```mysql
  WITH abc(userid, total)
  AS
      (SELECT userid, SUM(price * amount)
          FROM buytbl
          GROUP BY userid )
  SELECT *
  	FROM abc
  	ORDER BY total DESC ;
  ```

- 중복 CTE

  ```mysql
  WITH AAA( 컬럼들 )
  AS ( AAA의 쿼리문 ),
  	BBB( 컬럼들 )
  		AS (BBB의 쿼리문),	-- AAA 참조 가능
  	CCC( 컬럼들)
  		AS (CCC의 쿼리문)	-- AAA, BBB 참조 가능
  SELECT *
  	FROM [AAA 또는 BBB 또는 CCC]
  ```

  

---