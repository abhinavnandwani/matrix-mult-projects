## Data Fitting vs. Sparsity Tradeoff

This assignment explores sparse regularization in a least squares problem using the `BreastCancer.mat` dataset. The dataset contains gene expression levels from 295 patients, with 8141 genes as features. The goal is to analyze the tradeoff between data-fitting and sparsity in the context of Lasso regression.

### Background

The journal article *[A Gene-Expression Signature as a Predictor of Survival in Breast Cancer](https://www.nejm.org/doi/full/10.1056/NEJMoa021967)* (NEJM, 2002) provides significant insights into how gene expression profiles can predict patient outcomes in breast cancer. The study presents a gene-expression signature that correlates with survival rates, emphasizing the importance of specific genes in prognosis.

#### Key Components of the Article:
- **Objective:** To identify a set of genes whose expression levels predict survival in breast cancer patients.
- **Methods:** Utilizes microarray technology to analyze gene expression profiles and employs statistical models to identify predictive gene signatures.
- **Findings:** Identifies a 70-gene signature associated with patient survival, demonstrating the potential of gene-expression profiles in prognostic assessments.
- **Relevance:** The study highlights the role of gene selection in improving predictive models, which is directly applicable to the Lasso regression problem we are addressing.

### Problem Statement

We seek to solve the Lasso problem:

$$
\mathbf{w}^* = \arg \min_{\mathbf{w} \in \mathbb{R}^n} \|A\mathbf{w} - \mathbf{d}\|_2^2 + \lambda \|\mathbf{w}\|_1
$$

where \(\mathbf{w}\) represents the weight vector for the gene expression levels. The regularization parameter \(\lambda\) controls the tradeoff between fitting the data well and achieving sparsity in the weight vector.

### Methodology

Scripts are provided to implement the iterative soft-thresholding algorithm using proximal gradient descent to solve the Lasso problem. The algorithm is designed to handle varying values of \(\lambda\) efficiently through a hot start procedure. This approach uses the converged solution from one \(\lambda\) value as the initial guess for the next, accelerating convergence when subsequent \(\lambda\) values lead to similar solutions.

### Usage Instructions

To run the scripts, ensure you have the necessary dependencies installed. Execute the provided script with the appropriate parameters to perform Lasso regression with varying \(\lambda\). Example usage:

```bash
python lasso_regression.py --lambda_value <value>
