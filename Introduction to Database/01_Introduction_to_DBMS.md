

## 01. Introduction to DBMS & Course Overview

### 1. 핵심 개념 (Core Concepts)
* **Database (DB)**: 서로 관련 있는 데이터들의 집합.
* **DBMS**: 데이터를 효율적으로 관리하고 사용자의 질의를 처리하는 소프트웨어.
* **Database System**: DB + DBMS.

### 2. 질의 처리 및 실행 계획 (Query Processing & Execution Plan) - *중요(Ch.13)*
교수님이 강조하신 DBMS의 내부 동작 원리입니다.
* **T-Structure (Tree)**: 실행 계획은 트리 구조로 표현됩니다.
  - **Bottom (Scan)**: 테이블 A, B를 디스크에서 읽어오는 스캔 작업.
  - **Intermediate**: 조인(Join), 필터(Filter), 프로젝션(Projection) 등의 연산 수행.
  - **Top**: 최종 결과를 사용자에게 반환.
* **Evaluation**: 생성된 실행 계획에 따라 각 연산자(Operator)를 실제로 실행하여 데이터를 추출합니다.



### 3. 트랜잭션 관리 (Transaction Management) - *핵심(Ch.14-16)*
계좌 이체 예시(A계좌에서 10원 차감 후 B계좌에 입금)를 통해 설명된 개념입니다.
* **Atomicity (원자성)**: "All or Nothing". 작업이 도중에 실패하면 아예 수행되지 않은 상태로 되돌려야 합니다.
* **Consistency**: 시스템 장애 후에도 데이터의 총합(잔액 등)은 일치해야 합니다.
* **Concurrency Control (동시성 제어)**: 여러 사용자가 동시에 접근할 때 발생하는 충돌을 관리합니다. (Lock, Timestamp 기법 등 사용)
  - *교수님 曰: "Chapter 15는 이 과목에서 가장 어려운 부분이니 많은 시간을 할애할 예정입니다."*



### 4. 사용자 분류 (Types of Users)
교수님의 목표는 우리를 **'DBA(전문가)'**로 만드는 것입니다.
1. **Naive Users**: 애플리케이션 기능을 그냥 사용하는 일반 사용자 (예: 할머니).
2. **Application Programmers**: SQL을 이용해 프로그램을 개발하는 개발자.
3. **Sophisticated Users (Data Analysts)**: 애플리케이션 없이 DBMS API나 SQL로 데이터를 분석하는 전문가.
4. **Database Administrators (DBA)**: 시스템 성능을 최적화하고 일관성 문제를 해결하는 **최고 전문가**.

### 5. 수업 운영 및 정책 (Course Policy)
* **Attendance**: 1/3 이상 결석 시 F. '대리 출석(Trutty)'은 엄격히 금지하며 적발 시 불이익이 큼.
* **Goal**: 단순히 사용법을 배우는 것이 아니라, DBMS의 **내부 구조(Internals)**를 깊게 이해하여 DBA 수준의 역량을 갖추는 것.
