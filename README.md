# RBF Network Analysis for Classification

## Overview
This project investigates the performance of **Radial Basis Function (RBF) Networks** in a classification task using a synthetic dataset of 441 distinct 2D data points. The experiment analyzes the impact of the spread parameter (`σ`) and the choice of RBF kernel centers on training and validation accuracy and Mean Squared Error (MSE). Three models are compared: one using all training points as centers, another with 150 randomly selected centers, and a third with 150 K-Means cluster centers. The goal is to understand how center selection and `σ` affect model performance and generalization.

## Dataset
- **Generation**: 441 unique combinations of `(xi, xj)`, where `xi` and `xj` range from `-2.0` to `2.0` in steps of `0.2` (21 values: `[-2.0, -1.8, ..., 1.8, 2.0]`).
- **Split**:
  - Training: 352 points (80%).
  - Validation: 89 points (20%).

## Methodology
The analysis is split into two parts:

### Part 1: All Training Points as Centers (Model 1)
- All 352 training points serve as RBF kernel centers.
- Evaluated across `σ = [0.1, 2.0]` in increments of `0.1`.

### Part 2: Subset of Centers
- **A) 150 Random Centers (Model 2)**: 150 points randomly sampled from training data.
- **B) 150 K-Means Centers (Model 3)**: 150 centers derived via K-Means clustering on training data.
- Both tested across the same `σ` range.

### Metrics
- **Accuracy**: Percentage of correct classifications.
- **Mean Squared Error (MSE)**: Error between predicted and true values.
- **Parameter**: `σ` (spread) controls the Gaussian kernel’s width.

## Results

### Model 1: All Training Points
- **Training**: 
  - Peak accuracy: 100% at `σ = [0.1, 0.3]`.
  - Drops to 20-50% beyond `σ = 0.5`.
  - MSE: 0 at `σ = [0.1, 0.3]`, rises to 1.5-3 later.
- **Validation**: 
  - Peak accuracy at `σ = 0.1`, falls to 20-75% beyond `σ = 0.5`.
  - MSE: 0 at `σ = [0.1, 0.3]`, then 1.5-3.

### Model 2: 150 Random Centers
- **Training**: 
  - Peak accuracy at `σ = [0.3, 0.6]`, fluctuates beyond `σ = 0.7`.
  - MSE: Near 0 at `σ = [0.1, 0.6]`, peaks at ~2.5.
- **Validation**: 
  - High accuracy up to `σ = 0.6`, fluctuates later.
  - MSE: 0 at `σ = [0.1, 0.6]`, rises thereafter.

### Model 3: 150 K-Means Centers
- **Training & Validation**: 
  - Good accuracy at `σ = [0.1, 0.8]`.
  - MSE: Near 0 at `σ = [0.1, 0.8]`, fluctuates beyond `σ = 0.8`.

### Comparative Analysis
- **Model 1**: Overfits, performs poorly beyond `σ = 0.3` due to excessive centers.
- **Model 2**: Stable up to `σ = 0.6`, less overfitting than Model 1.
- **Model 3**: Best performance up to `σ = 1.1`, leveraging clustered centers for better generalization.
- **Trend**: Low `σ` yields high accuracy; high `σ` introduces noise, reducing performance.

## Insights
- **Low `σ`**: Narrow kernels interpolate similar points well, boosting accuracy.
- **High `σ`**: Wide kernels include dissimilar points, degrading performance.
- **Overfitting**: Model 1’s use of all points as centers causes rapid accuracy drops.
- **Center Selection**: K-Means (Model 3) outperforms random selection (Model 2) by capturing data patterns effectively.

## Requirements
- **Python**: Core language.
- **NumPy**: Dataset generation and computation.
- **Scikit-learn**: K-Means clustering.
- **Matplotlib**: Visualization of accuracy/MSE trends (implied).

## How to Run
1. **Generate Dataset**: Create 441 `(xi, xj)` pairs using the range `[-2.0, 2.0]` with `0.2` steps.
2. **Split Data**: Divide into 352 training and 89 validation points.
3. **Implement Models**:
   - Model 1: Use all 352 training points as centers.
   - Model 2: Randomly select 150 training points.
   - Model 3: Apply K-Means (k=150) to training data for centers.
4. **Evaluate**: Test each model across `σ = [0.1, 2.0]` with `0.1` steps.
5. **Analyze**: Compute accuracy and MSE, plot results.

## Future Work
- Experiment with real-world datasets to validate findings.
- Explore additional center selection methods (e.g., hierarchical clustering).
- Test adaptive `σ` values per kernel for improved flexibility.