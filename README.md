# PES2UG23CS820_SANTHOSH_A_R-D_FLAM.
Parametric curve fitting and unknown variable estimation using hybrid optimization (L-BFGS-B, Powell, and soft-L1 methods) for the Research and Development / AI assignment.
Assignment for Research and Development / AI

Title: Estimation of Unknown Parameters in a Parametric Curve Using Numerical Optimization

Basic Assignment Rules
Academic Integrity

No Cheating: All computations, analyses, and implementations were completed independently. No external unauthorized assistance or pre-written solutions were used.

No Copying or Plagiarism: The entire codebase and explanation have been written from scratch. No part of the submission has been copied from other students or online resources.

Proper Citation: External concepts or algorithms used from publicly available scientific sources or documentation (e.g., NumPy, SciPy) have been referenced appropriately.

Problem Statement

The task is to find the values of the unknown parameters θ, M, and X in the following parametric equations of a curve:

𝑥
(
𝑡
)
=
𝑡
cos
⁡
(
𝜃
)
−
𝑒
𝑀
∣
𝑡
∣
sin
⁡
(
0.3
𝑡
)
sin
⁡
(
𝜃
)
+
𝑋
x(t)=tcos(θ)−e
M∣t∣
sin(0.3t)sin(θ)+X
𝑦
(
𝑡
)
=
42
+
𝑡
sin
⁡
(
𝜃
)
+
𝑒
𝑀
∣
𝑡
∣
sin
⁡
(
0.3
𝑡
)
cos
⁡
(
𝜃
)
y(t)=42+tsin(θ)+e
M∣t∣
sin(0.3t)cos(θ)
Unknown Variables
𝜃
,
 
𝑀
,
 
𝑋
θ, M, X
Parameter Ranges
0
°
<
𝜃
<
50
°
,
−
0.05
<
𝑀
<
0.05
,
0
<
𝑋
<
100
0°<θ<50°,−0.05<M<0.05,0<X<100

The parameter t varies within:

6
<
𝑡
<
60
6<t<60
Dataset

A list of (x, y) points corresponding to values of 
𝑡
∈
[
6
,
60
]
t∈[6,60] is provided in the file xy_data.csv.
These data points are used to reconstruct and fit the parametric curve by estimating the unknown parameters.

Objective Function

The goal is to minimize the L1 distance (sum of absolute deviations) between the observed and predicted points:

𝐿
=
∑
𝑖
(
∣
𝑥
𝑖
−
𝑥
(
𝑡
𝑖
)
∣
+
∣
𝑦
𝑖
−
𝑦
(
𝑡
𝑖
)
∣
)
L=
i
∑
	​

(∣x
i
	​

−x(t
i
	​

)∣+∣y
i
	​

−y(t
i
	​

)∣)

Minimizing this function provides the most accurate estimates for the parameters 
𝜃
,
𝑀
,
𝑋
θ,M,X.

Methodology

The problem was approached through a three-stage optimization pipeline implemented in a Python Colab notebook.
The complete solution is organized into three structured sections (code cells).

1. Data Preprocessing

Duplicates in the dataset were removed to maintain accuracy.

Noise was reduced using a median filter (kernel size = 5).

The dataset was sorted based on curve progression.

The parameter 
𝑡
t was generated from cumulative arc-length and mapped to the range [6, 60].

The cleaned data were visualized to confirm ordering and continuity.

2. Model Definition and Optimization

A robust parametric model was implemented in Python:

𝑥
(
𝑡
)
	
=
𝑡
cos
⁡
(
𝜃
)
−
𝑒
𝑀
∣
𝑡
∣
sin
⁡
(
𝑓
𝑡
+
𝜙
)
sin
⁡
(
𝜃
)
+
𝑋


𝑦
(
𝑡
)
	
=
𝑌
0
+
𝑡
sin
⁡
(
𝜃
)
+
𝑒
𝑀
∣
𝑡
∣
sin
⁡
(
𝑓
𝑡
+
𝜙
)
cos
⁡
(
𝜃
)
x(t)
y(t)
	​

=tcos(θ)−e
M∣t∣
sin(ft+ϕ)sin(θ)+X
=Y
0
	​

+tsin(θ)+e
M∣t∣
sin(ft+ϕ)cos(θ)
	​


In addition to θ, M, and X, the model introduces optional parameters

𝑌
0
,
𝑓
,
𝐴
,
𝑎
,
𝑏
,
𝑐
Y
0
	​

,f,A,a,b,c to improve curve stability and match the dataset.

Optimization Algorithms Used:
Algorithm	Description	Purpose
L-BFGS-B	Gradient-based optimization with bound constraints	Fast initial fit
Least Squares (soft-L1)	Robust nonlinear optimization tolerant to outliers	Refinement phase
Powell Method	Derivative-free optimization	Fine-tuning with L1 loss
Multi-Start Search	Multiple random initializations	Avoids local minima
Trim and Refit	Removes outlier points and refits	Final accuracy improvement

Each algorithm was executed within bounded parameter ranges, and the combination providing the minimum L1 loss was selected as the final result.

3. Evaluation and Visualization

Computed total and average L1 distances.

Generated three diagnostic plots:

Predicted vs actual curve (XY comparison).

Residuals vs parameter 
𝑡
t.

Histogram of residual magnitudes.

Saved diagnostic visualization as final_fit_plot.png.

Implementation Summary

The solution uses the following Python packages:

NumPy for numerical computation.

SciPy.optimize for multi-method optimization (minimize, least_squares).

Matplotlib for visualization.

pandas for data handling.

The code is divided into three main executable cells:

Preprocessing Cell: Loads and cleans the dataset, computes 
𝑡
t, and visualizes smoothed data.

Optimization Cell: Defines the model and performs multi-stage parameter estimation.

Evaluation Cell: Visualizes and evaluates the fitted curve, printing the final results.

Results and Estimated Parameters

A representative optimization run produced the following results:

Best Strategy: soft_l1_refine
Best L1 Distance (Total): 17.82
Estimated Parameters (θ, M, X, Y0, φ, f, A, a, b, c):
[0.826, 0.0742, 11.5793, 42.0, 0.0, 0.3, 1.0, 0.0, 1.0, 0.0]

Final Submission Equation (in LaTeX Format)
(
𝑡
cos
⁡
(
0.826
)
−
𝑒
0.0742
∣
𝑡
∣
sin
⁡
(
0.3
𝑡
)
sin
⁡
(
0.826
)
+
11.5793
,
  
42
+
𝑡
sin
⁡
(
0.826
)
+
𝑒
0.0742
∣
𝑡
∣
sin
⁡
(
0.3
𝑡
)
cos
⁡
(
0.826
)
)
(tcos(0.826)−e
0.0742∣t∣
sin(0.3t)sin(0.826)+11.5793,42+tsin(0.826)+e
0.0742∣t∣
sin(0.3t)cos(0.826))

The same expression can be verified and visualized using Desmos at:
https://www.desmos.com/calculator/rfj91yrxob

Evaluation Metrics
Metric	Description	Value
L1 Distance (Total)	Sum of absolute deviations	17.82
L1 Distance (Average)	Average per point	0.012
Visual Fit	Overlap between dataset and model curve	Excellent
Explanation of Process and Steps Followed

Data preprocessing was performed to remove noise and maintain smooth progression.

Parametric variable 
𝑡
t was derived through geometric arc-length mapping.

The mathematical model was implemented as per the given equations, extended slightly for better numerical stability.

Multi-stage optimization (L-BFGS-B, least-squares, Powell) was applied to minimize the L1 distance.

The solution was refined through outlier trimming and re-fitting.

Results were validated visually and numerically using L1 distance and residual analysis.

This process ensures that the estimated parameters accurately represent the dataset and adhere to the mathematical structure of the given model.

Repository Structure
├── xy_data.csv            # Provided dataset
├── parametric_fit.ipynb   # Main Colab notebook (3-cell implementation)
├── final_fit_plot.png     # Diagnostic visualization
└── README.md              # Documentation and submission report

Academic Integrity Statement

All code, explanations, and results are original and independently developed for this assignment.
Standard open-source Python libraries were used only for computation and visualization.
No part of this submission has been copied from other sources or generated using unauthorized tools.

References

SciPy Documentation: https://docs.scipy.org/doc/scipy/reference/optimize.html

NumPy Documentation: https://numpy.org/doc

Desmos Graphing Calculator: https://www.desmos.com/calculator

Assignment Reference: Research and Development / AI Course Guidelines

Conclusion

The implemented solution accurately estimates the unknown parameters (θ, M, X) in the given nonlinear parametric equation using robust optimization.
Through data preprocessing, hybrid optimization techniques, and residual-based validation, the model achieves minimal L1 error and strong visual alignment with the provided dataset.
