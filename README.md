# Functional Regression with Splines: A Statistical Perspective

Post: https://www.linkedin.com/posts/brenogdsilva_datascience-regression-analytics-activity-7456043532978552832-0Ay5?utm_source=share&utm_medium=member_desktop&rcm=ACoAADzYEn0BidO853LZcLlVhNbNq-HOPuFNURk

## Introduction

In many real-world data science problems, the relationship between variables is inherently nonlinear. This is particularly evident in temporal processes such as demand modeling, where the response variable often exhibits multiple peaks, cycles, and regime changes throughout the day.

Classical linear regression assumes a fixed functional form:

$$
Y = \beta_0 + \beta_1 X + \varepsilon
$$

While interpretable, this assumption is often too restrictive. When the true relationship is nonlinear, linear models may fail to capture relevant structure, leading to biased predictions and poor generalization.

Spline-based methods provide a flexible alternative by allowing the data to determine the shape of the function. These approaches are widely studied in statistics (de Boor, 1978; Eilers & Marx, 1996; Hastie & Tibshirani, 1990; Wood, 2017) and are central to modern data science workflows.

This project explores different smoothing approaches applied to a simulated demand problem, comparing how each method captures nonlinear dynamics.

---

## Problem Formulation

Let:

$$
Y_i = f(x_i) + \varepsilon_i
$$

where:

- $Y_i$ is the observed response  
- $x_i$ is the predictor (hour of day)  
- $f(\cdot)$ is an unknown smooth function  
- $\varepsilon_i \sim N(0, \sigma^2)$  

The objective is to estimate $f(x)$.

---

## Data Generating Process

The true function is defined as:

$$ f(x) = 95 + \sum_{j=1}^{4} a_j \exp\left[-\left(\frac{x-\mu_j}{\sigma_j}\right)^2\right] + 6\sin\left(\frac{2\pi x}{24}\right) $$

This structure introduces:

- Multiple peaks: morning, midday and evening
- Local dips
- Cyclic behavior

---

## Methodology

### Linear Regression

$$
f(x) = \beta_0 + \beta_1 x
$$

Rigid and unable to capture nonlinear patterns.

---

### Cubic Spline

$$
f(x) = \beta_0 + \beta_1 x + \beta_2 x^2 + \beta_3 x^3 + \sum_{k=1}^{K} \gamma_k (x - \kappa_k)_+^3
$$

Piecewise cubic polynomial with knots.

---

### Natural Spline

Adds boundary constraints to stabilize behavior at extremes.

---

### B-Spline

$$
f(x) = \sum_{j=1}^{J} \beta_j B_j(x)
$$

Numerically stable representation using basis functions.

---

### P-Spline

$$
\min_{\beta} \left[
\sum (y_i - f(x_i))^2 +
\lambda \sum (\Delta^d \beta)^2
\right]
$$

Balances fit and smoothness.

---

### Cyclic Spline

For periodic data:

$$
f(0) = f(24)
$$

Ensures continuity in time cycles.

---

## Model Evaluation

Models are evaluated using:

$$
R^2 = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}
$$

---

## Results

The comparison shows:

- Linear regression underfits the data
- Splines capture nonlinear patterns effectively
- P-splines balance smoothness and flexibility
- Cyclic splines are best suited for periodic data

Key insight:

$$
\text{Model choice must reflect data structure}
$$

---

## Data Science Interpretation

This problem highlights a fundamental concept:

- Not all problems are linear
- Model flexibility is crucial
- Domain structure (e.g., periodicity) matters

Spline models act as a bridge between:

- classical statistics
- modern machine learning

---

## Conclusion

Spline-based regression provides a powerful framework for modeling nonlinear relationships.

Choosing the appropriate smoother depends on:

- data structure
- interpretability needs
- prediction goals

---

## References

- de Boor, C. (1978). *A Practical Guide to Splines*
- Eilers, P. H. C., & Marx, B. D. (1996). Flexible smoothing with B-splines
- Hastie, T., & Tibshirani, R. (1990). *Generalized Additive Models*
- Wood, S. N. (2017). *Generalized Additive Models: An Introduction with R*
