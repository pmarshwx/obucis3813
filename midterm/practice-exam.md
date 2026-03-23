# CIS 3813 – Advanced Data Science
## Midterm Practice Exam
### Spring 2026 | Dr. Patrick T. Marsh

---

**Name:**

---

**Instructions:**

- This exam must be completed **without** the use of a computer, AI tools, or notes.
- You have **60 minutes** to complete the exam.
- Write all answers clearly in the space provided.
- Show your work where calculations are required — partial credit may be awarded.
- If you are unsure of an answer, write down what you do know — partial credit is possible.

---

**Point Summary:**

| Section | Topic | Points |
|---|---|---|
| Section 1 | Short Answer | 50 |
| Section 2 | Concept Application | 30 |
| Section 3 | Code Analysis | 20 |
| **Total** | | **100** |

---

## Section 1 — Short Answer *(50 points)*

*Answer each question concisely but completely. Most answers should be 2–5 sentences.*

---

**1.** *(3 points)* A model achieves 97% accuracy on a binary classification problem where 97% of samples belong to class 0. Explain why this accuracy score may be misleading and what it likely tells you about the model's behavior.

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**2.** *(3 points)* You are building a cancer screening tool where missing a true cancer case is far more dangerous than a false alarm. Name the metric you should prioritize and explain why it is the right choice for this context.

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**3.** *(3 points)* Describe the key difference between Lasso (L1) and Ridge (L2) regularization in terms of what each does to model coefficients. Which one can perform automatic feature selection, and why?

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**4.** *(3 points)* A data scientist fits a `StandardScaler` on the entire dataset before splitting into train and test sets. Explain the problem this creates and what the correct approach should be.

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**5.** *(3 points)* In 5-Fold Cross-Validation, how many times does each data point appear in a test fold? Briefly explain how the final performance estimate is computed from the five evaluation results.

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**6.** *(4 points)* Explain the difference between **bias** and **variance** in machine learning. In your answer, describe what causes each and what they imply about the model's behavior.

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**7.** *(4 points)* A classmate says: *"My model gets 99% accuracy on the training data and only 61% on the test data. It must be a great model since training accuracy is so high."* Identify the problem with this reasoning and name the phenomenon at work.

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**8.** *(4 points)* Explain in plain English what the **dot product** of a weight vector and a feature vector represents in the context of a linear model making a prediction. Why is this operation central to machine learning?

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**9.** *(5 points)* Explain why **feature scaling** is a critical prerequisite for regularization. What goes wrong if you apply Ridge or Lasso regression to unscaled features?

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**10.** *(4 points)* Describe what the **sigmoid function** does and why it is used in logistic regression instead of a raw linear output. What property of its output makes it suitable for classification?

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**11.** *(5 points)* Explain the **precision-recall tradeoff**. What happens to each metric when you lower the decision threshold of a logistic regression model from 0.5 to 0.2? Why can't you simultaneously maximize both?

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**12.** *(4 points)* What is **K-Fold Cross-Validation** and why is it preferable to a single train/test split for evaluating model performance?

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**13.** *(5 points)* Compare and contrast **GridSearchCV** and **RandomizedSearchCV**. When would you choose one over the other?

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

## Section 2 — Concept Application *(30 points)*

*These questions require deeper reasoning. Be thorough but focused.*

---

**14.** *(8 points)* The confusion matrix below shows the results of a binary classifier predicting whether patients have a rare disease (Positive = disease present).

|  | Predicted Positive | Predicted Negative |
|---|---|---|
| **Actually Positive** | 40 | 10 |
| **Actually Negative** | 30 | 920 |

**(a)** Identify TP, FP, TN, and FN from the table. *(2 points)*

&nbsp;
&nbsp;
&nbsp;

**(b)** Compute **Precision** and **Recall**. Show your work. *(3 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

**(c)** In this medical context, which error type (FP or FN) is more dangerous, and which metric (Precision or Recall) should be prioritized? Briefly justify your answer. *(3 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**15.** *(8 points)* Consider the following scenario:

> A data scientist is building a model to predict house prices using 12 features. She tries standard Linear Regression, Ridge Regression, and Lasso Regression, all on the same scaled dataset. She finds that Lasso zeroes out 5 of the 12 feature coefficients.

**(a)** What does it mean for Lasso to "zero out" a coefficient, and what does it tell you about those 5 features? *(3 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

**(b)** The data scientist wants to compare regularization strengths (alpha values) for Ridge. She tries alpha = 0.001, 1.0, and 1000. Describe what you would expect to happen to the model's coefficients and its train/test performance as alpha increases from very small to very large. *(5 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**16.** *(7 points)* In 1884, Sergeant Finley reported 96.6% accuracy forecasting tornadoes, which was later criticized by Gilbert as a "serious fallacy."

**(a)** What was Gilbert's critique? Why was 96.6% accuracy misleading in this context? *(3 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

**(b)** Gilbert proposed a metric that excluded True Negatives entirely. What is this metric called, and why does excluding True Negatives make sense for rare-event forecasting? *(4 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**17.** *(7 points)* Explain the **Bias-Variance Tradeoff** using the following setup:

> A student is preparing for a comprehensive final exam covering 15 topics. They have a choice: memorize the exact solutions to last year's practice exam (Strategy A), or study the underlying concepts deeply across all topics (Strategy B).

**(a)** Which strategy maps to **high variance** (overfitting) and which maps to **high bias** (underfitting)? Justify your answer. *(4 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

**(b)** What would the "sweet spot" look like for this student, and how does this map back to machine learning? *(3 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

## Section 3 — Code Analysis *(20 points)*

*Read each code snippet carefully and answer the questions. You do not need to write code — only explain, analyze, or identify issues.*

---

**18.** *(6 points)* Examine the following code:

```python
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Ridge
from sklearn.model_selection import train_test_split

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

X_train, X_test, y_train, y_test = train_test_split(
    X_scaled, y, test_size=0.2, random_state=42
)

model = Ridge(alpha=1.0)
model.fit(X_train, y_train)
print(model.score(X_test, y_test))
```

**(a)** Identify the data leakage problem in this code. *(3 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

**(b)** Describe how you would fix it — you do not need to write code, just explain the correct order of operations. *(3 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**19.** *(7 points)* Examine the following code:

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Ridge
from sklearn.model_selection import GridSearchCV

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('model', Ridge())
])

param_grid = {'model__alpha': [0.01, 0.1, 1.0, 10.0, 100.0]}

grid_search = GridSearchCV(pipeline, param_grid, cv=5, scoring='r2')
grid_search.fit(X_train, y_train)

print(grid_search.best_params_)
print(grid_search.score(X_test, y_test))
```

**(a)** What is the purpose of wrapping the scaler and model together in a `Pipeline`? How does this prevent data leakage during cross-validation? *(3 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

**(b)** The `param_grid` uses the key `'model__alpha'` rather than just `'alpha'`. Why does scikit-learn require this naming convention in a Pipeline? *(2 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;

**(c)** `GridSearchCV` is initialized with `cv=5`. Explain exactly what happens when `grid_search.fit(X_train, y_train)` is called — how many total models are trained? *(2 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

**20.** *(7 points)* Examine the following code and output:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report

model = LogisticRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

print(classification_report(y_test, y_pred))
```

```
              precision    recall  f1-score   support

           0       0.97      1.00      0.98       970
           1       0.00      0.00      0.00        30

    accuracy                           0.97      1000
```

**(a)** The model achieves 97% accuracy. Based on the full report, is this model performing well? Explain. *(3 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

**(b)** What does the `support` column tell you about this dataset? How does it explain the model's behavior? *(2 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;

**(c)** Given the output, what metric would you recommend using instead of accuracy to evaluate this model, and why? *(2 points)*

&nbsp;
&nbsp;
&nbsp;
&nbsp;
