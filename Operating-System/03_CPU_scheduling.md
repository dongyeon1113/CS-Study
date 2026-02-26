# Chapter 3. CPU 스케줄링 (CPU Scheduling)

## 1. CPU 스케줄링 개요
- **CPU Burst vs I/O Burst**: 프로세스는 CPU를 사용하는 단계(CPU Burst)와 I/O를 기다리는 단계(I/O Burst)를 반복하며 실행됨.
- **CPU-bound process**: CPU 연산이 주를 이루는 프로세스.
- **I/O-bound process**: I/O 요청이 빈번해 CPU를 짧게 자주 쓰는 프로세스.
- **목적**: CPU 이용률을 극대화하고, 응답성이 중요한 I/O-bound 프로세스(대화형 프로그램)가 CPU를 효율적으로 얻게 하기 위함.

### 1-1. CPU Scheduler & Dispatcher
- **CPU Scheduler**: Ready 상태의 프로세스 중에서 이번에 CPU를 줄 프로세스를 결정 (소프트웨어적 설계).
- **Dispatcher**: CPU Scheduler에 의해 선택된 프로세스에게 실제로 CPU 제어권을 넘김 (Context Switch 수행).
- **Non-preemptive (비선점형)**: 프로세스가 스스로 CPU를 반납할 때까지 빼앗지 않음.
- **Preemptive (선점형)**: OS가 강제로 CPU 제어권을 빼앗을 수 있음 (현대 OS의 방식).

---

## 2. 성능 척도 (Scheduling Criteria)

| 성능 척도 | 설명 | 비유 |
| :--- | :--- | :--- |
| **CPU Utilization** | 전체 시간 중 CPU가 일한 시간의 비율 (시스템 관점) | CPU가 얼마나 바쁘게 일했는가 |
| **Throughput** | 단위 시간당 완료한 프로세스의 개수 (시스템 관점) | 제한된 시간에 몇 명을 처리했는가 |
| **Response Time** | Ready Queue에 들어와서 **최초로 CPU를 얻기까지** 걸린 시간 | 식당에서 첫 음식이 나오기까지 시간 |
| **Waiting Time** | Ready Queue에서 CPU 할당을 기다리며 보낸 **시간의 총합** | 줄 서서 멍 때린 총 시간 |
| **Turnaround Time** | 프로세스가 시작되어 **완료될 때까지 걸린 전체 시간** (Wait + Run) | 식당 입장부터 다 먹고 나갈 때까지 시간 |



---

## 3. 스케줄링 알고리즘 (Scheduling Algorithms)

### (1) FCFS (First-Come, First-Served)
- **특징**: 먼저 온 순서대로 처리 (비선점형).
- **Convoy Effect**: 수행 시간이 긴 프로세스가 먼저 오면, 뒤의 짧은 프로세스들이 지나치게 오래 기다리는 현상.

### (2) SJF (Shortest-Job-First)
- **특징**: CPU burst가 가장 짧은 프로세스에게 먼저 할당.
- **SRTF (Shortest Remaining Time First)**: 선점형 SJF. 새로운 프로세스의 남은 시간이 더 짧으면 CPU를 빼앗음.
- **문제점**: 
    - **Starvation (기아 현상)**: 긴 프로세스가 영원히 CPU를 못 잡을 수 있음.
    - CPU 사용 시간을 미리 알 수 없어 과거 기록 기반의 예측(Exponential Averaging)이 필요함.

### (3) Priority Scheduling
- **특징**: 우선순위가 높은 프로세스에게 CPU 할당.
- **문제점**: Starvation 현상 발생 가능.
- **해결책 (Aging)**: 대기 시간이 길어지면 우선순위를 점진적으로 높여줌.

### (4) Round Robin (RR)
- **특징**: 현대적인 OS의 기반. 각 프로세스는 동일한 **Time Quantum(할당 시간)**을 가짐.
- **작동**: 할당 시간이 지나면 프로세스는 선점당하고 Ready Queue의 제일 뒤로 가서 줄을 섬.
- **장점**: 응답 시간(Response Time)이 매우 빠름.
- **주의**: 할당 시간이 너무 길면 FCFS와 같아지고, 너무 짧으면 Context Switch 오버헤드가 커짐.



### (5) Multilevel Queue
- **특징**: Ready Queue를 성격에 따라 여러 개로 분할.
    - 예: Foreground(RR 적용) / Background(FCFS 적용)
- **Multilevel Feedback Queue**: 프로세스가 큐 사이를 이동할 수 있게 하여 Aging 등을 구현하고 효율성을 극대화함.

---

## 4. 실시간 스케줄링 (Real-time Scheduling)
- **Hard Real-time**: 정해진 데드라인 내에 반드시 완료를 보장해야 함.
- **Soft Real-time**: 일반 프로세스보다 높은 우선순위를 가지지만, 데드라인 엄수를 100% 보장하지는 않음.

---

## 5. 스레드 스케줄링 (Thread Scheduling)
- **Local Scheduling**: User level thread의 경우 사용자 수준의 thread library에 의해 어떤 thread를 스케줄할지 결정
- **Global Scheduling**: Kernel level thread의 경우 일반 프로세스와 마찬 가지로 커널의 단기 스케줄러가 어떤 thread를 스케줄할지 결정
