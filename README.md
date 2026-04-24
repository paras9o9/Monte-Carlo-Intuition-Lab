# Monte Carlo Intuition Lab
**Statistics & Simulation**

## Overview

This lab builds probabilistic intuition through three tightly connected simulation experiments: the **Law of Large Numbers**, the **Central Limit Theorem**, and **Confidence Intervals**. All simulations are written in Python (NumPy + Matplotlib) and run in Google Colab. A bonus benchmark section connects the statistical machinery to a real-world ML/DS use case: comparing sorting algorithm runtimes.

---

## Objectives

- Understand the **Law of Large Numbers (LLN)** and observe how sample proportions converge to the true population mean as trial count grows.
- Understand the **Central Limit Theorem (CLT)** — why the distribution of sample means approaches a normal distribution regardless of the underlying population, and how variability decreases as sample size increases.
- Simulate **Confidence Intervals (CIs)** to build correct intuition about what a "95% CI" actually means (a statement about the *procedure*, not a specific interval).
- Apply CIs to **algorithm runtime benchmarking** (MergeSort vs QuickSort) to compare algorithms with statistical uncertainty rather than point estimates.

---

## Concepts Covered

### 1. Law of Large Numbers — Coin Flip Simulation

> *"As n → ∞, the probability that |Sₙ − μ| > ε goes to 0 for any small ε > 0."*

- Simulates `n = 50,000` coin flips using `numpy.random.default_rng(seed=42)`.
- Tracks the **cumulative proportion of heads** over flips.
- Plots convergence of the running proportion toward `p = 0.5` on a log-scaled x-axis.

**Key takeaway:** The sample mean stabilises around the true expected value as the number of trials increases, but fluctuates wildly at small sample sizes.

---

### 2. Central Limit Theorem (CLT)

> *"As n → ∞, the normalised sum of i.i.d. random variables approaches a standard normal distribution (μ = 0, σ = 1), regardless of the original population distribution."*

- Samples from different population shapes and plots the distribution of **sample means** for increasing sample sizes (`n = 5`, `n = 100`).
- Demonstrates:
  - Sample mean distribution becomes more bell-shaped as n grows.
  - Variance of sample means decreases with larger n.
  - Even small sample sizes (n = 5) already show approximate normality.

**Key takeaway:** ML/DS algorithms perform best with normally distributed data — the CLT tells us *when* we can rely on that assumption, even for non-normal populations.

---

### 3. Confidence Interval Simulation

> *"A 95% CI refers to the procedure, not to any one specific interval."*

- Simulates `n_experiments = 500` confidence intervals for a `N(0, 1)` population.
- Uses the **t-distribution** (`scipy.stats.t`) to compute CI bounds.
- Visualises the first 50 CIs, colour-coded green (captures true mean) or red (misses).
- Reports the **empirical coverage rate** (observed ≈ 0.934, target = 0.95).

**Common misinterpretation addressed:**
> Treating a CI as the probability that *this specific interval* contains the true value — it does not. It is a statement that if this process were repeated many times, ~95% of resulting intervals would contain the true value.

---

### 4. Bonus: CI for Sorting Algorithm Runtimes

Connects statistical CIs to practical algorithm comparison.

#### Algorithms Implemented
| Algorithm  | Strategy         | Implementation |
|------------|------------------|----------------|
| MergeSort  | Divide & Conquer | Recursive merge |
| QuickSort  | Divide & Conquer | Lomuto partition |

#### Experiment Setup
- **Array size:** `n = 10,000` (random integers in `[0, 10⁶]`)
- **Runs per algorithm:** `n_runs = 100`
- **Timing:** `timeit.Timer` (single pass per run)

#### Results

| Algorithm | Mean Runtime | 95% CI |
|-----------|-------------|--------|
| MergeSort | ~0.0370 s | [0.0336, 0.0404] s |
| QuickSort | ~0.0238 s | [0.0218, 0.0257] s |

**Key takeaway:**
- MergeSort has wider CI → higher runtime variability across runs.
- QuickSort has tighter CI → more consistent runtime.
- Using CIs instead of point estimates gives a richer comparison: we can assess both *speed* and *stability*.

---

## Reflections

- Regardless of original population shape, the CLT guarantees sample means approach normality.
- The CLT is why ML algorithms can assume normality in many settings, even with real-world skewed data.
- Confidence intervals are notoriously misinterpreted; this lab builds the correct frequentist intuition.
- In a real ML/DS pipeline, CI-based algorithm comparison is more rigorous than comparing single benchmark values.

---

## Dependencies

```
numpy
matplotlib
scipy
timeit (standard library)
```

---

## How to Run

1. Open `Monte_Carlo_Intuition_Lab_-Track_2_Statistics_-_Simulation.ipynb` in **Google Colab** or **Jupyter Notebook**.
2. Run all cells sequentially (Runtime → Run All).
3. All outputs, plots, and printed statistics will regenerate in order.

> **Seed:** `numpy.random.default_rng(seed=42)` — results are fully reproducible.

---

## File Structure

```
Monte_Carlo_Intuition_Lab_-Track_2_Statistics_-_Simulation.ipynb   ← main notebook
README.md                                                            ← this file
```

---

## Author

**Paras** — Statistics & Simulation  
Part of a structured curriculum in Machine Learning & Data Science.
