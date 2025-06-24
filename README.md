# Vasicek Bond Pricing and Kalman Filtering: Multi-Method Fixed Income Modeling

## Overview

This repository provides a complete and professional implementation of zero-coupon bond pricing and interest rate modeling using the **Vasicek model**, enhanced with **Kalman filtering and smoothing** techniques for state and parameter estimation.

The project comprises two core modules:

1. **Vasicek Bond Pricing** – Zero-coupon bond valuation using:
   - Analytical closed-form formula
   - Monte Carlo simulations
   - Partial Differential Equation (PDE) finite difference method

2. **Kalman Filtering for Ornstein-Uhlenbeck Process** – Recursive estimation of hidden states and parameters in the Vasicek (OU) model with noisy measurements, using:
   - Ordinary Least Squares (OLS)
   - Kalman Filter (KF)
   - Kalman Smoother (KS)
   - Maximum Likelihood Estimation (MLE)
   - Expectation-Maximization (EM)-like parameter refinement

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

The **Vasicek model** describes the stochastic evolution of interest rates using a **mean-reverting Ornstein-Uhlenbeck process**. It is widely used in bond pricing, asset liability management, and interest rate derivative modeling.

The project extends this model by estimating latent states and parameters using noisy data, mimicking real-world market imperfections.

---

## Mathematical Formulation

### Vasicek Short Rate Model:
\[ dr_t = \kappa(\theta - r_t)dt + \sigma dW_t \]

Where:
- \( r_t \): Short rate
- \( \kappa \): Mean reversion speed
- \( \theta \): Long-term mean
- \( \sigma \): Volatility

### Zero-Coupon Bond Price:
\[ P(t, T) = A(t, T) \cdot e^{-B(t, T) r_t} \]
With:
- \( B(t,T) = \frac{1 - e^{-\kappa (T - t)}}{\kappa} \)
- \( A(t,T) = \exp \left[ \left( \theta - \frac{\sigma^2}{2\kappa^2} \right)(B(t,T) - (T - t)) - \frac{\sigma^2}{4\kappa} B(t,T)^2 \right] \)

### Kalman Filter Recursive Equations:
Estimates latent states and model parameters from noisy measurements.

---

## Project Structure

```bash
├── vasicek_bond_pricing.py        # Analytical, Monte Carlo, PDE bond pricing
├── kalman_filter_ou.py            # OLS, Kalman filter & smoother, MLE estimation
├── plots/                         # Output visualizations
├── requirements.txt               # Python dependencies
├── README.md                      # Project documentation
```

---

## Methodologies

### 1. Bond Pricing

- **Analytical Formula**: Closed-form solution using Vasicek assumptions
- **Monte Carlo Simulation**:
  - Simulates thousands of short-rate paths
  - Computes expected discount factors
- **Finite Difference PDE**:
  - Solves the Vasicek PDE using implicit method
  - Employs sparse tridiagonal matrices for efficiency

### 2. Kalman Filtering

- **OLS Estimation**: Initial parameter guesses using linear regression
- **Kalman Filter**: Recursive estimation of latent states
- **Kalman Smoother**: Backward pass using future information for refinement
- **MLE Optimization**: Parameter tuning via log-likelihood maximization
- **Iterative Refinement**: EM-like convergence to optimal parameter values

---

## Dependencies

- Python 3.8+
- numpy
- scipy
- matplotlib

Install dependencies using:
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

### Bond Pricing:
| Method           | Estimated Bond Price | Notes                         |
| ---------------- | -------------------- | ----------------------------- |
| Analytical       | 0.0530               | Benchmark                    |
| Monte Carlo      | 0.0535 ± 0.0006      | High accuracy                 |
| PDE              | 0.0532               | Converges with MC            |

### Kalman Filter Estimates:
| Parameter                 | Estimated (KF)         | True Value  | Error       |
|--------------------------|------------------------|-------------|-------------|
| \( \theta \) (OLS)        | 0.507                  | 0.5         | ~1.4%       |
| \( \kappa \) (OLS)        | 2.566                  | 3.0         | ~14.5%      |
| \( \sigma \) (OLS)        | 0.497                  | 0.5         | ~0.6%       |
| \( \alpha \) (Kalman)     | 0.00044                | derived     | —           |
| \( \beta \) (Kalman)      | 0.9993                 | ~1          | ~0.07%      |
| Process Noise \( \eta \)  | \( 6.88 \times 10^{-5} \) | small       | —           |
| Measurement Noise \( \epsilon \) | 0.00998        | 0.01        | ~0.2%       |

---

## Visualizations

- Interest Rate vs. Bond Price Curve
- 3D Surface of Bond Price over Rate & Time
- OU Process with Measurement Noise
- Kalman Filter and Smoother Estimates with Confidence Bands

---

## Applications

- Interest rate derivatives pricing
- Central bank short rate modeling
- Term structure construction
- Noisy signal denoising
- Time-series state estimation

---

## Author

**MD Amir Khan**  
Master’s in Financial Engineering – Stevens Institute of Technology  
Focus: Fixed Income Analytics, Derivatives, Quantitative Risk Modeling  
📎 [LinkedIn Profile](https://www.linkedin.com/in/amirkhan2317/)

---

## License

This project is licensed under the MIT License.
See the `LICENSE` file for more details.
