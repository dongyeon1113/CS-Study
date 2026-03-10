# 📈 Machine Learning: Regression & Optimization

이 저장소는 선형 회귀(Linear Regression)의 확장 모델인 **가산 선형 모델(Additive Linear Model)**과 이를 최적화하기 위한 **경사 하강법(Gradient Descent Method)**의 이론 및 구현 내용을 담고 있습니다.

---

## 1. Additive Linear Model (가산 선형 모델)

단순 선형 회귀를 넘어, 기저 함수(Basis Function)를 도입하여 비선형 데이터를 모델링합니다.

### 🔹 핵심 개념
- **모델 구조**: $f(x) = \sum_{j=0}^{M} w_j h_j(x)$
- **기저 함수 ($h_j(x)$)**: 데이터를 고차원 공간으로 매핑 (예: Polynomial, Gaussian, Sigmoid 등)
- **설계 행렬 (Design Matrix, $H$)**:
  $$H = \begin{pmatrix} h_0(x_1) & \cdots & h_M(x_1) \\ \vdots & \ddots & \vdots \\ h_0(x_n) & \cdots & h_M(x_n) \end{pmatrix}$$

### 🔹 정규 방정식 (Normal Equation)
오차 제곱합(SSE)을 최소화하는 최적의 가중치 $w$를 행렬 연산으로 한 번에 구합니다.
$$\mathbf{w} = (H^T H)^{-1} H^T \mathbf{t}$$

---

## 2. Gradient Descent Method (경사 하강법)

데이터가 너무 방대하여 행렬 역연산이 불가능하거나, 모델이 비선형적일 때 사용하는 최적화 알고리즘입니다.

### 🔹 학습 원리
오차 함수 $E(w)$의 기울기(Gradient)를 따라 가중치를 반복적으로 업데이트합니다.
$$w_{new} = w_{old} - \eta \frac{\partial E}{\partial w}$$
- **$\eta$ (Learning Rate)**: 한 번에 이동할 보폭을 결정합니다.

### 🔹 알고리즘 종류
1. **Batch Gradient Descent**: 전체 데이터를 사용하여 업데이트 (정확하지만 느림)
2. **Stochastic Gradient Descent (SGD)**: 데이터 한 개마다 업데이트 (빠르지만 불안정)
3. **Mini-batch Gradient Descent**: 데이터를 묶음(Batch) 단위로 나누어 업데이트 (실무에서 가장 많이 사용)

---

## 3. 요약 및 비교

| 특징 | Normal Equation (Closed-form) | Gradient Descent (Iterative) |
| :--- | :--- | :--- |
| **계산 방식** | 공식을 통해 한 번에 계산 | 반복적인 업데이트를 통해 수렴 |
| **데이터 크기** | 소규모 데이터에 적합 ($N < 10,000$) | 대규모 빅데이터에 필수적 |
| **특징** | 역행렬 계산 필요 ($O(n^3)$) | 하이퍼파라미터($\eta$) 설정 필요 |

---

## 💻 Implementation Example (Python)

```python
import numpy as np

# 1. Normal Equation 구현
def solve_normal_equation(H, t):
    return np.linalg.inv(H.T @ H) @ H.T @ t

# 2. Gradient Descent 구현 (Simple)
def gradient_descent(x, t, lr=0.01, epochs=1000):
    w = 0
    for _ in range(epochs):
        prediction = w * x
        error = prediction - t
        gradient = 2 * np.mean(error * x)
        w = w - lr * gradient
    return w
