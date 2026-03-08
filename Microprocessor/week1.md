# Microprocessors (ICE3001) - Week 1 Summary

## 📌 Course Information
* **Professor**: Vitaly P. Panov 
* **Course Policy**: 
  * "NO MOBILE ZONE" - 수업 중 휴대폰 사용 금지.
  * 최소 출석 요건: 13/16 (미달 시 큰 페널티, 결석 당 -5점).
* **Grading**: Attendance 10%, Assignments 35%, Midterm 20%, Final 35%.

## 🗓️ Course Outline
* **Wk 1-2**: Introduction, Numerical systems.
* **Wk 3-5**: Microprocessors Architecture (registers, addressing, memory, hardware I/O).
* **Wk 6-7**: Input / Output Architecture.
* **Wk 8**: Memory Interfacing.
* **Wk 9-11**: Assembler (Assembly instructions).
* **Wk 12-14**: Input / Output interfacing (Serial/Parallel, DAC/ADC).
* **Wk 15-16**: Timings, timers, interrupts.

---

## 🖥️ Introduction to Microprocessors

### 1. Microprocessor vs Microcontroller
* **Microprocessor**: 컴퓨터의 CPU(Central Processing Unit) 기능을 모두 포함하는 집적 회로(IC). 컴퓨터 시스템의 심장 역할을 함.
* **Microcontroller (MCU)**: 단일 집적 회로 위에 CPU 코어, 메모리, 입출력(I/O)이 모두 포함된 소형 컴퓨터. 임베디드(Embedded) 애플리케이션에 주로 사용됨.

### 2. Classification of Basic Architectures
* **Von Neumann Architecture (폰 노이만 구조)**:
  * 프로그램과 데이터가 함께 저장되며 동일한 버스(Bus)를 통해 접근함.
  * 프로그램 접근과 데이터 접근이 충돌할 수 있어 '폰 노이만 병목현상(Bottleneck)'과 지연을 유발함.
* **Harvard Architecture (하버드 구조)**:
  * 프로그램과 데이터를 별도의 메모리에 분리하여 저장하고 개별 버스를 통해 접근함.
  * 데이터 충돌이 없어 시스템 성능이 향상되지만 더 많은 하드웨어가 요구됨.

---

## 🔢 Numerical Systems & Data Representation

### 1. Positional Notation (진법)
* **Binary (2진법)**: Base 2, Digits (0, 1).
* **Octal (8진법)**: Base 8, Digits (0~7).
* **Decimal (10진법)**: Base 10, Digits (0~9).
* **Hexadecimal (16진법)**: Base 16, Digits (0~9, A~F).

### 2. Information Codes
* **ASCII**: American Standard Code for Information Interchange (1961).
