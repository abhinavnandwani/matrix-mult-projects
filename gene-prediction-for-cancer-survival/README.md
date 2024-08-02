# Data Fitting vs. Sparsity Tradeoff

This assignment explores sparse regularization in a least squares problem using the `BreastCancer.mat` dataset. The dataset contains gene expression levels from 295 patients, with 8141 genes as features. The goal is to analyze the tradeoff between data-fitting and sparsity in the context of Lasso regression.

## Background

The journal article *[A Gene-Expression Signature as a Predictor of Survival in Breast Cancer](https://www.nejm.org/doi/full/10.1056/NEJMoa021967)* (NEJM, 2002) provides significant insights into how gene expression profiles can predict patient outcomes in breast cancer. The study presents a gene-expression signature that correlates with survival rates, emphasizing the importance of specific genes in prognosis.

### Key Components of the Article:
- **Objective:** To identify a set of genes whose expression levels predict survival in breast cancer patients.
- **Methods:** Utilizes microarray technology to analyze gene expression profiles and employs statistical models to identify predictive gene signatures.
- **Findings:** Identifies a 70-gene signature associated with patient survival, demonstrating the potential of gene-expression profiles in prognostic assessments.
- **Relevance:** The study highlights the role of gene selection in improving predictive models, which is directly applicable to the Lasso regression problem we are addressing.

## Problem Statement

We seek to solve the Lasso problem:

$$
\mathbf{w}^* = \arg \min_{\mathbf{w} \in \mathbb{R}^n} \|A\mathbf{w} - \mathbf{d}\|_2^2 + \lambda \|\mathbf{w}\|_1
$$

where \(\mathbf{w}\) represents the weight vector for the gene expression levels. The regularization parameter \(\lambda\) controls the tradeoff between fitting the data well and achieving sparsity in the weight vector.

## Methodology

Scripts are provided to implement the iterative soft-thresholding algorithm using proximal gradient descent to solve the Lasso problem. The algorithm is designed to handle varying values of \(\lambda\) efficiently through a hot start procedure. This approach uses the converged solution from one \(\lambda\) value as the initial guess for the next, accelerating convergence when subsequent \(\lambda\) values lead to similar solutions.

# Iterative Soft-Thresholding for Lasso Regression

## Overview

The code implements the Iterative Soft-Thresholding Algorithm (ISTA) to solve Lasso regression problems for multiple values of the regularization parameter \(\lambda\). This approach uses a hot start for faster convergence.

## `ista_solve_hot` Function

### Description

The `ista_solve_hot` function solves the Lasso regression problem:

$$
\text{Minimize} \; ||Ax - d||_2^2 + \lambda \; ||x||_1
$$

where:
- \(A\) is the design matrix.
- \(d\) is the response vector.
- \(\lambda\) is the regularization parameter.

### Key Components

- **Initialization**: The function initializes the solution vector \(w\) and other parameters. A hot start is used to improve convergence for each \(\lambda\).
- **Iterative Updates**: For each \(\lambda\), the function iteratively updates the solution vector using the soft-thresholding rule.
- **Termination**: The loop terminates when the solution converges or the maximum number of iterations is reached.

### Function Output

- **`X`**: A matrix where each column corresponds to the solution vector \(w\) for a given \(\lambda\).

## Example: Finding Optimal Weights for the First 100 Patients

### Setup

1. **Lambda Values**: A range of \(\lambda\) values is defined logarithmically.
2. **Data Loading**: Breast cancer dataset is loaded, and the first 100 patients' data is used.

### Execution

The `ista_solve_hot` function is used to find solutions for each \(\lambda\), and results are analyzed as follows:

- **L1 Norms**: The L1 norm of the solution vectors is computed to understand how the sparsity of solutions changes with \(\lambda\).
- **Residuals**: The residuals (difference between predicted and actual values) are calculated to evaluate the model's fit.

### Results and Analysis

- **L1 Norm Plot**: As \(\lambda\) increases, the L1 norm of the solutions typically increases, indicating more sparsity. This is expected in Lasso regression where higher \(\lambda\) encourages sparsity.
- **Residuals Plot**: Residuals generally decrease as \(\lambda\) increases up to a point, after which they may start to increase due to over-penalization. This demonstrates the trade-off between fitting the data and regularization.

## Visualizations

### L1 Norm vs. Lambda

The plot typically shows how the L1 norm of the solution vectors changes with \(\lambda\). As \(\lambda\) increases, the L1 norm should increase, reflecting greater sparsity in the model.

### Residuals vs. Lambda

The residuals plot illustrates how the fit of the model varies with \(\lambda\). Initially, residuals decrease, indicating a better fit, but after a certain \(\lambda\), residuals may increase, indicating over-regularization.

## Conclusion

The iterative soft-thresholding approach with hot start effectively solves the Lasso regression problem, providing insights into the trade-offs between model sparsity and fit. This method is computationally efficient and suitable for handling a range of \(\lambda\) values in practice.
