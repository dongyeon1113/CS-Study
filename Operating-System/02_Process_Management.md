# Chapter 2. 프로세스 관리 (Process Management)

## 1. 프로세스의 개념과 주소 공간
### 프로세스의 정의
- **정의**: 실행 중인 프로그램 (Program in execution)
- **Virtual Memory**: 각 실행 파일이 메모리에 올라갈 때 갖는 독자적인 주소 공간 (Address Space).
- **Address Translation**: 가상 메모리 주소를 실제 물리적 메모리(Physical memory) 주소로 변환하는 과정.

### 커널(Kernel) 주소 공간의 내용
- **Code**: 시스템 콜, 인터럽트 처리 코드, 자원 관리 코드 등.
- **Data**: CPU, Memory, Disk 등 하드웨어 관리 자료구조 및 모든 프로세스를 관리하기 위한 **PCB(Process Control Block)** 위치.
- **Stack**: 각 프로세스의 커널 스택 (커널 함수 호출 시 사용).

### 사용자 프로그램이 사용하는 함수의 구분
1. **사용자 정의 함수**: 내 프로그램 주소 공간의 Code 영역에 위치.
2. **라이브러리 함수**: 내 프로그램 주소 공간의 Code 영역에 위치 (컴파일 시 포함).
3. **커널 함수**: 운영체제 커널 주소 공간의 Code 영역에 위치 (System Call을 통해 호출).

---

## 2. 프로세스의 문맥 (Process Context)
프로세스가 현재 어떤 상태에 있는지 나타내는 모든 정보입니다.
1. **하드웨어 문맥**: CPU 수행 상태 (Program Counter, Registers).
2. **주소 공간 (Address Space)**: 가상 메모리의 Code, Data, Stack 상태.
3. **커널 상의 문맥**: 운영체제가 관리하는 PCB 및 해당 프로세스의 Kernel Stack.

---

## 3. 프로세스의 상태 (Process State)
- **Running**: CPU를 점유하여 명령을 수행 중인 상태.
- **Ready**: CPU 할당을 기다리는 상태 (메모리 등 다른 조건은 모두 만족).
- **Blocked (Wait, Sleep)**: I/O 등 특정 이벤트를 기다리는 상태. CPU를 주어도 당장 실행 불가능.
- **New / Terminated**: 프로세스 생성 중 또는 수행 종료 후 정리 중인 상태.
- **Suspended (Stopped)**: 외부적인 이유(메모리 부족 등)로 수행이 정지되어 프로세스 전체가 디스크로 쫓겨난(Swap out) 상태.

---

## 4. PCB (Process Control Block)
운영체제가 각 프로세스를 관리하기 위해 커널 주소 공간(Data 영역)에 유지하는 정보입니다.
1. **OS 관리 정보**: Process ID, 우선순위, 프로세스 상태.
2. **CPU 수행 정보**: Program Counter, Registers (Context Switch를 위함).
3. **메모리 정보**: Code, Data, Stack의 위치 정보.
4. **리소스 정보**: Open file descriptors 등 사용 중인 자원 정보.

---

## 5. 문맥 교환 (Context Switch)
### 정의
CPU를 한 프로세스에서 다른 프로세스로 넘겨주는 과정입니다. (Time interrupt 발생 또는 I/O 요청 등)

### 절차
1. CPU를 반납하는 프로세스의 상태를 해당 PCB에 저장.
2. 새롭게 CPU를 얻는 프로세스의 상태를 PCB에서 읽어와 하드웨어 레지스터에 복구.

### 주의사항
System Call이나 Interrupt 발생 시 항상 문맥 교환이 일어나는 것은 아닙니다. 동일 프로세스 내에서 **사용자 모드 → 커널 모드**로 전환되는 경우는 문맥 교환이 아니며, CPU 제어권이 다른 프로세스로 넘어갈 때만 문맥 교환이라 합니다.



---

## 6. 스케줄링을 위한 큐 (Queue)
- **Job Queue**: 시스템 내의 모든 프로세스 집합.
- **Ready Queue**: 메모리에 있으면서 CPU 할당을 기다리는 프로세스 집합.
- **Device Queue**: 특정 I/O 장치의 처리를 기다리는 프로세스 집합.

---

## 7. 스케줄러 (Scheduler)
- **장기 스케줄러 (Job Scheduler)**: 어떤 프로세스를 메모리에 올릴지 결정 (Degree of Multiprogramming 제어). 현대 OS에서는 보통 생략(바로 Ready 상태로 진입).
- **단기 스케줄러 (CPU Scheduler)**: Ready Queue의 프로세스 중 누구에게 CPU를 줄지 결정.
- **중기 스케줄러 (Swapper)**: 메모리에 너무 많은 프로그램이 있을 때, 통째로 디스크로 쫓아내어 메모리 공간을 확보.
