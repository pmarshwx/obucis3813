# CIS 3813 – Advanced Data Science
## Midterm Exam Study Guide
### Weeks 1–7 | Spring 2026 | Dr. Patrick T. Marsh

> **Exam Format:** Paper and pencil — no computers, no AI, no notes.
> **Exam Focus:** Conceptual understanding, algorithm selection, metric interpretation, and reading/debugging code.
> You do **not** need to memorize code syntax from scratch, but you should be able to read code and explain what it does.

---

# Week 1 — The Machine Learning Workflow

## Key Concepts

### What is Machine Learning?
Machine learning uses algorithms to parse data, learn from it, and make predictions or decisions — instead of coding explicit rules, we let the algorithm discover rules from data.

**Three Types:**
- **Supervised Learning** — Learning from labeled data (with an "answer key")
  - *Regression* — predicting a continuous quantity (e.g., house price)
  - *Classification* — predicting a category/label (e.g., spam vs. not spam)
- **Unsupervised Learning** — Finding patterns in unlabeled data (no "answer key")
  - *Clustering* — grouping similar data
  - *Dimensionality Reduction* — compressing data
- **Reinforcement Learning** — Learning through reward/penalty feedback

### The Machine Learning Workflow
> Problem ↔ Data Acquisition ↔ Cleaning/Preparation ↔ Exploration/Visualization ↔ Modeling/Inference ↔ Evaluation ↔ Communication/Deployment

Note that **arrows point both directions** — you can jump from any stage to any other stage repeatedly.

### Train/Test Split
- **Training set** — data the model learns from (analogous to homework problems)
- **Test set** — data used to evaluate the model (analogous to a final exam)
- The model should **never** see test data during training

### Data Leakage
Data leakage occurs when information from the test set is inadvertently used during training, producing **artificially inflated performance** that does not hold up in the real world.

**Classic example:** Feature selection performed on the *entire* dataset before the train/test split — the model "peeked" at the test data.

**The fix:** Always split data **first**, then fit all preprocessing steps only on training data.

### Bias-Variance Tradeoff

| | Definition | Analogy |
|---|---|---|
| **Bias** | Error from wrong assumptions; model is too simple | Consistently missing the target in the same direction (always left of center) |
| **Variance** | Error from sensitivity to training data; model is too complex | Scatter all over the place — inconsistent results |

**Total Error = Bias² + Variance + Irreducible Error**

| Situation | Bias | Variance | Called |
|---|---|---|---|
| Model too simple | High | Low | Underfitting |
| Model too complex | Low | High | Overfitting |
| Just right | Low | Low | Sweet spot |

**Strategies to find the sweet spot:** more data, simpler models, regularization (Week 4), cross-validation (Week 5).

### Functions & Slope (Calculus Review)
- A **function** maps each input to exactly one output
- **Slope (derivative)** = how much the output changes per unit change in input
- For `y = mx + b`, slope = m (constant)
- For nonlinear functions, slope varies at every point — the derivative gives the instantaneous slope
- In ML, the model learns by following the **slope of the error** — this is gradient descent (Week 2)

---

## Study Questions — Week 1

1. What is the difference between supervised and unsupervised learning? Give one example of each.
2. In the exam analogy, what do "homework problems" and "the final exam" correspond to in machine learning terms?
3. A classmate builds a model that achieves 98% accuracy on training data but only 55% on test data. What is the likely cause? What can be done to fix it?
4. Define bias and variance in your own words. Draw a rough sketch of the bias-variance tradeoff curve.
5. A researcher selects the top 50 most correlated features from a dataset of 10,000 features *before* splitting into train and test. Why is this a problem? How should it be done correctly?
6. A model has high bias. Should you increase or decrease model complexity? Why?

---

---

# Week 2 — How Models Learn (Gradient Descent)

## Key Concepts

### The Learning Problem
"Learning" = finding the **best parameter values** for a model.

For a linear model `ŷ = mx + b`, we want to find the values of `m` and `b` that make predictions as close as possible to actual values.

### Loss Functions
A **loss function** (also called a cost function) measures how wrong predictions are.

**Mean Squared Error (MSE):**
$$\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$

Why squared?
- Penalizes large errors more than small ones
- Always positive (no cancellation)
- Differentiable everywhere (smooth — necessary for gradient descent)

### The Loss Landscape
For a model with parameters `m` and `b`, MSE creates a **surface** over the parameter space. For linear regression, this surface is shaped like a **bowl** — there is a clear global minimum. The goal of optimization is to find the lowest point.

### Gradient Descent
**Intuition:** Imagine you are blindfolded on a hilly landscape and want to find the lowest point. You feel the slope under your feet and take a step downhill. Repeat.

**The Algorithm:**
1. Start with random parameter values
2. Compute the gradient (slope) of the loss function
3. Take a step in the **opposite** direction of the gradient
4. Repeat until convergence

**The Update Rule:**
$$\theta_{\text{new}} = \theta_{\text{old}} - \alpha \cdot \nabla L(\theta)$$

Where:
- θ = parameter (e.g., weight `w` or bias `b`)
- α (alpha) = **learning rate** (step size)
- ∇L(θ) = gradient of the loss

### The Gradient (Direction & Magnitude)
- **Positive gradient** → function is increasing → move **left** (decrease θ) to reduce loss
- **Negative gradient** → function is decreasing → move **right** (increase θ) to reduce loss
- **Zero gradient** → at a critical point (minimum, maximum, or saddle point)

### The Learning Rate (α)
| α too large | α too small |
|---|---|
| Overshoot the minimum | Takes forever to converge |
| Loss may oscillate or diverge | Very slow training |

Choosing the right learning rate is part of **hyperparameter tuning**.

### Convergence
The algorithm has converged when the gradient is near zero and the loss is not changing significantly. At this point, `θ` is at (or very near) a minimum of the loss surface.

### MSE Gradients for Linear Regression
For `ŷ = mX + b`:
- Gradient with respect to `m`: $\frac{\partial \text{MSE}}{\partial m} = \frac{-2}{n} \sum x_i(y_i - \hat{y}_i)$
- Gradient with respect to `b`: $\frac{\partial \text{MSE}}{\partial b} = \frac{-2}{n} \sum (y_i - \hat{y}_i)$

---

## Study Questions — Week 2

1. What is a loss function? Why do we use Mean Squared Error rather than Mean Absolute Error in many situations?
2. Describe gradient descent in your own words, as if explaining to someone who has never heard of it.
3. If the gradient at a point is positive, should we increase or decrease the parameter? Why?
4. A model's loss is not decreasing during training. Give two possible causes related to the learning rate.
5. What does it mean for gradient descent to "converge"?
6. How does gradient descent relate to the concept of slope (derivative) from calculus?
7. Sketch what the loss landscape looks like for a simple linear regression model with two parameters (m and b). What is the goal of gradient descent on this surface?

---

---

# Week 3 — Linear Algebra for Data Science

## Key Concepts

### Building Blocks

| Term | What it is | ML Context | NumPy Shape |
|---|---|---|---|
| **Scalar** | A single number | One measurement (e.g., one person's age) | `()` |
| **Vector** | Ordered list of numbers | One data sample (all features for one row) | `(n,)` |
| **Matrix** | 2D grid of numbers | Entire dataset (all samples × all features) | `(m, n)` |

### Shape Matters!
- `(n,)` — 1D vector
- `(m, n)` — matrix with m rows and n columns
- `(m, 1)` — column vector
- `(1, n)` — row vector

Many bugs in data science arise from **shape mismatches**. Always check `.shape`.

### Element-wise Operations
When adding, subtracting, or multiplying vectors of the same length, NumPy operates **element by element**:
```
a = [1, 2, 3]
b = [4, 5, 6]
a + b = [5, 7, 9]
a * b = [4, 10, 18]
```

**Application:** Standardizing a feature (subtracting mean, dividing by std) is an element-wise operation on an entire column at once.

### The Dot Product
**The single most important operation in ML.**

Given vectors **a** = [a₁, a₂, ..., aₙ] and **b** = [b₁, b₂, ..., bₙ]:

$$\mathbf{a} \cdot \mathbf{b} = a_1 b_1 + a_2 b_2 + \cdots + a_n b_n$$

*Multiply corresponding elements, then add them all up.*

**Three ways to think about the dot product:**
1. **Algebraic** — multiply pairs, sum them up
2. **Geometric** — measures how much two vectors point in the same direction
3. **Machine Learning** — it's how a linear model makes a single prediction!

**A linear model prediction IS a dot product:**
$$\hat{y} = w_1 x_1 + w_2 x_2 + \cdots + w_p x_p + b = \mathbf{w} \cdot \mathbf{x} + b$$

### Matrix Multiplication
Matrix multiplication = **many dot products organized into a grid**.

**The shape rule:** `(m × n) @ (n × p) = (m × p)`

- Inner dimensions must match! The `n` in `(m × n)` must equal the `n` in `(n × p)`.
- Each element of the result is the dot product of a **row from the left** matrix with a **column from the right** matrix.

**Why this matters:**
```
houses (4×3)  @  weights (3,)  =  predictions (4,)
```
This predicts prices for all 4 houses simultaneously — exactly what scikit-learn's `.predict()` does internally.

### DataFrames vs. NumPy Arrays
| | pandas DataFrame | NumPy array |
|---|---|---|
| **Column names** | Yes | No |
| **Speed** | Slower (overhead) | Much faster |
| **ML use** | Data exploration, display | Model training, computation |

Convert with `.values` or `.to_numpy()`.

---

## Study Questions — Week 3

1. What is the difference between a vector and a matrix? How do these map to data science concepts?
2. Compute the dot product of [2, 3, 4] and [1, 0, 2] by hand.
3. You have a feature matrix with shape (500, 8) and a weight vector with shape (8,). What is the shape of the output when you multiply them? What does that output represent?
4. Why does the shape rule say the **inner** dimensions must match for matrix multiplication?
5. A model predicts house prices using `ŷ = w · x + b`. If `w = [150, 20000, -500]` (weights for sqft, bedrooms, age) and `b = 50000`, what is the predicted price for a house with 2000 sqft, 4 bedrooms, and 10 years old? Show your work.
6. Why would we ever convert a pandas DataFrame to a NumPy array?

---

---

# Week 4 — Multiple Linear Regression & Regularization

## Key Concepts

### From Simple to Multiple Linear Regression
**Simple linear regression:** `ŷ = w₀ + w₁x` (one feature)

**Multiple linear regression:** `ŷ = w₀ + w₁x₁ + w₂x₂ + … + wₚxₚ` (p features)

In **matrix notation** (connecting to Week 3): `ŷ = Xw`

Adding more features increases risk of **overfitting** — the model memorizes training noise.

### The Problem: Unscaled Coefficients
With features at different scales (e.g., income ranges 0–15, population ranges 3–35,000), raw coefficients **cannot be compared directly**. A small coefficient on population doesn't mean population is unimportant — it means a 1-person change has a tiny dollar effect.

### Regularization
Regularization adds a **penalty term** to the cost function to discourage large coefficients. A large coefficient often means the model is relying too heavily on one feature — possibly overfitting noise.

**Standard OLS minimizes:**
$$\text{Cost}_{OLS} = \sum (y_i - \hat{y}_i)^2$$

**Regularized regression minimizes:**
$$\text{Cost}_{regularized} = \sum (y_i - \hat{y}_i)^2 + \alpha \cdot \text{Penalty}(\mathbf{w})$$

The **traveler analogy:** Packing everything (all features) is like preparing for every scenario. An airline charging per pound (regularization) forces you to weigh the value of each item (feature) against its cost.

### Ridge Regression (L2)
$$\text{Penalty} = \alpha \sum_{j=1}^{p} w_j^2$$

- **Shrinks** all coefficients toward zero
- Coefficients are **rarely exactly zero**
- Like *Traveler A* who distributes weight evenly
- Best when you expect most features to matter, but want smaller coefficients
- Constraint region is a **circle/sphere** in coefficient space

### Lasso Regression (L1)
$$\text{Penalty} = \alpha \sum_{j=1}^{p} |w_j|$$

- **Shrinks** coefficients; some become **exactly zero**
- Performs automatic **feature selection** — drops irrelevant features
- Like *Traveler B* who eliminates entire items from their bag
- Best when you believe many features are irrelevant
- Constraint region is a **diamond** in coefficient space — corners touch axes → exact zeros

### The Geometry of Regularization
The OLS solution lives at the center of the RSS contours (an ellipse). Regularization imposes a constraint — Ridge uses a circle, Lasso uses a diamond. The regularized solution is where the RSS ellipse **first touches** the constraint boundary:
- Diamond corners lie on the axes → Lasso frequently finds solutions where one coordinate = 0 (exact zero coefficient)
- Circle has no corners → Ridge rarely zeroes out coefficients exactly

### The Alpha Hyperparameter (α)
| α value | Effect |
|---|---|
| α = 0 | No penalty → standard OLS |
| α → ∞ | Maximum penalty → all coefficients → 0 |
| "Just right" α | Balances fit vs. simplicity |

**Choosing α requires cross-validation (Week 5).**

### Feature Scaling — A CRITICAL Prerequisite
Regularization penalizes based on **coefficient size**, which depends on **feature scale**. An unscaled feature that ranges over 35,000 units will have a tiny coefficient — and the penalty will be unfairly small for it.

**Fix: StandardScaler** — subtract mean, divide by standard deviation:
$$x_{scaled} = \frac{x - \mu}{\sigma}$$

After scaling, all features are on the same scale → regularization applies fairly.

**CRITICAL RULE:** Fit the scaler **only on training data**, then transform both train and test:
```python
scaler.fit(X_train)          # Learn mean/std from train only
X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)   # Use train's mean/std!
```
Fitting the scaler on the full dataset is **data leakage**.

### Ridge vs. Lasso Summary

| | Ridge (L2) | Lasso (L1) |
|---|---|---|
| Penalty | Sum of squared weights | Sum of absolute weights |
| Coefficients → 0? | Approaches but not exactly | Can be exactly zero |
| Feature selection? | No | Yes |
| Use when | Most features relevant | Many features irrelevant |
| Constraint shape | Circle | Diamond |

---

## Study Questions — Week 4

1. Why does adding more features to a linear regression model increase the risk of overfitting?
2. What problem does regularization solve? Describe it in the context of the traveler analogy.
3. What is the key difference between Ridge and Lasso regularization in terms of what they do to coefficients?
4. Why does Lasso produce exact zeros while Ridge does not? (Think about the geometry — circles vs. diamonds.)
5. Why is feature scaling a critical prerequisite for regularization?
6. A data scientist fits a StandardScaler to the entire dataset before splitting into train and test. What is wrong with this approach?
7. If α = 0 in Ridge regression, what model do you get? What happens as α approaches infinity?
8. You have a dataset with 200 features and you believe most are irrelevant. Should you use Ridge or Lasso? Why?

---

---

# Week 5 — Cross-Validation & Model Selection

## Key Concepts

### The Problem with Simple Train/Test Splits
A single train/test split has a **hidden problem**: the test score depends heavily on which samples ended up in the test set. By chance, you might get an "easy" or "hard" test set — making the same model look great or poor with no real change.

**Consequences:**
- Unreliable model comparisons
- Hyperparameter selection that depends on luck of the split
- Overconfident deployment expectations

### K-Fold Cross-Validation
**The solution:** Use ALL data for both training and testing — just not simultaneously.

**Algorithm:**
1. Divide data into K equal parts ("folds") — typically K = 5 or K = 10
2. Train K times: each time, use K-1 folds for training, 1 fold for testing
3. Rotate which fold is the test fold each time
4. Average the K test scores

**Result:** Every sample is used for testing exactly once, and K different performance measurements are averaged.

**Why K=5?** With K=5, each fold uses 80% of data for training — a good balance between training size and evaluation reliability.

### Implementing Cross-Validation
```python
from sklearn.model_selection import cross_val_score
scores = cross_val_score(model, X_scaled, y, cv=5, scoring='r2')
print(f"Mean: {scores.mean():.3f} ± {scores.std():.3f}")
```

**Important:** `cross_val_score` does not automatically scale data. Use a Pipeline (see below) to handle this correctly!

### Common Scoring Metrics

**Regression:**
| Parameter | Metric | Notes |
|---|---|---|
| `'r2'` | R² | Proportion of variance explained; higher = better |
| `'neg_mean_squared_error'` | Negative MSE | Negative because sklearn maximizes; negate to get MSE |
| `'neg_root_mean_squared_error'` | Negative RMSE | Same units as target; easier to interpret than MSE |
| `'neg_mean_absolute_error'` | Negative MAE | More robust to outliers than MSE |

**Classification:**
| Parameter | Metric | Notes |
|---|---|---|
| `'accuracy'` | Accuracy | Fraction correct; misleading for imbalanced data |
| `'f1'` | F1-Score | Balance of precision and recall |
| `'roc_auc'` | ROC-AUC | Probability that model ranks a positive higher than a negative |

### Hyperparameter Tuning: GridSearchCV
Instead of manually trying different values of α (or other hyperparameters), `GridSearchCV` systematically evaluates every combination.

```python
param_grid = {'ridge__alpha': [0.001, 0.01, 0.1, 1.0, 10.0, 100.0]}
grid_search = GridSearchCV(pipeline, param_grid, cv=5, scoring='r2')
grid_search.fit(X_train, y_train)
print(grid_search.best_params_)
```

**Limitation:** With many hyperparameters, the number of combinations explodes (the "curse of dimensionality" for search spaces).

### RandomizedSearchCV
Instead of exhaustive search, samples hyperparameter combinations **randomly** for a fixed number of iterations.

- **Faster** than GridSearchCV for large search spaces
- Trades completeness for speed
- Usually finds very good (if not the absolute best) parameters

```python
param_dist = {'ridge__alpha': np.logspace(-3, 3, 1000)}
random_search = RandomizedSearchCV(pipeline, param_dist, n_iter=50, cv=5)
```

### Pipelines
A Pipeline chains preprocessing and modeling steps into one object — eliminating data leakage risk and making code cleaner.

```python
from sklearn.pipeline import Pipeline
pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('ridge', Ridge())
])
```

**Critical benefit:** When used inside cross-validation, the scaler is fit only on training folds — never on the test fold. This is the correct way to prevent leakage.

### GridSearchCV vs. RandomizedSearchCV

| | GridSearchCV | RandomizedSearchCV |
|---|---|---|
| Search strategy | Exhaustive | Random sampling |
| Speed | Slower | Faster |
| Guarantee best | Yes (in grid) | No |
| Use when | Small search space | Large search space |

---

## Study Questions — Week 5

1. Why is a single train/test split insufficient for reliable model evaluation? Give a concrete example of how it could mislead you.
2. Describe how 5-fold cross-validation works, step by step.
3. How many times does each data point appear in a test fold during 5-fold cross-validation?
4. Why should preprocessing (like StandardScaler) be placed inside a Pipeline when doing cross-validation?
5. What is GridSearchCV doing, and when would you prefer RandomizedSearchCV instead?
6. A model's 5-fold CV scores are [0.82, 0.79, 0.75, 0.83, 0.81]. What would you report as its performance? How is this better than a single test score?
7. `cross_val_score` returns negative values when using `'neg_mean_squared_error'`. Why?
8. What is the difference between a **parameter** (learned during training) and a **hyperparameter** (set before training)?

---

---

# Week 6 — Logistic Regression & The Sigmoid Function

## Key Concepts

### Regression vs. Classification

| | Regression | Classification |
|---|---|---|
| **Output** | Continuous number | Category/label |
| **Example output** | $425,000 | "Spam" or "Not Spam" |
| **Loss function** | MSE | Log-loss (binary cross-entropy) |
| **Model** | Linear Regression | Logistic Regression |

### Why Linear Regression Fails for Classification
1. **Outputs outside [0, 1]** — can predict -0.5 or 1.7, which can't be probabilities
2. **No probabilistic interpretation** — what does "0.7" mean exactly?
3. **Treats classes as ordered numbers** — 0.5 isn't "halfway between spam and not spam"

### The Sigmoid Function (Logistic Function)
The sigmoid function transforms any real number into a value between 0 and 1:

$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

**Key properties:**
- **Range:** Always outputs between 0 and 1 (valid probability)
- **Shape:** S-curve (sigmoid = S-shaped)
- **Symmetry:** σ(0) = 0.5 exactly
- **Asymptotes:** Approaches 0 as z → -∞, approaches 1 as z → +∞
- **Differentiable:** Can be used with gradient descent

| z value | σ(z) approximately |
|---|---|
| z = -10 | ≈ 0.00005 (very close to 0) |
| z = -2 | ≈ 0.119 |
| z = 0 | = 0.500 (exactly) |
| z = 2 | ≈ 0.881 |
| z = 10 | ≈ 0.99995 (very close to 1) |

### Logistic Regression
Logistic regression uses a linear combination of features, then passes the result through the sigmoid:

$$z = w_0 + w_1 x_1 + w_2 x_2 + \cdots + w_p x_p = \mathbf{w} \cdot \mathbf{x} + b$$

$$P(\hat{y} = 1) = \sigma(z) = \frac{1}{1 + e^{-z}}$$

The output is interpreted as the **probability of belonging to class 1**.

### Decision Threshold
By default, a probability ≥ 0.5 is classified as class 1; < 0.5 as class 0.

```python
predicted_class = 1 if probability >= 0.5 else 0
```

**Shifting the threshold:**
- **Lower threshold** (e.g., 0.3) → catches more positives, but more false alarms (higher recall, lower precision)
- **Higher threshold** (e.g., 0.7) → fewer false alarms, but misses more positives (higher precision, lower recall)

This creates the **precision-recall tradeoff** (covered more deeply in Week 7).

### Log-Loss (Binary Cross-Entropy)
Logistic regression does not use MSE. Instead, it minimizes **log-loss**:

$$\text{Log-Loss} = -\frac{1}{n} \sum_{i=1}^{n} \left[ y_i \log(\hat{p}_i) + (1 - y_i) \log(1 - \hat{p}_i) \right]$$

**Intuition:** Heavily penalizes confident wrong predictions (predicting 0.99 when the true answer is 0 is much worse than predicting 0.55 when the true answer is 0).

### scikit-learn Implementation
```python
from sklearn.linear_model import LogisticRegression
model = LogisticRegression()
model.fit(X_train, y_train)
probabilities = model.predict_proba(X_test)   # Returns [P(class=0), P(class=1)]
predictions   = model.predict(X_test)          # Returns class labels (0 or 1)
```

---

## Study Questions — Week 6

1. What is the fundamental difference between a regression problem and a classification problem? Give one example of each.
2. Give three reasons why linear regression is inappropriate for binary classification.
3. Write the sigmoid function formula from memory. What is its output when z = 0?
4. As z approaches +∞, what does σ(z) approach? What about as z approaches -∞?
5. A logistic regression model outputs a probability of 0.73 for a patient. What class is predicted with a default threshold of 0.5? What would happen if you lowered the threshold to 0.4?
6. Why does logistic regression use log-loss instead of MSE?
7. A doctor needs to screen for cancer — missing a true case is catastrophic, but a false alarm just leads to more tests. Should they use a higher or lower threshold? Explain.
8. Logistic regression outputs 0.65. Interpret this number in plain English for a non-technical audience.

---

---

# Week 7 — Evaluating Classification Models

## Key Concepts

### The Accuracy Fallacy (The Finley Problem)
In 1884, Sgt. Finley reported 96.6% accuracy forecasting tornadoes. But predicting "no tornado" every time would have achieved 98.2% accuracy — better, while being completely useless.

**Lesson:** Accuracy is misleading for **imbalanced datasets** (where one class dominates).

### The Confusion Matrix
Rather than collapsing everything into one number, examine all four outcomes:

|  | Predicted Positive | Predicted Negative |
|---|---|---|
| **Actually Positive** | **True Positive (TP)** ✅ | **False Negative (FN)** ❌ |
| **Actually Negative** | **False Positive (FP)** ❌ | **True Negative (TN)** ✅ |

- **TP** — Predicted positive, was positive ("Hit")
- **TN** — Predicted negative, was negative ("Correct rejection")
- **FP** — Predicted positive, was negative ("False alarm" / Type I error)
- **FN** — Predicted negative, was positive ("Miss" / Type II error)

### The Full Metric Family

**Accuracy**
$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$
Use when: classes are balanced and error costs are equal.
Avoid when: data is imbalanced (misleading!).

**Precision** ("When I raise the alarm, am I usually right?")
$$\text{Precision} = \frac{TP}{TP + FP}$$
High precision → few false alarms.
Use when: false positives are costly (spam filter, legal discovery).
Can be gamed: predict positive only when extremely confident (but then you miss many real positives).

**Recall / Sensitivity / True Positive Rate (TPR)** ("Did I find all the needles?")
$$\text{Recall} = \frac{TP}{TP + FN}$$
High recall → few misses.
Use when: false negatives are costly (cancer screening, fraud, tornado warnings).
Can be gamed: predict everything as positive (100% recall, 0 misses — but useless).

**Specificity / True Negative Rate (TNR)** ("How well do I handle negatives?")
$$\text{Specificity} = \frac{TN}{TN + FP}$$
"Recall for the negative class." High specificity → few false alarms on the negative class.

**False Positive Rate (FPR)**
$$\text{FPR} = \frac{FP}{FP + TN} = 1 - \text{Specificity}$$

**False Negative Rate (FNR)**
$$\text{FNR} = \frac{FN}{FN + TP} = 1 - \text{Recall}$$

**F1-Score** ("Balance precision and recall when you can't prioritize either")
$$F_1 = 2 \cdot \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$
F1 is the **harmonic mean** of precision and recall.
Why harmonic? It punishes extreme imbalance — Precision=1.0, Recall=0.0 gives F1=0, not 0.5.
**Blind spot:** Completely ignores TN — can be misleading on severely imbalanced data.

**Critical Success Index (CSI) / Threat Score** (Gilbert, 1884)
$$\text{CSI} = \frac{TP}{TP + FP + FN}$$
Excludes TN entirely. Use when quiet-day correct predictions should not inflate the score (rare events like tornadoes, natural disasters).

**Frequency Bias (Bias Score)**
$$\text{Bias} = \frac{TP + FP}{TP + FN}$$
- Bias = 1.0 → predicts at the right frequency
- Bias > 1.0 → over-predicts (trigger-happy)
- Bias < 1.0 → under-predicts (too conservative)
- **Warning:** Bias = 1.0 does not mean the model is good!

**Matthews Correlation Coefficient (MCC)**
$$\text{MCC} = \frac{TP \cdot TN - FP \cdot FN}{\sqrt{(TP+FP)(TP+FN)(TN+FP)(TN+FN)}}$$
Range: -1 to +1, where +1 = perfect, 0 = random, -1 = perfectly inverted.
Uses all four cells symmetrically. Preferred by biomedical literature for imbalanced datasets because F1 ignores TN.

### The Precision-Recall Tradeoff
Precision and recall **pull in opposite directions** — you cannot increase both simultaneously without a better underlying model:

- **Lowering threshold** → Recall ↑, Precision ↓ (catch more positives, but more false alarms)
- **Raising threshold** → Precision ↑, Recall ↓ (fewer false alarms, but miss more positives)

**Which metric to prioritize:**

| Context | Costly Error | Prioritize |
|---|---|---|
| Cancer screening | Missing a cancer (FN) | Recall |
| Spam filter | Blocking good email (FP) | Precision |
| Tornado warnings | Missing a tornado (FN) | Recall |
| Legal e-discovery | Reviewing non-relevant documents (FP) | Precision |
| Fraud detection | Missing fraud (FN) | Recall |

### ROC Curve & AUC
The **ROC (Receiver Operating Characteristic) curve** sweeps all decision thresholds and plots:
- **Y-axis:** True Positive Rate (Recall) — what fraction of positives we catch
- **X-axis:** False Positive Rate — what fraction of negatives we incorrectly flag

**AUC (Area Under the Curve):**
- AUC = 1.0 → perfect classifier
- AUC = 0.5 → random classifier (diagonal line)
- AUC < 0.5 → worse than random

AUC is **threshold-independent** — it measures overall discriminative ability across all possible thresholds.

### When to Use What

| Metric | Use When | Watch Out For |
|---|---|---|
| Accuracy | Balanced classes | Misleading on imbalanced data |
| Precision | FP are costly | Ignores FN; can be gamed by under-predicting |
| Recall | FN are costly | Can be gamed by predicting all positive |
| Specificity | Negative class matters | Rarely sufficient alone |
| F1-Score | Imbalanced, no strong P/R preference | Ignores TN |
| CSI | Rare events, TN should be excluded | Always ≤ F1 |
| MCC | Imbalanced data, complete picture needed | Complex formula |
| ROC-AUC | Overall model ranking ability | Less interpretable for specific thresholds |

---

## Study Questions — Week 7

1. A model achieves 99% accuracy on a dataset where 99% of samples belong to class 0. Is this a good model? Why or why not?
2. Define True Positive, False Positive, True Negative, and False Negative in plain English. Use a medical diagnosis example.
3. Given TP=80, TN=900, FP=20, FN=0, compute: accuracy, precision, recall, F1-score, and specificity.
4. A researcher claims their model is "unbiased" because its Frequency Bias = 1.0. Is this a valid claim? Why or why not?
5. Precision and recall are in tension. In the context of a cancer screening model, explain which error type (FP or FN) is more costly and which metric should be prioritized.
6. What does the F1-Score measure, and why does it use the harmonic mean instead of the arithmetic mean?
7. Describe the ROC curve in your own words. What does an AUC of 0.5 indicate? What about 0.95?
8. What is the Critical Success Index (CSI) and why was it invented? Why does it exclude True Negatives?
9. You lower a logistic regression's decision threshold from 0.5 to 0.3. How does this affect precision and recall?
10. Your colleague says "I'll just use F1-Score for everything." What is one scenario where this would be problematic, and what metric would be better?

---

---

# Quick Reference — Formulas

## Loss Functions
| Name | Formula | Used for |
|---|---|---|
| MSE | $\frac{1}{n}\sum(y_i - \hat{y}_i)^2$ | Regression |
| Log-Loss | $-\frac{1}{n}\sum[y_i\log\hat{p}_i + (1-y_i)\log(1-\hat{p}_i)]$ | Classification |

## Regularization
| Method | Penalty Added | Effect |
|---|---|---|
| Ridge (L2) | $+\alpha\sum w_j^2$ | Shrinks coefficients |
| Lasso (L1) | $+\alpha\sum |w_j|$ | Shrinks + zeroes coefficients |

## Gradient Descent
$$\theta_{new} = \theta_{old} - \alpha \cdot \nabla L(\theta)$$

## Sigmoid
$$\sigma(z) = \frac{1}{1+e^{-z}}$$

## Confusion Matrix Metrics
| Metric | Formula |
|---|---|
| Accuracy | $(TP+TN)/N$ |
| Precision | $TP/(TP+FP)$ |
| Recall (TPR) | $TP/(TP+FN)$ |
| Specificity (TNR) | $TN/(TN+FP)$ |
| FPR | $FP/(FP+TN)$ |
| F1-Score | $2 \cdot \frac{P \times R}{P+R}$ |
| CSI | $TP/(TP+FP+FN)$ |
| MCC | $\frac{TP\cdot TN - FP \cdot FN}{\sqrt{(TP+FP)(TP+FN)(TN+FP)(TN+FN)}}$ |

---

# Concept Map — How the Weeks Connect

```
Week 1: The ML Workflow
    └── Train/Test Split, Bias-Variance Tradeoff, Data Leakage
         │
Week 2: How Models Learn (Gradient Descent)
    └── Loss functions, gradients, learning rate, convergence
         │
Week 3: Linear Algebra for Data Science
    └── Vectors, matrices, dot products → prediction = w · x + b
         │
Week 4: Multiple Linear Regression & Regularization
    └── Multiple features, overfitting, Ridge/Lasso, feature scaling
         │
Week 5: Cross-Validation & Model Selection
    └── K-fold CV, GridSearchCV, RandomizedSearchCV, Pipelines
         │
Week 6: Logistic Regression & The Sigmoid Function
    └── Classification, sigmoid, log-loss, decision thresholds
         │
Week 7: Evaluating Classification Models
    └── Confusion matrix, precision, recall, F1, ROC-AUC, CSI, MCC
```

**The big through-line:** Every week builds on the same core idea — how do we build models that *generalize* to new data? The workflow (W1) → learning algorithm (W2) → math foundation (W3) → more complex models (W4) → honest evaluation (W5) → new problem type (W6) → honest evaluation of that (W7).

---

*Good luck on the exam! Remember: you are responsible for understanding concepts and being able to explain them — not for memorizing code from scratch. If you can explain it to a classmate without notes, you know it.*