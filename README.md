# VolCore-C
**High-Performance Option Pricing & Risk Engine (C++ / Python)**

VolCore-C is a **production-style quantitative risk and pricing engine** written in **C++** with **Python bindings** via `pybind11`.  
It implements **dual-number automatic differentiation** for exact Greeks computation on derivatives — a key building block for real trading and risk systems.

**Live demo notebook:**  
https://www.kaggle.com/code/gaurav11062002/volcore-c-high-performance-risk-engine

---

## Why VolCore Exists

In real trading and risk environments:

- Finite-difference Greeks are **slow, noisy, and unstable**
- Python autograd is **too slow for pricing loops**
- Production desks use **C++ pricing cores** with Python orchestration

VolCore mirrors how **sell-side and prop desks** build risk engines — fast, precise, and extensible.

---

##  Key Features

-  **Exact Greeks via Dual Numbers** – computes price and Delta analytically  
-  **High Performance** – compiled with `-O3` and low overhead  
-  **Python Bindings (pybind11)** – call from research pipelines  
-  **Mixed-Mode Arithmetic** – correct `double ↔ Dual` interactions  
-  **Quantitative Audit** – validated against finite differences  
-  **Risk Visualization** – Delta surface across strikes and maturities

---

##  Architecture Overview

```text
Python (Research / Analysis)
        │
        ▼
pybind11 Interface
        │
        ▼
C++ Pricing Core
  ├── Dual Number Engine (Automatic Differentiation)
  ├── Black-Scholes Pricing Model
  └── Exact Greeks Computation
```
---

##  Mathematical Core

### Dual Number Definition

```text
x = x_value + ε * x_derivative
```
Each variable carries its value and derivative, enabling exact **first-order differentiation** in a single evaluation pass.

---

###Greeks via Automatic Differentiation
Delta = ∂Price / ∂Spot


- Computed exactly, not via perturbations

- No numerical instability from step-size selection

## Current Model Support

- European Call Option

- Black-Scholes pricing

- Exact Delta via Automatic Differentiation

The architecture is extensible to **Gamma**, **Vega**, **multi-asset options**, and **stochastic volatility models**.
---
## Installation & Build

**Requirements**

- C++17 compatible compiler (g++ >= 9)

- Python 3.8+

- pybind11

##  Quantitative Audit (Validation)

The Delta computed via **Automatic Differentiation** is compared against **Finite Differences**:

| Method | Delta |
|------|-------|
| Automatic Differentiation | 0.5422283336 |
| Finite Difference | 0.5422283336 |
| Absolute Error | ~4e-11 |

This confirms **machine-precision accuracy**.

##  Visualization

Includes a **3D Delta Surface** visualization:

- **X-axis:** Strike  
- **Y-axis:** Time to Maturity  
- **Z-axis:** Delta  

This demonstrates how option sensitivity behaves across the surface — a **core risk insight** for derivatives trading.

### Delta Surface Plot

![Delta Surface Visualization](https://github.com/gaurav-kar-ji/VolCore-C-High-Performance-Risk-Engine/blob/main/plot.png)

