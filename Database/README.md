Database
=================================

</br>

## 데이터베이스

### 정의
* Integrated Data (통합된 데이터) : 자료의 중복 배제
* Stored Data (저장된 데이터)
* Operational Data (운영 데이터) : 조직 업무 수행에 있어서 반드시 필요한 자료
* Shared Data (공용 데이터)

### 특징
* **Real Tiem Accessibility (실시간 접근성)**  
    수시, 비정형적인 조회에 대해 실시간 처리에 의한 응답 가능
* **Continuous Evolution (계속적인 변화)**  
    새로운 데이터의 삽입, 삭제 갱신으로 항상 최신 데이터 유지
* **Concurrent Sharing (동시 공유)**  
    여러 사용자가 동시에 데이터 이용 가능
* **Content Reference (내용에 의한 참고)**  
    DB에 있는 데이터를 참조할 때 주소나 위치에 의해서가 아닌 데이터 내용, 즉 값으로 조회 가능

</br>

## DBMS

### DBMS의 정의
* DataBase Management System
* User와 DB사이에서 사용자의 요구에 따라 정보를 생성해주고, DB를 관리해주는 소프트웨어

### DBMS의 필수 기능
* **Definition (정의)**  
    데이터의 형과 구조, 데이터가 DB에 저장될 때의 제약조건 등을 명시하는 기능
* **Manipulation (조작)**  
    데이터 연산을 위한 사용자와 DB 사이의 접근 수단 (인터페이스) 제공
* **Control (제어)**  
    데이터 무결성 유지, 보안 유지, 권한 검사, 병행 제어

### DBMS의 장점
* **논리적 독립성**  
    개별 사용자나 응용 프로그램의 데이터 관점을 변경하지 않고 전체 데이터베이스의 논리적 구조를 변경시킬 수 있다.
* **물리적 독립성**  
    기존 응용프로그램에 영향을 주지 않고 데이터의 물리적 구조만을 변경시킬 수 있다.
    
</br>

## 데이터베이스 언어

### 데이터 정의 언어 (DDL : Data Definition Language)
* 데이터베이스, 테이블, 인덱스 생성 및 삭제
* 번역 결과가 데이터 사전이라는 파일에 여러개의 테이블로 저장
* 스키마, 도메인, 테이블, 뷰, 인덱스 정의, 변경, 삭제
* **DDL의 세가지 유형**  
    CREATE(정의), ALTER(변경), DROP(삭제)

### 데이터 조작 언어 (DML : Data Manipulation Language)
* 사용자와 DBMS 간의 인터페이스 제공
* **DML의 네가지 유형**  
    SELECT(튜플 검색), INSERT(튜플 삽입), UPDATE(튜플 갱신), DELETE(튜플 삭제)

### 데이터 제어 언어 (DCL : Data Control Language)
* 데이터의 보안, 무결성, 회복, 복구 및 병행 제어
* **DCL의 종류**  
    COMMIT(결과를 실제 물리적 디스트로 저장), ROLLBACK(비정상 종료시 복구), GRANT(권한 부여), REVOKE(권한 취소)
