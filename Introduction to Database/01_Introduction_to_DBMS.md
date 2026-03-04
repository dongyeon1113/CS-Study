
## 01. Introduction to DBMS

### 1. 기본 개념
* **Database (DB)**: 서로 관련 있는 데이터들의 집합.
* **DBMS (Database Management System)**: 데이터베이스를 관리하고, 사용자가 데이터를 효율적으로 조회/수정할 수 있도록 돕는 소프트웨어 시스템.
* **Database System**: DB와 DBMS를 통칭하는 말.

### 2. 파일 시스템(File System) vs DBMS
과거에는 파일을 직접 관리했지만, 다음과 같은 문제점 때문에 DBMS를 사용합니다.
1. **데이터 중복 및 불일치 (Redundancy and Inconsistency)**: 동일 정보가 여러 파일에 중복 저장되어 데이터가 꼬일 수 있음.
2. **데이터 접근의 어려움 (Difficulty in Accessing Data)**: 새로운 요구사항이 생길 때마다 매번 새로운 프로그램을 짜야 함.
3. **데이터 고립 (Data Isolation)**: 데이터가 여러 파일과 형식으로 흩어져 있음.
4. **무결성 문제 (Integrity Problems)**: 데이터가 지켜야 할 규칙(예: 잔액은 0원 이상)을 강제하기 어려움.
5. **원자성 문제 (Atomicity)**: 작업 도중 시스템 장애 발생 시 데이터가 불완전한 상태로 남을 수 있음 (예: 송금 중 서버 다운).
6. **동시 접속 문제 (Concurrent Access)**: 여러 사용자가 동시에 데이터를 수정할 때 충돌 발생.
7. **보안 문제 (Security)**: 사용자별로 접근 권한을 세밀하게 제어하기 어려움.



### 3. 데이터 추상화 (Data Abstraction)
사용자에게 복잡한 물리적 저장 구조를 숨기기 위해 3단계로 나눕니다.
1. **Physical Level (물리적 단계)**: 데이터가 하드디스크 등에 '어떻게' 저장되는지 설명.
2. **Logical Level (논리적 단계)**: '어떤' 데이터가 저장되고, 데이터 간의 '관계'는 무엇인지 설명.
3. **View Level (뷰 단계)**: 각 사용자가 필요한 부분만 골라서 보여주는 단계.



### 4. 스키마와 인스턴스 (Schema & Instance)
* **Schema**: 데이터베이스의 전체적인 설계도 (논리적 구조). 자주 바뀌지 않음.
* **Instance**: 특정 시점의 데이터베이스에 저장된 실제 값. 수시로 바뀜.

### 5. 데이터 언어 (Data Languages)
* **DDL (Data Definition Language)**: 데이터베이스의 구조(틀)를 정의하거나 수정하는 언어.
* **DML (Data Manipulation Language)**: 데이터를 조회, 삽입, 삭제, 수정하는 언어 (SQL 등).

### 6. 트랜잭션 관리 (Transaction Management)
* **Transaction**: 하나의 논리적인 기능을 수행하는 작업 단위.
* **Storage Manager**: 데이터 저장 및 질의 실행을 담당.
* **Query Processor**: SQL 쿼리를 최적화하고 실행 계획을 수립.
