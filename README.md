# Parametric Curve Fitting using Non-Linear Least Squares

## Objective
The goal of this project is to estimate the unknown parameters **(θ, M, X)** in a given **parametric curve model** so that it best fits the observed dataset (`xy_data.csv`).

The parametric equations are:

\[
x(t) = t \cos\theta - e^{M|t|}\sin(0.3t)\sin\theta + X
\]
\[
y(t) = 42 + t\sin\theta + e^{M|t|}\sin(0.3t)\cos\theta
\]

---

## Methodology

1. **Data Loading**
   - The dataset `xy_data.csv` is loaded using **Pandas**.
   - Observed coordinates are extracted as arrays:  
     `x_obs`, `y_obs`.
   - A corresponding `t` range (6 → 60) is generated to match the number of data points.

2. **Model Definition**
   - The equations are implemented in a Python function `model_function(theta, M, X, t)` to generate predicted values of `x(t)` and `y(t)`.

3. **Error Function**
   - The residuals are computed as:
     ```
     r_x = x_model - x_obs
     r_y = y_model - y_obs
     ```
   - The total squared error to minimize is:
     \[
     E(\theta, M, X) = \sum_i (r_{x,i}^2 + r_{y,i}^2)
     \]

4. **Optimization**
   - The `scipy.optimize.least_squares()` function is used to minimize `E(θ, M, X)`.
   - Constraints:
     ```
     0° < θ < 50°
     -0.05 < M < 0.05
     0 < X < 100
     ```

5. **Evaluation**
   - Fit quality is evaluated using the **L1 distance**:
     \[
     L_1 = \sum_i (|x_{\text{model}} - x_{\text{obs}}| + |y_{\text{model}} - y_{\text{obs}}|)
     \]
   - Plots compare predicted vs observed data.

---

## Results

| Parameter | Symbol | Value        | Description |
|------------|----------|--------------|--------------|
| Angle      | θ        | 0.5163 rad (29.58°) | Rotation of curve |
| Exponential factor | M | -0.05 | Slight exponential decay |
| Translation | X | 55.0135 | Horizontal shift |

**L1 Distance:** 38,102.17  
**Mean L1 per point:** 25.40  

---

## Interpretation

- **θ = 29.58°** → Curve rotated upwards from x-axis.  
- **M = -0.05** → Damped oscillations with increasing t.  
- **X = 55.01** → Shifts curve right to align with data.

The final model visually and numerically fits the observed dataset well.

---



