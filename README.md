# Vasicek Bond Pricing and Kalman Filtering: Multi-Method Fixed Income Modeling

## Overview

This repository offers a complete and professional pipeline for zero-coupon bond pricing and state-space modeling using the **Vasicek model**, enhanced with **Kalman filtering and smoothing** techniques for robust state and parameter estimation.

The project is organized into two integrated components:

1. **Bond Pricing Module** – Valuation of zero-coupon bonds via:
   - Analytical closed-form Vasicek solution
   - Monte Carlo simulation
   - Finite difference PDE discretization

2. **Kalman Filter Module** – Estimation of hidden Ornstein-Uhlenbeck states with noisy observations using:
   - Ordinary Least Squares (OLS) pre-estimation
   - Kalman Filtering and Smoothing
   - Maximum Likelihood Estimation (MLE)
   - Expectation-Maximization (EM)-like iterative parameter learning

---

## Table of Contents

- [Background](#background)
- [Mathematical Formulation](#mathematical-formulation)
- [Project Structure](#project-structure)
- [Methodologies](#methodologies)
  - [1. Bond Pricing](#1-bond-pricing)
  - [2. Kalman Filtering](#2-kalman-filtering)
- [Dependencies](#dependencies)
- [Usage](#usage)
- [Results](#results)
- [Visualizations](#visualizations)
- [Applications](#applications)
- [Author](#author)
- [License](#license)

---

## Background

The **Vasicek model** describes the dynamics of interest rates through a **mean-reverting stochastic differential equation**, making it foundational in fixed income analytics. In practice, observed data often include noise, requiring robust estimation frameworks such as the **Kalman filter**.

This project integrates simulation, pricing, and estimation techniques, forming a comprehensive framework applicable to both theoretical finance and real-world trading environments.

---

## Mathematical Formulation

### Vasicek Model Dynamics

$$ dr_t = \kappa(\theta - r_t)dt + \sigma dW_t $$

- $r_t$: Short rate
- $\kappa$: Speed of mean reversion
- $\theta$: Long-term mean level
- $\sigma$: Volatility

### Analytical Zero-Coupon Bond Price

$$ P(t, T) = A(t, T) e^{-B(t, T) r_t} $$

Where:

$$ B(t,T) = \frac{1 - e^{-\kappa (T - t)}}{\kappa} $$

$$ A(t,T) = \exp \left[ \left( \theta - \frac{\sigma^2}{2\kappa^2} \right)(B(t,T) - (T - t)) - \frac{\sigma^2}{4\kappa} B(t,T)^2 \right] $$

### Kalman Filter (State-Space Form)

- **State equation**:
  $$ x_t = \alpha + \beta x_{t-1} + \eta_t, \quad \eta_t \sim \mathcal{N}(0, \sigma_\eta^2) $$

- **Observation equation**:
  $$ y_t = x_t + \epsilon_t, \quad \epsilon_t \sim \mathcal{N}(0, \sigma_\epsilon^2) $$

---

## Project Structure

```bash
├── vasicek_bond_pricing.py        # Bond pricing via analytical, MC, PDE
├── kalman_filter_ou.py            # Kalman filtering, smoothing, EM
├── plots/                         # Output figures
├── requirements.txt               # Python packages
├── README.md                      # Documentation
```

---

## Methodologies

### 1. Bond Pricing Techniques

- **Closed-form Analytical**: Computes Vasicek zero-coupon bond price
- **Monte Carlo Simulation**: Simulates thousands of short-rate paths and computes expected discount factors
- **Finite Difference PDE**:
  - Solves Vasicek PDE using backward time-stepping
  - Implements implicit scheme with sparse tridiagonal solvers

### 2. Kalman Filtering & EM Estimation

- **OLS**: Initial regression-based parameter estimation
- **Kalman Filter**: Recursive estimation of hidden states
- **Kalman Smoother**: Uses future information for state refinement
- **MLE**: Maximizes likelihood over noisy measurements
- **EM-like Refinement**: Iterative updates until convergence

---

## Dependencies

- Python 3.8+
- numpy
- scipy
- matplotlib

Install:
```bash
pip install -r requirements.txt
```

---

## Usage

```bash
git clone https://github.com/Mkhan2317/Vasicek-Bond-Pricing.git
cd Vasicek-Bond-Pricing
python vasicek_bond_pricing.py
python kalman_filter_ou.py
```

---

## Results

### Bond Pricing Summary

| Method           | Price Estimate       | Notes                         |
|------------------|----------------------|-------------------------------|
| Analytical       | 0.0530               | Benchmark solution            |
| Monte Carlo      | 0.0535 ± 0.0006      | Stochastic validation         |
| PDE Finite Diff. | 0.0532               | Deterministic approximation   |

### Kalman Filtering Estimates

| Parameter                     | Estimate        | Ground Truth | Estimation Error |
|-------------------------------|------------------|---------------|------------------|
| $\theta$ (OLS)               | 0.507           | 0.5           | ~1.4%            |
| $\kappa$ (OLS)               | 2.566           | 3.0           | ~14.5%           |
| $\sigma$ (OLS)               | 0.497           | 0.5           | ~0.6%            |
| $\alpha$ (Kalman)            | 0.00044         | Derived       | —                |
| $\beta$ (Kalman)             | 0.9993          | ~1.0          | ~0.07%           |
| $\sigma_\eta^2$ (Process Noise) | $6.88 \times 10^{-5}$ | Small    | —                |
| $\sigma_\epsilon^2$ (Obs. Noise) | 0.00998      | 0.01          | ~0.2%            |

---

## Visualizations

- Vasicek bond price curve and 3D surface
- Ornstein-Uhlenbeck process with observation noise
- Kalman Filter and Smoother state estimates
- Uncertainty bands ($\pm$ 1 std dev) and residual errors

---

## Applications

- Fixed income derivatives pricing
- Yield curve construction
- Monetary policy modeling
- State-space inference in noisy systems
- Interest rate risk management

---

## Author

**MD Amir Khan**  
Master’s in Financial Engineering – Stevens Institute of Technology  
Specialization: Fixed Income Modeling, Quantitative Risk, Derivatives  
🔗 [LinkedIn](https://www.linkedin.com/in/amirkhan2317/)

---

## License

This project is licensed under the MIT License.  
See the `LICENSE` file for usage permissions.
