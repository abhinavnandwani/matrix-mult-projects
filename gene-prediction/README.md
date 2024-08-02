## Data Fitting vs. Sparsity Tradeoff

This assignment uses the dataset `BreastCancer.mat` to explore sparse regularization of a least squares problem. The journal article "A gene-expression signature as a predictor of survival in breast cancer" provides background on the role of genes in breast cancer.

The goal is to solve the Lasso problem:

$$
\mathbf{w}^* = \arg \min_{\mathbf{w} \in \mathbb{R}^n} \|A\mathbf{w} - \mathbf{d}\|_2^2 + \lambda \|\mathbf{w}\|_1
$$

Here, $\mathbf{w}$ is the weight vector applied to the expression levels of 8141 genes, and there are 295 patients (feature sets and labels). In this problem, we will vary $\lambda$ to explore the tradeoff between data-fitting and sparsity.

Scripts that implement iterative soft-thresholding via proximal gradient descent to solve the LASSO problem are available. The scripts use a hot start procedure for finding the solution with different values for $\lambda$. The initial guess for the next value of $\lambda$ is the converged solution for the preceding value. This accelerates convergence when subsequent values of $\lambda$ lead to similar solutions.
