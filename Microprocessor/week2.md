# 2주차 강의 요약

---

## 1. 강의 개요 (Course Outline)
프로세서의 작동 원리와 하드웨어 제어 기법을 폭넓게 다룹니다.
* Architecture: 레지스터, 주소 지정 방식, 명령어 세트 및 타이밍, 메모리 및 주변기기
* I/O & Memory: 입출력 아키텍처 및 메모리 인터페이스 (Serial/Parallel, DAC/ADC 등)
* Assembler: 어셈블리 명령어와 프로그래밍 기법
* Timings & Interrupts: 타이머 작동 원리 및 인터럽트 처리

---

## 2. 디지털 논리 회로: TTL vs CMOS

### TTL (Transistor-Transistor Logic)
* 전압 기준 ($V_{CC} = 5V$): 
  * `0` (Low): 0.4V 미만
  * `1` (High): 2.4V 초과
* 팬아웃 (Fan-out): 하나의 출력에 연결할 수 있는 입력 단자의 최대 개수. TTL은 전류 제한 때문에 보통 10개 미만으로 제한됩니다.

### CMOS (Complementary Metal-Oxide-Semiconductor)
TTL의 전력 소모 문제를 해결한 현대 프로세서의 핵심 논리 소자입니다.
* 특징: 평상시에는 전력을 거의 소모하지 않으며, 0에서 1로(또는 반대로) 논리 상태가 바뀌는 스위칭 순간에만 전류가 흐릅니다.
* 핵심 수식 3가지:
  1. 동적 전력 소모: $P_L = C_L \times V_{CC}^2 \times f_0$
     *(발열 및 전력 소모는 작동 주파수에 비례하고, 공급 전압의 제곱에 비례함)*
  2. 스위칭 전류: $I = C \frac{dV}{dt}$
  3. 정전 용량(커패시턴스): $C = \epsilon_1 \epsilon_0 \frac{A}{d}$ 
     *(트랜지스터 면적 A 를 줄이면 정전 용량 C가 줄어들어 속도가 빨라지고 전력 소모가 감소함)*

---

## 3. 논리 게이트와 메모리 소자

### 논리 게이트 (Logic Gates)


[Image of basic logic gates truth tables]

* NOT, AND, OR, NAND, NOR, XOR, XNOR 등의 게이트를 사용하여 부울 대수(Boolean Algebra) 연산을 수행합니다.
* 기능적 완전성 (Functional Completeness): NAND 게이트(또는 NOR 게이트) 하나만으로도 모든 논리 회로를 구현할 수 있습니다.

### 경합 조건 및 메모리 소자

* 경합 조건 (Race Condition): 논리 게이트 간의 신호 전달 속도 차이(전파 지연)로 인해 발생하는 의도치 않은 짧은 오류 신호(Spike).
* 메모리 소자: 이전 상태를 저장(기억)할 수 있는 회로. 
  * 래치(Latch) 및 플립플롭(Flip-flops): SR, D, T, JK 타입이 존재.

---

## 4. 아키텍처 비교



| 구분 | 폰 노이만 아키텍처 (Von Neumann) | 하버드 아키텍처 (Harvard) |
| :--- | :--- | :--- |
| 구조 | 프로그램과 데이터가 하나의 메모리를 공유 | 프로그램 메모리와 데이터 메모리가 물리적으로 분리 |
| 버스 | 데이터와 명령어가 동일한 버스를 사용 | 명령어 버스와 데이터 버스가 따로 존재 |
| 장점 | 하드웨어 구조가 단순하고 범용성이 높음 | 버스 병목현상이 없어 데이터 처리 속도가 빠름 |
| 단점 | 병목 현상(Bottleneck) 발생 가능 | 하드웨어 구성이 복잡하고 공간을 많이 차지함 |
| 적용 | 일반적인 PC (Intel, AMD CPU 등) | 마이크로컨트롤러 (Arduino, AVR, DSP 등) |

---

## 5. 데이터 표현 방식 (Data Representation)

### 정수 표현 (Integer)
* 음수 표현 방식: 부호-크기(Sign-magnitude), 1의 보수(1's complement), 2의 보수(2's complement, 현대 컴퓨터의 표준)
* 1 Byte(8 bits) 기준: 부호 없는 정수는 0~255, 부호 있는 정수는 -128~127 표현.

### 실수 표현 (IEEE-754 부동소수점 표준)



컴퓨터가 소수점이 있는 실수(Real Numbers)를 이진수로 처리하기 위한 국제 표준 방식입니다.

* Single Precision (단정밀도, 32-bit):
  * Sign (부호): 1 bit (0=양수, 1=음수)
  * Exponent (지수): 8 bits (바이어스 적용)
  * Mantissa / Significand (가수): 23 bits (실제 유효숫자 저장)
* Double Precision (배정밀도, 64-bit):
  * 부호(1 bit) + 지수(11 bits) + 가수(52 bits)
* 예외 처리 (Exceptions):
  * 0 (Zero): 모든 비트가 0으로 채워질 때
  * 무한대 (Infinity): 지수부의 모든 비트가 1이고, 가수부의 모든 비트가 0일 때
