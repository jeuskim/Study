# Part 02 MySQL 기본

# Chapter 05 MySQL 유틸리티 사용법

## 5.1 MySQL Workbench 사용 방법

- Workbench의 주요 기능
  - 데이터베이스 연결 기능
  - 인스턴스 관리
  - 위저드를 이용한 MySQL의 동작
  - 통합된 기능의 SQL 편집기
  - 데이터베이스 모델링 기능
  - 포워드/리버스 엔지니어링 기능
  - 데이터베이스 인스턴스 시작/종료
  - 데이터베이스 내보내기/가져오기
  - 데이터베이스 계정 관리

#### 5.1.1 MySQL Workbench의 버전과 실행

#### 5.1.2 [MySQL Connections] 창

- 접속될 서버, 사용자, 포트를 선택 후 접속 시도

- [Connection] 탭

  - Connection Method: Standard (TCP/IP), Local Socket/Pipe, Standard TCP/IP over SSH 등등

  - [Parameters] 탭

    - Hostname: 접속할 서버 컴퓨터의 IP 주소(자신의 컴퓨터일 때 127.0.0.1 또는 localhost)
    - Port: 3306
    - Username: 접속할 MySQL 사용자
    - root: MySQL 관리자의 이름
    - Password
    - <Store in Vault ...>: 사용자의 비밀번호 저장
    - \<Clear\>: 저장해 둔 비밀번호 삭제
    - Default Schema: 접속 후에 기본적으로 선택되는 데이터베이스 이름

  - [SSL] 탭

    > SSL(Secure Socket Layer): 보안을 위한 암호 규약

  - [Advanced] 탭

    > 프로토콜의 압축, 인증 방식 등을 설정

- [Remote Management] 탭

  > 원격 관리를 설정하는 부분

  - 'Native Windows remove Management': Window인 경우에만 설정 가능
  - 'SSH login based management': SSH 서버 기반으로 원격 접속

- [System Profile] 탭

  > 접속할 서버의 OS 종류 및 MySQL 설정 파일의 경로 등을 설정(Remote Management의 원격 관리 설정 변경 필요)

  - [System Type] 탭: FreeBSD, Linux, MacOS X, OpenSolaris, Windows
  - [Installation Type] 탭
  - [Configuration Type] 탭: MySQL의 설정 파일이 경로에 함께 지정
  - [Configuration File Section] 탭: 서버의 서비스 이름 지정
  - [MySQL Management] 탭: MySQL 서비스를 시작하거나 중지하는 시스템 명령어를 적어준다.

#### 5.1.3 MySQL Workbench의 화면 구성

- 내비게이터(Navigator): MySQL의 관리 및 운영을 위한 강력한 도구
  - [Schemas] 탭
    - 데이터베이스(=스키마) 생성 및 삭제
    - 데이터베이스 개체(테이블, 뷰, 인덱스, 저장 프로시저, 함수 등)를 생성하고 관리
    - 데이터베이스의 속성을 조회
  - [Administration] 탭
    - MANAGEMENT
      - [Server Status] 탭: MySQL  서버의 가동 상태, 포트, 환경 파일의 경로, 메모리 상태, CPU 사용 상태 등 확인
      - [Client Connections] 탭: MySQL 서버에 연결되어 있는 클라이언트의 정보를 확인
      - [User and Privileges] 탭: 사용자의 생성, 삭제 및 권한 관리
      - [Status and System Variables] 탭: 서버 변숫값의 확인
      - [Data Export], [Data Import/Restore] 탭: 데이터 내보내기/가져오기 기능
    - INSTANCE
      - [Startup / Shutdown] 탭: MySQL 연결 정보 관리, MySQL 인스턴스의 중지, 시작
      - [Server Logs] 탭: Server에 기록된 로그 조회
      - [Options File] 탭: MySQL 옵션 파일의 설정 정보 확인 및 변경(my.ini 파일의 내용을 GUI 모드로 보여준다.)
    - PERFORMANCE
      - [Dashboard] 탭: 네트워크 상태 및 MySQL 서버, InnoDB의 성능 상태를 확인
      - [Performance Reports] 탭: 항목들을 조회하고 결과 내보내기(성능 상태의 보고서 작성)
      - [Performance Schema Setup] 탭: 성능 구성의 설정

---

## 5.2 외부 MySQL 서버 관리

- MySQL의 초기화면에서 Hostname에 IP주소를 적어서 외부 서버에 접근할 수 있다.
  - Linux 관리자의 아이디는 root고 비밀번호는 password다.
  - MySQL에 접속하려면 ```mysql -u root -p``` 명령을 사용한다.
  - MySQL 관리자의 아이디는 root고 비밀번호는 1234다.
  - IP 주소를 확인하려면 ```ip addr``` 명령을 사용한다.
  - Linux를 종료하려면 ```shutdown -h now``` 명령을 사용한다.

---

## 5.3 사용자 관리

- [Navigator]의 Administration]의 [User and Privileges]에서 사용자 생성 및 권한 부여를 할 수 있다.

---

