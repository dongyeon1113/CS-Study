# Chapter 5. 병행 제어 (Concurrency Control) - II

## 1. Semaphore의 종류
- **Counting Semaphore**: 자원의 개수가 여러 개일 때 사용 (S가 0 이상인 정수).
- **Binary Semaphore (Mutex)**: 자원이 하나뿐일 때 사용 (S가 0 또는 1). 주로 **Mutual Exclusion(상호 배제)**을 위해 사용함.

---

## 2. 고전적인 동기화 문제들 (Classical Problems of Synchronization)

### (1) Bounded-Buffer Problem (Producer-Consumer Problem)
- **상황**: 크기가 유한한 버퍼를 공유하는 생산자(Producer)와 소비자(Consumer)가 있음.
- **문제점**:
    1. 공유 버퍼에 여러 명의 생산자/소비자가 동시에 접근 (Race Condition).
    2. 버퍼가 꽉 찼을 때 생산자가 데이터를 넣으려 하거나, 버퍼가 비었을 때 소비자가 꺼내려 함.
- **해결책 (세마포어 3개 사용)**:
    - **mutex**: 버퍼 자체에 대한 상호 배제 (Binary Semaphore).
    - **full**: 채워진 버퍼의 개수 (Counting Semaphore).
    - **empty**: 비어 있는 버퍼의 개수 (Counting Semaphore).

### (2) Readers-Writers Problem
- **상황**: 공유 데이터에 대해 읽기(Read) 작업을 하는 프로세스와 쓰기(Write) 작업을 하는 프로세스가 있음.
- **특징**:
    - Reader들은 여러 명이 동시에 읽어도 상관없음.
    - Writer가 쓰려고 할 때는 다른 누구도 접근해서는 안 됨.
- **해결책**:
    - Writer의 기아(Starvation) 현상이 발생할 수 있음 (Reader들이 끊임없이 들어오면 Writer는 영원히 대기). 이를 해결하기 위해 우선순위를 조절하는 복잡한 로직이 필요함.

### (3) Dining Philosophers Problem (식사하는 철학자 문제)
- **상황**: 5명의 철학자가 원탁에 앉아 생각과 식사를 반복함. 젓가락(공유 자원)은 철학자 사이에 1개씩 총 5개가 있음.
- **문제점**: 모든 철학자가 동시에 왼쪽 젓가락을 집으면, 아무도 오른쪽 젓가락을 집을 수 없어 **Deadlock(교착 상태)**에 빠짐.
- **해결책**:
    1. 4명의 철학자만 동시에 테이블에 앉게 함.
    2. 젓가락 두 개를 모두 집을 수 있을 때만 집게 함.
    3. 비대칭 전략 (홀수 번호는 왼쪽, 짝수 번호는 오른쪽부터 집게 함).

---

## 3. Monitor (모니터)
- **Semaphore의 문제점**: 
    - 코딩하기 어렵고 한 번의 실수가 시스템에 치명적임 (P와 V 연산의 순서 오류 등).
    - 예: `V(S)`를 먼저 하고 `P(S)`를 하면 상호 배제가 깨짐.
- **Monitor란?**: 
    - 프로그래밍 언어 차원에서 동기화를 제공하는 고수준 자료형.
    - 공유 데이터와 그 데이터를 다루는 프로시저(Procedure)를 한데 묶음.
    - **특징**: 모니터 내부의 프로시저는 한 번에 **하나의 프로세스만 실행** 가능 (자동으로 상호 배제 보장).
- **Condition Variable**: 
    - 자원을 기다리게 하기 위해 사용 (`wait()`, `signal()` 연산).
    - 세마포어처럼 값을 가지는 게 아니라, 프로세스를 재우고 깨우는 역할만 수행함.

---

## 4. Deadlock vs Starvation
- **Deadlock (교착 상태)**: 둘 이상의 프로세스가 서로 상대방이 가진 자원을 기다리며 무한히 대기하는 상태.
- **Starvation (기아 현상)**: 특정 프로세스가 자원을 할당받지 못하고 영원히 기다리는 상태 (우선순위 문제 등).

---
