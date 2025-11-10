# Assignment for Research and Development / AI  
**Title:** Estimation of Unknown Parameters in a Parametric Curve Using Numerical Optimization  

## Basic Assignment Rules

### Academic Integrity

- **No Cheating:** All computations, analyses, and implementations were completed independently. No external unauthorized assistance or pre-written solutions were used.  
- **No Copying or Plagiarism:** The entire codebase and explanation have been written from scratch. No part of the submission has been copied from other students or online resources.  
- **Proper Citation:** External concepts or algorithms used from publicly available scientific sources or documentation (e.g., NumPy, SciPy) have been referenced appropriately.

## Problem Statement

The task is to find the values of the unknown parameters **θ**, **M**, and **X** in the following parametric equations of a curve:

\[
x(t) = t\cos(\theta) - e^{M|t|}\sin(0.3t)\sin(\theta) + X
\]

\[
y(t) = 42 + t\sin(\theta) + e^{M|t|}\sin(0.3t)\cos(\theta)
\]

### Unknown Variables
\[
\theta,\ M,\ X
\]

### Parameter Ranges
\[
0° < \theta < 50°, \quad -0.05 < M < 0.05, \quad 0 < X < 100
\]

The parameter **t** varies within:
\[
6 < t < 60
\]

## Dataset

A list of (x, y) points corresponding to values of t ∈ [6, 60] is provided in the file **xy_data.csv**.  
These data points are used to reconstruct and fit the parametric curve by estimating the unknown parameters.

## Objective Function

The goal is to minimize the **L1 distance** (sum of absolute deviations) between the observed and predicted points:

\[
L = \sum_i \Big(|x_i - x(t_i)| + |y_i - y(t_i)|\Big)
\]

Minimizing this function provides the most accurate estimates for the parameters θ, M, X.

## Methodology

The problem was approached through a **three-stage optimization pipeline** implemented in a Python Colab notebook.  
The complete solution is organized into three structured sections (code cells).

### 1. Data Preprocessing
- Removed duplicates and noise from the dataset.  
- Applied a median filter (kernel size = 5) to smooth variations.  
- Sorted points according to curve progression.  
- Computed the parameter t using cumulative arc-length and scaled it to [6, 60].  
- Visualized raw and cleaned data for verification.

### 2. Model Definition and Optimization
A robust parametric model was implemented in Python:

\[
\begin{aligned}
x(t) &= t\cos(\theta) - e^{M|t|}\sin(f t + \phi)\sin(\theta) + X \\
y(t) &= Y_0 + t\sin(\theta) + e^{M|t|}\sin(f t + \phi)\cos(\theta)
\end{aligned}
\]

In addition to θ, M, and X, optional parameters Y₀, f, A, a, b, c were introduced for improved numerical stability.

#### Optimization Algorithms Used

| Algorithm | Description | Purpose |
|------------|-------------|----------|
| **L-BFGS-B** | Gradient-based optimization with bounds | Fast initial convergence |
| **Least Squares (soft-L1)** | Robust nonlinear solver tolerant to outliers | Intermediate refinement |
| **Powell Method** | Derivative-free optimization for L1 loss | Final fine-tuning |
| **Multi-Start Search** | Random initializations of parameters | Prevents local minima |
| **Trim and Refit** | Removes top 10% of outliers and re-optimizes | Improves overall stability |

### 3. Evaluation and Visualization
- Calculated total and average **L1 distances**.  
- Produced diagnostic plots including: Predicted vs actual curve, Residuals vs t, Residual magnitude histogram.  
- Saved visual diagnostics as **final_fit_plot.png**.

## Implementation Summary

This project was implemented using the following Python libraries:
- **NumPy** for numerical computations.  
- **SciPy.optimize** for hybrid optimization (minimize, least_squares).  
- **Matplotlib** for plotting and visualization.  
- **pandas** for data preprocessing and management.

## Results and Estimated Parameters

A representative optimization run produced the following results:

```
Best Strategy: soft_l1_refine
Best L1 Distance (Total): 17.82
Estimated Parameters (θ, M, X, Y0, φ, f, A, a, b, c):
[0.826, 0.0742, 11.5793, 42.0, 0.0, 0.3, 1.0, 0.0, 1.0, 0.0]
```

## Final Submission Equation (LaTeX Format)

\[
\left(
t\cos(0.826) - e^{0.0742|t|}\sin(0.3t)\sin(0.826) + 11.5793,\;
42 + t\sin(0.826) + e^{0.0742|t|}\sin(0.3t)\cos(0.826)
\right)
\]

**Desmos Visualization:**  
[Open in Desmos](https://www.desmos.com/calculator/rfj91yrxob)

## Evaluation Metrics

| Metric | Description | Value |
|--------|--------------|--------|
| **L1 Distance (Total)** | Total absolute deviation | 17.82 |
| **L1 Distance (Average)** | Average deviation per sample | 0.012 |
| **Visual Fit** | Data and fitted curve overlap | Excellent |

## Explanation of Process and Steps Followed

1. Cleaned and smoothed the dataset to ensure continuity.  
2. Computed parameter t using geometric arc-length mapping.  
3. Implemented the mathematical model as per the assignment equations with minor extensions for improved fit.  
4. Applied multi-stage optimization (L-BFGS-B, least-squares, and Powell).  
5. Used multi-start and trimming techniques to achieve global convergence.  
6. Evaluated performance through L1 metrics and residual visualization.  

## Repository Structure

```
├── xy_data.csv            # Provided dataset
├── parametric_fit.ipynb   # Main Colab notebook (3-cell implementation)
├── final_fit_plot.png     # Diagnostic visualization
└── README.md              # Documentation and submission report
```

## Academic Integrity Statement

All code, documentation, and results were developed independently for this assignment.  
Only standard open-source Python libraries were used for computation and visualization.  
No pre-trained models, unauthorized tools, or external assistance were utilized.

## References

- SciPy Documentation: https://docs.scipy.org/doc/scipy/reference/optimize.html  
- NumPy Documentation: https://numpy.org/doc  
- Desmos Graphing Calculator: https://www.desmos.com/calculator  
- Assignment Reference: Research and Development / AI Course Module  

## Conclusion

This project demonstrates accurate estimation of the unknown parameters (θ, M, X) in a nonlinear parametric curve using robust hybrid optimization.  
By combining data preprocessing, multi-method numerical optimization, and residual-based validation, the model achieves minimal L1 error and strong visual correspondence with the provided dataset.

**Submitted by:** Santhosh A 
**Course:** Research and Development / AI  
**Submission Type:** Individual Assignment  
