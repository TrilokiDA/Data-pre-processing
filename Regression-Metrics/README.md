The major Regression metrics
---

### 🔹 1. **Mean Absolute Error (MAE)**

#### ✅ Why we use it:

MAE measures the **average magnitude** of the errors in a set of predictions, without considering their direction (i.e., positive or negative). It tells us how far our predictions are from actual values on average.

#### 🔍 How it's calculated:

$$
\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} | y_i - \hat{y}_i |
$$

* $y_i$: Actual value
* $\hat{y}_i$: Predicted value
* $n$: Number of observations

#### 📌 Where to use:

* When you want a metric that’s **robust to outliers** and **easily interpretable**.
* Used in business applications where the cost of an error is linear (e.g., predicting delivery time).

#### 🔗 Related to others:

* MAE is **less sensitive to outliers** compared to RMSE (Root Mean Squared Error).
* Always non-negative and **in the same unit** as the output variable.

---

### 🔹 2. **Mean Squared Error (MSE)**

#### ✅ Why we use it:

MSE measures the **average squared difference** between predicted and actual values. It **penalizes larger errors** more than MAE, making it useful when large errors are especially undesirable.

#### 🔍 How it's calculated:

$$
\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
$$

#### 📌 Where to use:

* When you want to **heavily penalize large errors**.
* Common in optimization problems because it's **differentiable**, making it suitable for gradient-based algorithms like linear regression.

#### 🔗 Related to others:

* MSE is the **square** of RMSE.
* Compared to MAE, it’s **more sensitive to outliers**.
* Same unit as the **square** of the target variable (not interpretable in original unit).

---

### 🔹 3. **Root Mean Squared Error (RMSE)**

#### ✅ Why we use it:

RMSE is the **square root of MSE**, which brings the error back to the original unit of the target variable, making it easier to interpret.

#### 🔍 How it's calculated:

$$
\text{RMSE} = \sqrt{\text{MSE}} = \sqrt{ \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 }
$$

#### 📌 Where to use:

* When interpretability in the same unit as the output is important.
* Useful in domains like real estate (predicting house prices), energy demand, etc.

#### 🔗 Related to others:

* RMSE **amplifies the effect of outliers** more than MAE.
* RMSE ≥ MAE (always true except when all errors are the same).

---

### 🔹 4. **Mean Absolute Percentage Error (MAPE)**

#### ✅ Why we use it:

MAPE expresses the error **as a percentage** of the actual values, making it **scale-independent** and easy to interpret.

#### 🔍 How it's calculated:

$$
\text{MAPE} = \frac{100\%}{n} \sum_{i=1}^{n} \left| \frac{y_i - \hat{y}_i}{y_i} \right|
$$

#### 📌 Where to use:

* When comparing models across datasets with **different scales**.
* Business forecasts (e.g., sales, demand), where % error is intuitive.

#### ⚠️ Pitfalls:

* Undefined when $y_i = 0$
* Sensitive to small actual values

#### 🔗 Related to others:

* Unlike MAE/RMSE, MAPE is **relative**, not absolute.
* Used for performance **comparison across units**.

---

### 🔹 5. **Symmetric Mean Absolute Percentage Error (sMAPE)**

#### ✅ Why we use it:

sMAPE adjusts MAPE to **symmetrically** treat over- and under-forecasting, especially useful when actual values are near zero.

#### 🔍 How it's calculated:

$$
\text{sMAPE} = \frac{100\%}{n} \sum_{i=1}^{n} \frac{|y_i - \hat{y}_i|}{(|y_i| + |\hat{y}_i|)/2}
$$

#### 📌 Where to use:

* Time series forecasting
* Better than MAPE when $y_i$ can be close to 0

#### 🔗 Related to others:

* An improvement over MAPE in handling zero or near-zero values.
* Still suffers when both actual and predicted are small.

---

### 🔹 6. **R-squared (R² Score)**

#### ✅ Why we use it:

R² measures the **proportion of variance explained** by the model. It's a **goodness-of-fit** measure.

#### 🔍 How it's calculated:

$$
R^2 = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}
$$

* $\bar{y}$: Mean of actual values

#### 📌 Where to use:

* When you want to understand how much variability in the target is captured by the model.
* Useful for model comparison.

#### 🔗 Related to others:

* R² ranges from $-\infty$ to 1.
* 1 = perfect fit, 0 = no better than mean, negative = worse than mean.
* Based on **MSE** in the numerator and total variance in the denominator.

---

### 🔹 7. **Adjusted R-squared**

#### ✅ Why we use it:

Adjusted R² adjusts the R² score for the **number of predictors**, preventing overestimation of model quality when adding irrelevant features.

#### 🔍 How it's calculated:

$$
\text{Adjusted } R^2 = 1 - \left( \frac{(1 - R^2)(n - 1)}{n - p - 1} \right)
$$

* $n$: Number of observations
* $p$: Number of predictors

#### 📌 Where to use:

* In multiple linear regression
* When comparing models with **different numbers of features**

#### 🔗 Related to others:

* Always **≤ R²**
* Rewards useful features, **penalizes** unnecessary ones

---

### 🔹 8. **Huber Loss**

#### ✅ Why we use it:

Huber loss combines advantages of MAE and MSE: it's **quadratic** for small errors and **linear** for large ones — making it **robust to outliers** while still differentiable.

#### 🔍 How it's calculated:

$$
L_\delta(a) = 
\begin{cases} 
\frac{1}{2}a^2 & \text{for } |a| \leq \delta \\
\delta(|a| - \frac{1}{2}\delta) & \text{otherwise}
\end{cases}
$$

* $a = y_i - \hat{y}_i$

#### 📌 Where to use:

* When you want a **robust and smooth** loss function in optimization.
* Often used in robust regression models.

#### 🔗 Related to others:

* Transitions from **MSE** (near center) to **MAE** (far from center).
* Requires tuning $\delta$ threshold.

---

### 🔹 9. **Mean Bias Deviation (MBE)**

#### ✅ Why we use it:

MBE gives the **average error with sign**, telling if the model tends to **overpredict or underpredict**.

#### 🔍 How it's calculated:

$$
\text{MBE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)
$$

#### 📌 Where to use:

* In **energy modeling**, environmental modeling, or when **bias direction** matters.
* Indicates model tendency, not accuracy.

#### 🔗 Related to others:

* Not typically used alone — often paired with RMSE or MAE.

---

### 🔹 10. **Relative Absolute Error (RAE)**

#### ✅ Why we use it:

RAE compares the **total absolute error** of the model to that of a naive model that predicts the mean of actuals.

#### 🔍 How it's calculated:

$$
\text{RAE} = \frac{\sum |y_i - \hat{y}_i|}{\sum |y_i - \bar{y}|}
$$

#### 📌 Where to use:

* To evaluate model improvement over a baseline (e.g., mean predictor).

#### 🔗 Related to others:

* If RAE < 1, model is better than mean.
* Closely linked to MAE and R².

---

### 🔹 11. **Relative Squared Error (RSE)**

#### ✅ Why we use it:

RSE compares **squared errors** to a naive predictor's squared error.

#### 🔍 How it's calculated:

$$
\text{RSE} = \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}
$$

#### 📌 Where to use:

* When comparing models to a baseline using **squared loss**.

#### 🔗 Related to others:

* Inverse of $R^2$:

  $$
  R^2 = 1 - RSE
  $$

---

### 🔚 Summary Table

| Metric     | Penalizes Outliers | Scale Dependent | Interpretable | Robust to Outliers |
| ---------- | ------------------ | --------------- | ------------- | ------------------ |
| MAE        | No                 | Yes             | Yes           | ✅                  |
| MSE        | ✅                  | Yes             | No            | ❌                  |
| RMSE       | ✅✅                 | Yes             | ✅             | ❌                  |
| MAPE       | ❌                  | No              | ✅             | ❌                  |
| sMAPE      | ❌                  | No              | ✅             | ❌                  |
| R²         | No                 | No              | Partial       | ❌                  |
| Adj. R²    | No                 | No              | Partial       | ❌                  |
| Huber Loss | ✅                  | Yes             | No            | ✅                  |
| MBE        | No                 | Yes             | Partial       | ❌                  |
| RAE/RSE    | No                 | No              | Partial       | ❌                  |


---

## 🧩 Why This Is Important:

Not all metrics are equally useful in every regression task. The **best metric** often depends on:

| Factor                     | Why It Matters                                                                        |
| -------------------------- | ------------------------------------------------------------------------------------- |
| **Scale of the target**    | Some metrics (like MAPE) don’t work well if values are near zero                      |
| **Presence of outliers**   | Some metrics (like RMSE) are very sensitive to outliers; others (like MAE) are robust |
| **Business goal**          | Are you minimizing large errors? Is direction of bias important?                      |
| **Interpretability needs** | Some metrics are easier to explain to stakeholders                                    |
| **Model comparison**       | Relative metrics help compare to a baseline (like R², RAE, RSE)                       |

---

## ✅ Example 1: Predicting House Prices

* **Target:** House price in ₹
* **Problem nature:** Large range, outliers possible
* **Best metrics:**

  * RMSE → To heavily penalize large price prediction errors
  * MAE → For interpretable average error
  * R² → For model goodness-of-fit

---

## ✅ Example 2: Forecasting Energy Demand

* **Target:** kWh usage (can be close to zero)
* **Problem nature:** Forecasting time series
* **Best metrics:**

  * sMAPE → Handles % error better when values are near zero
  * MAE → Stable across forecast horizon
  * MBE → To check if the model over- or under-predicts

---

## ✅ Example 3: Predicting Sales Volume for Inventory

* **Target:** Number of items sold (e.g., 0–100)
* **Problem nature:** Many small values, no outliers
* **Best metrics:**

  * MAPE → Good because % error is meaningful
  * MAE → Direct interpretation
  * Adjusted R² → For comparing models with different features

---
