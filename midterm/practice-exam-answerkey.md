# CIS 3813 – Advanced Data Science
## Midterm Practice Exam — Answer Key & Rubric
### Spring 2026 | Dr. Patrick T. Marsh

---

> **Instructor note:** These are model answers. Student responses need not match word-for-word. Award full credit for answers that demonstrate the correct concept, even if phrased differently. Partial credit is encouraged — a student who identifies the right phenomenon but explains it incompletely should receive more than zero.

---

## Section 1 — Short Answer *(50 points)*

---

**1.** *(3 points)* A model achieves 97% accuracy on a binary classification problem where 97% of samples belong to class 0. Explain why this accuracy score may be misleading and what it likely tells you about the model's behavior.

**Model Answer:** When 97% of samples belong to class 0, a model that predicts class 0 for every single input — without learning anything — will achieve 97% accuracy by default. This means high accuracy provides no evidence that the model has learned anything useful. The model is almost certainly failing entirely on class 1 (the minority class), which is typically the class of interest. This is a classic example of the accuracy fallacy on imbalanced datasets.

**Rubric:**
- 2 pts — Correctly identifies that a trivial "always predict class 0" model would match this accuracy
- 1 pt — Notes that accuracy is misleading on imbalanced data / the model may have learned nothing

---

**2.** *(3 points)* You are building a cancer screening tool where missing a true cancer case is far more dangerous than a false alarm. Name the metric you should prioritize and explain why it is the right choice for this context.

**Model Answer:** Recall (also called Sensitivity or True Positive Rate) should be prioritized. Recall measures the fraction of actual positive cases (true cancers) that the model correctly identifies: TP / (TP + FN). In this context, a False Negative — predicting "no cancer" when cancer is present — could be fatal, as the patient receives no treatment. A False Positive leads to additional tests, which is costly and stressful but not life-threatening. Maximizing recall minimizes missed cancers.

**Rubric:**
- 1 pt — Correctly names Recall (or Sensitivity / TPR)
- 1 pt — Correctly explains what recall measures (captures true positives, minimizes FN)
- 1 pt — Connects the choice to the cost of a False Negative in this domain

---

**3.** *(3 points)* Describe the key difference between Lasso (L1) and Ridge (L2) regularization in terms of what each does to model coefficients. Which one can perform automatic feature selection, and why?

**Model Answer:** Both Ridge and Lasso add a penalty to the loss function that discourages large coefficients, but they differ in the shape of the penalty. Ridge (L2) adds the sum of squared coefficients, which shrinks all coefficients toward zero but rarely sets any exactly to zero. Lasso (L1) adds the sum of absolute values of coefficients, which can drive some coefficients to exactly zero — effectively removing those features from the model. Lasso performs automatic feature selection because its diamond-shaped constraint region has corners that sit on the axes; the RSS ellipse is more likely to first touch a corner, producing an exact zero.

**Rubric:**
- 1 pt — Correctly describes Ridge as shrinking toward zero but not reaching it
- 1 pt — Correctly states Lasso can produce exact zeros
- 1 pt — Identifies Lasso as performing feature selection and gives a reason (geometry or penalty shape)

---

**4.** *(3 points)* A data scientist fits a `StandardScaler` on the entire dataset before splitting into train and test sets. Explain the problem this creates and what the correct approach should be.

**Model Answer:** Fitting the scaler on the entire dataset before splitting means the scaler's computed mean and standard deviation are influenced by the test data. When the test set is then scaled using these values, information from the test set has already leaked into the preprocessing step — this is data leakage. The correct approach is to split the data first, then fit the scaler only on the training set, and use those training statistics (mean and std) to transform both the training and test sets.

**Rubric:**
- 1 pt — Identifies this as data leakage
- 1 pt — Explains that the scaler learns test-set statistics, contaminating evaluation
- 1 pt — Describes the correct order: split first, fit scaler on train only, transform both

---

**5.** *(3 points)* In 5-Fold Cross-Validation, how many times does each data point appear in a test fold? Briefly explain how the final performance estimate is computed from the five evaluation results.

**Model Answer:** Each data point appears in a test fold exactly once. The dataset is divided into 5 equal folds; each fold serves as the test set exactly one time while the remaining 4 folds are used for training. After all 5 iterations, you have 5 separate performance scores. The final performance estimate is computed by averaging these 5 scores, often reported along with the standard deviation to convey the variability of the estimate.

**Rubric:**
- 1 pt — Correctly states each point appears in a test fold exactly once
- 1 pt — Explains the rotation: each fold serves as test set once
- 1 pt — States final estimate is the average of the 5 scores

---

**6.** *(4 points)* Explain the difference between **bias** and **variance** in machine learning. In your answer, describe what causes each and what they imply about the model's behavior.

**Model Answer:** Bias measures how far the model's average predictions are from the true values — it reflects systematic error caused by overly simplistic assumptions. A high-bias model underfits the data, missing real patterns (e.g., fitting a straight line to clearly curved data). Variance measures how much the model's predictions change in response to different training sets — it reflects the model's sensitivity to noise in training data. A high-variance model overfits, memorizing the training set and failing to generalize. The bias-variance tradeoff describes the tension between these: simpler models have high bias and low variance; complex models have low bias and high variance.

**Rubric:**
- 1 pt — Correct definition of bias (systematic error, too simple)
- 1 pt — Correct definition of variance (sensitivity to training data, overfitting)
- 1 pt — Connects high bias to underfitting, high variance to overfitting
- 1 pt — Notes the tradeoff / tension between the two

---

**7.** *(4 points)* A classmate says: *"My model gets 99% accuracy on the training data and only 61% on the test data. It must be a great model since training accuracy is so high."* Identify the problem with this reasoning and name the phenomenon at work.

**Model Answer:** The classmate has confused high training accuracy with model quality. A large gap between training and test performance is the hallmark of overfitting (also called high variance). The model has memorized the training data — including its noise — rather than learning generalizable patterns. Training accuracy tells you how well the model fits what it has already seen; test accuracy tells you how well it generalizes to new data. Only test performance is a valid measure of a model's real-world usefulness. A model that overfits is not "great" — it has failed at the fundamental goal of machine learning.

**Rubric:**
- 1 pt — Identifies the problem as overfitting (or high variance)
- 1 pt — Explains that high training accuracy does not imply the model has learned generalizable patterns
- 1 pt — Notes that test accuracy is the meaningful measure
- 1 pt — Explains the gap between train and test performance as the key warning sign

---

**8.** *(4 points)* Explain in plain English what the **dot product** of a weight vector and a feature vector represents in the context of a linear model making a prediction. Why is this operation central to machine learning?

**Model Answer:** The dot product of a weight vector **w** and a feature vector **x** is computed by multiplying each feature value by its corresponding weight and summing all those products. In the context of a linear model, this produces the prediction for a single data sample: ŷ = w · x + b. Each weight reflects how much influence its corresponding feature has on the prediction, and the dot product aggregates all of those influences at once. This operation is central to machine learning because virtually every linear model — including logistic regression — computes predictions this way, and it extends naturally to matrix multiplication for predicting all samples simultaneously.

**Rubric:**
- 1 pt — Correctly describes the computation (multiply pairs, sum)
- 1 pt — Connects the dot product to a model prediction for a single sample
- 1 pt — Explains the role of weights as feature importance/influence
- 1 pt — Notes why this is central (generalizes to all linear models / matrix form)

---

**9.** *(5 points)* Explain why **feature scaling** is a critical prerequisite for regularization. What goes wrong if you apply Ridge or Lasso regression to unscaled features?

**Model Answer:** Regularization penalizes large coefficients. The size of a coefficient is directly tied to the scale of the corresponding feature — a feature measured in dollars (ranging in the hundreds of thousands) will produce a small coefficient, while a feature measured in years (ranging 0–100) will produce a larger coefficient for the same predictive contribution. Without scaling, the regularization penalty is applied unequally: features with large scales are under-penalized, while features with small scales are over-penalized. This means regularization is not comparing features fairly. After scaling (e.g., with StandardScaler), all features are on the same scale, so the penalty treats each coefficient equally and the regularization is meaningful. Failing to scale can also cause important features to be incorrectly zeroed out by Lasso, or cause Ridge to leave a dominant unscaled feature unpenalized.

**Rubric:**
- 2 pts — Explains that coefficient size depends on feature scale, making raw penalty unfair
- 2 pts — Describes the consequence: over/under-penalization of certain features
- 1 pt — States that scaling puts all features on equal footing so the penalty is fair

---

**10.** *(4 points)* Describe what the **sigmoid function** does and why it is used in logistic regression instead of a raw linear output. What property of its output makes it suitable for classification?

**Model Answer:** The sigmoid function takes any real number as input and maps it to a value between 0 and 1: σ(z) = 1 / (1 + e^(-z)). When z is large and positive, the output approaches 1; when z is large and negative, the output approaches 0; and at z = 0 the output is exactly 0.5. This makes the sigmoid suitable for classification because its output can be interpreted as a probability of belonging to the positive class. A raw linear output can produce values outside [0, 1], which cannot be meaningfully interpreted as a probability. The sigmoid's S-shaped curve also provides a smooth, differentiable transition between the two classes, allowing gradient descent to be used for optimization.

**Rubric:**
- 1 pt — Correctly states the sigmoid maps any real input to (0, 1)
- 1 pt — Correctly states that σ(0) = 0.5 and describes the behavior at extremes
- 1 pt — Explains why linear output fails (can exceed [0, 1])
- 1 pt — Notes output is interpreted as a probability / enables probabilistic classification

---

**11.** *(5 points)* Explain the **precision-recall tradeoff**. What happens to each metric when you lower the decision threshold of a logistic regression model from 0.5 to 0.2? Why can't you simultaneously maximize both?

**Model Answer:** Precision measures the fraction of positive predictions that are correct (TP / (TP + FP)); recall measures the fraction of actual positives that were detected (TP / (TP + FN)). When you lower the decision threshold from 0.5 to 0.2, the model predicts "positive" for more samples — including samples it was previously uncertain about. This increases recall because fewer true positives are missed, but it decreases precision because more false positives are introduced. The two metrics pull in opposite directions because the positive and negative class distributions overlap in feature space. Any threshold cuts through that overlap; lowering the threshold sweeps up more true positives but inevitably includes more false positives as well. There is no threshold that simultaneously maximizes both — only a better underlying model can improve both at once.

**Rubric:**
- 1 pt — Correct definitions of precision and recall
- 1 pt — Correctly states lowering threshold increases recall
- 1 pt — Correctly states lowering threshold decreases precision
- 1 pt — Explains why (more positives predicted → more FP introduced)
- 1 pt — Explains the fundamental reason: class distributions overlap; no threshold eliminates both error types

---

**12.** *(4 points)* What is **K-Fold Cross-Validation** and why is it preferable to a single train/test split for evaluating model performance?

**Model Answer:** K-Fold Cross-Validation divides the dataset into K equal parts (folds). The model is trained K times, each time using K-1 folds for training and the remaining fold for evaluation. The results are averaged to produce a final performance estimate. This is preferable to a single train/test split because a single split produces a score that is heavily dependent on which samples happen to end up in the test set — a lucky or unlucky split can make the same model look dramatically better or worse. K-Fold uses every sample for testing exactly once, reducing this variability and giving a more stable, reliable estimate of how the model will perform on unseen data.

**Rubric:**
- 1 pt — Correctly describes the K-Fold process (divide into K folds, rotate test fold)
- 1 pt — States that results are averaged
- 1 pt — Identifies the problem with single splits (high variability / luck-dependent)
- 1 pt — Explains that K-Fold gives a more stable and reliable estimate

---

**13.** *(5 points)* Compare and contrast **GridSearchCV** and **RandomizedSearchCV**. When would you choose one over the other?

**Model Answer:** Both GridSearchCV and RandomizedSearchCV are tools for hyperparameter tuning that use cross-validation to evaluate each combination. GridSearchCV performs an exhaustive search — it evaluates every combination in a specified parameter grid. This guarantees finding the best combination within the grid but becomes computationally expensive as the number of hyperparameters and candidate values grows (the curse of dimensionality in search spaces). RandomizedSearchCV instead randomly samples a fixed number of combinations from the parameter space (set by `n_iter`), making it much faster. It does not guarantee finding the optimal combination, but in practice often finds near-optimal results in a fraction of the time. Choose GridSearchCV when the search space is small and exhaustive evaluation is feasible. Choose RandomizedSearchCV when the search space is large, when hyperparameters are continuous, or when compute time is a constraint.

**Rubric:**
- 1 pt — Correctly states GridSearchCV is exhaustive / evaluates all combinations
- 1 pt — Correctly states RandomizedSearchCV samples randomly for a fixed number of iterations
- 1 pt — Notes GridSearchCV guarantees the best in-grid result; RandomizedSearchCV does not
- 1 pt — Notes RandomizedSearchCV is faster / more efficient for large spaces
- 1 pt — Gives a reasonable recommendation for when to use each

---

## Section 2 — Concept Application *(30 points)*

---

**14.** *(8 points)*

|  | Predicted Positive | Predicted Negative |
|---|---|---|
| **Actually Positive** | 40 | 10 |
| **Actually Negative** | 30 | 920 |

**(a)** Identify TP, FP, TN, and FN. *(2 points)*

**Model Answer:**
- TP = 40 (predicted positive, actually positive)
- FP = 30 (predicted positive, actually negative)
- TN = 920 (predicted negative, actually negative)
- FN = 10 (predicted negative, actually positive)

**Rubric:** 1 pt for all four correctly identified; 0.5 pt if two or three are correct.

---

**(b)** Compute Precision and Recall. *(3 points)*

**Model Answer:**

$$\text{Precision} = \frac{TP}{TP + FP} = \frac{40}{40 + 30} = \frac{40}{70} \approx 0.571$$

$$\text{Recall} = \frac{TP}{TP + FN} = \frac{40}{40 + 10} = \frac{40}{50} = 0.800$$

**Rubric:** 1 pt for correct formula for each metric; 1 pt for correct arithmetic (award partial credit if formula is right but arithmetic is off).

---

**(c)** Which error type is more dangerous and which metric should be prioritized? *(3 points)*

**Model Answer:** In a medical context predicting a rare disease, a False Negative (FN) is more dangerous — it means a patient with the disease is told they are healthy and receives no treatment. A False Positive leads to unnecessary follow-up testing, which causes anxiety and cost but is not life-threatening. Therefore, Recall should be prioritized, as it directly measures how well the model captures true positive cases and minimizes False Negatives. With a recall of 0.80, the model is still missing 20% of actual disease cases (10 out of 50), which may warrant lowering the decision threshold to catch more.

**Rubric:**
- 1 pt — Correctly identifies FN as the more dangerous error
- 1 pt — Correctly names Recall as the metric to prioritize
- 1 pt — Justifies the choice with a clear explanation tied to the domain

---

**15.** *(8 points)*

**(a)** What does it mean for Lasso to "zero out" a coefficient? *(3 points)*

**Model Answer:** When Lasso sets a coefficient exactly to zero, it means that feature is completely excluded from the model — its value has no influence on the prediction whatsoever. Lasso does this because its L1 penalty (sum of absolute values) creates a diamond-shaped constraint region with corners on the axes; the optimization solution frequently falls at a corner where one or more coefficients are zero. For those 5 zeroed-out features, Lasso has determined that including them — after applying the regularization penalty — does not improve the model enough to justify their complexity cost. They may be irrelevant, redundant with other features, or too weakly correlated with the target.

**Rubric:**
- 1 pt — Correctly states the feature is excluded from the model / has no predictive contribution
- 1 pt — Explains why Lasso does this (L1 geometry / diamond constraint)
- 1 pt — Interprets what zero coefficients imply about those features (irrelevant/redundant)

---

**(b)** Describe what happens to coefficients and train/test performance as alpha increases. *(5 points)*

**Model Answer:**

- **Very small alpha (≈ 0.001):** Penalty is negligible, model behaves nearly like standard OLS linear regression. Coefficients can be large. Training error is low (possibly overfitting), test error may be higher than ideal.
- **Moderate alpha (≈ 1.0):** Coefficients are meaningfully shrunk toward zero. The model is more regularized, which should reduce overfitting. Training error increases slightly, but test error typically decreases — this is often near the optimal zone.
- **Very large alpha (≈ 1000):** All coefficients are shrunk so aggressively toward zero that the model essentially predicts the mean of y regardless of the features. Both training and test error increase significantly — the model is now underfitting (high bias).

The goal of cross-validation is to find the alpha where test error is minimized — the balance between underfitting and overfitting.

**Rubric:**
- 1 pt — Correctly describes near-zero alpha as close to OLS with potential overfitting
- 1 pt — Correctly describes moderate alpha as reducing overfitting
- 1 pt — Correctly describes very large alpha as causing underfitting / driving all coefficients to zero
- 1 pt — Describes the general pattern of training error increasing and test error having a U-shape as alpha grows
- 1 pt — States the goal is to find the alpha where test error is minimized

---

**16.** *(7 points)*

**(a)** What was Gilbert's critique of Finley's 96.6% accuracy? *(3 points)*

**Model Answer:** Gilbert pointed out that the overwhelming majority of Finley's 2,803 forecast occasions involved no tornado. Because tornadoes are extremely rare, a trivially simple strategy — predict "no tornado" every single time — would have achieved approximately 98.2% accuracy, which is actually higher than Finley's 96.6%. This revealed that Finley's model was not performing above a naive baseline. The apparent accuracy was inflated almost entirely by the model correctly identifying the abundant "no tornado" days (True Negatives), not by any genuine skill at detecting tornadoes. Accuracy is dominated by the majority class when data is highly imbalanced.

**Rubric:**
- 1 pt — Notes that always predicting "no tornado" achieves higher accuracy
- 1 pt — Explains the accuracy was driven by the abundance of true negatives (quiet days)
- 1 pt — Concludes that accuracy is misleading for rare-event prediction

---

**(b)** What is the metric Gilbert proposed, and why does it exclude True Negatives? *(4 points)*

**Model Answer:** Gilbert proposed what is now called the **Critical Success Index (CSI)**, also known as the Threat Score:

$$\text{CSI} = \frac{TP}{TP + FP + FN}$$

CSI excludes True Negatives entirely because in rare-event forecasting, the number of quiet days (TN) is enormous and completely dominates any metric that includes it. Including TN makes even a useless model look good. CSI focuses only on the events that "mattered" — days when a tornado was forecast (TP + FP) and days when a tornado was missed (FN). Correct quiet-day forecasts simply don't count. This makes CSI a fair measure of how well the model handles the rare event itself, without being inflated by the vast number of easy non-event days.

**Rubric:**
- 1 pt — Correctly names the metric (CSI / Threat Score)
- 1 pt — Writes or correctly describes the formula (TP / (TP + FP + FN))
- 2 pts — Explains why TN should be excluded (vast number of quiet days would dominate / inflate any metric that includes them; only the "events that matter" should count)

---

**17.** *(7 points)*

**(a)** Which strategy maps to high variance and which to high bias? *(4 points)*

**Model Answer:** **Strategy A** (memorizing exact solutions to last year's practice exam) maps to **high variance (overfitting)**. This student has essentially "trained" on one specific dataset (last year's exam) and memorized it perfectly. They will perform very well if the new exam is nearly identical to last year's, but will struggle badly if the questions are worded differently or test slightly different aspects of the material. The model has learned noise (the specific phrasing and problems) rather than signal (the underlying concepts).

**Strategy B** (studying underlying concepts deeply) maps to **high bias (underfitting)** only if taken to an extreme — but more likely represents the sweet spot. However, if a student only skims concepts very superficially without working through any examples, they may have such a simplified mental model that they can't solve specific problems — this would be high bias. The key insight is that Strategy A overfits to training data and Strategy B generalizes better.

**Rubric:**
- 2 pts — Correctly identifies Strategy A as high variance / overfitting with justification
- 2 pts — Correctly identifies Strategy B as the generalizing approach (or high bias if oversimplified) with justification

*Note: Accept answers that frame Strategy B as "low bias, low variance" or "the sweet spot" with good reasoning.*

---

**(b)** What does the "sweet spot" look like, and how does it map to machine learning? *(3 points)*

**Model Answer:** The sweet spot for this student would be someone who thoroughly understands the core concepts (so they can handle novel question phrasings) and has practiced enough specific problems to know how to apply those concepts concretely. They haven't memorized exact answers, but they can reconstruct solutions from understanding. In machine learning terms, this corresponds to a model with moderate complexity — complex enough to capture the true signal in the data (low bias) but not so complex that it memorizes training-set noise (low variance). This is the model that minimizes total error on unseen data, achieved through techniques like regularization and cross-validation.

**Rubric:**
- 1 pt — Describes a student who understands concepts AND can apply them specifically
- 1 pt — Maps this to a model that captures true patterns without memorizing noise
- 1 pt — Mentions regularization, cross-validation, or another technique that achieves the sweet spot

---

## Section 3 — Code Analysis *(20 points)*

---

**18.** *(6 points)*

```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

X_train, X_test, y_train, y_test = train_test_split(
    X_scaled, y, test_size=0.2, random_state=42
)
```

**(a)** Identify the data leakage problem. *(3 points)*

**Model Answer:** The `StandardScaler` is fit on the entire dataset `X` before the train/test split. This means the scaler's mean and standard deviation are computed using both training and test samples. When the test set is later evaluated, it has already influenced the preprocessing — the scaler has "seen" it. This is data leakage: information from the test set has contaminated the training pipeline, leading to an optimistically biased estimate of test performance. The correct order is to split first, then fit the scaler only on `X_train`.

**Rubric:**
- 1 pt — Identifies the specific problem (scaler fit on entire dataset before split)
- 1 pt — Explains what leakage means here (test data influences preprocessing)
- 1 pt — States the consequence (overly optimistic test score)

---

**(b)** Describe how to fix it. *(3 points)*

**Model Answer:** The correct order of operations is:
1. Perform the train/test split first on the raw, unscaled data.
2. Fit the `StandardScaler` using only `X_train` (call `.fit()` or `.fit_transform()` on training data only).
3. Use the fitted scaler to transform `X_train` and separately transform `X_test` (call `.transform()` — not `.fit_transform()` — on the test set).

This ensures the scaler's statistics are learned only from training data, and the test set is scaled using those same training statistics without contributing to them.

**Rubric:**
- 1 pt — States split must happen before scaling
- 1 pt — States scaler must be fit only on training data
- 1 pt — States test data must be transformed (not fit-transformed) using training statistics

---

**19.** *(7 points)*

**(a)** What is the purpose of a Pipeline and how does it prevent leakage? *(3 points)*

**Model Answer:** A Pipeline chains preprocessing and modeling steps into a single object that behaves like a model. When the Pipeline is used inside cross-validation, scikit-learn ensures that for each fold, the scaler is fit only on the training portion of that fold — never on the validation fold. Without a Pipeline, if you scaled the data before cross-validation, the scaler would have been fit on the full training set including what will become the validation fold for each iteration, leaking information. The Pipeline makes the correct behavior automatic and eliminates this risk.

**Rubric:**
- 1 pt — Describes Pipeline as chaining preprocessing and modeling into one object
- 1 pt — Explains that the scaler is re-fit on training folds only during CV
- 1 pt — Explains what would go wrong without the Pipeline (scaler sees validation data)

---

**(b)** Why does the param_grid use `'model__alpha'`? *(2 points)*

**Model Answer:** Inside a Pipeline, each step is given a name (in this case `'scaler'` and `'model'`). To specify a hyperparameter of a specific step, scikit-learn uses the convention `stepname__parametername` with a double underscore. So `'model__alpha'` means "the `alpha` parameter of the step named `model`." This naming convention is necessary to distinguish between hyperparameters that might share names across different steps in the Pipeline.

**Rubric:**
- 1 pt — Explains the double-underscore convention references the named step
- 1 pt — Notes it disambiguates between parameters of different steps

---

**(c)** How many total models are trained when `grid_search.fit()` is called? *(2 points)*

**Model Answer:** The parameter grid has 5 candidate alpha values, and cross-validation uses 5 folds. For each candidate alpha, the model is trained 5 times (once per fold). Therefore, the total number of models trained is 5 × 5 = **25 models**.

**Rubric:**
- 1 pt — Correctly identifies the calculation as (number of alpha values) × (number of CV folds)
- 1 pt — Arrives at the correct answer of 25

---

**20.** *(7 points)*

```
              precision    recall  f1-score   support

           0       0.97      1.00      0.98       970
           1       0.00      0.00      0.00        30

    accuracy                           0.97      1000
```

**(a)** Is the model performing well? *(3 points)*

**Model Answer:** No — the model is performing terribly on the class that matters most. Despite 97% overall accuracy, the model has precision and recall of 0.00 for class 1, meaning it never predicts class 1 at all. Every actual class 1 sample is misclassified as class 0. The model has learned to predict class 0 for every input, which trivially achieves high accuracy on an imbalanced dataset (970 of 1,000 samples are class 0). The 97% accuracy is completely misleading.

**Rubric:**
- 1 pt — States the model is not performing well / accuracy is misleading
- 1 pt — Notes that precision and recall for class 1 are 0.00 — the model never predicts class 1
- 1 pt — Explains why: the model likely always predicts class 0, and 97% of samples are class 0

---

**(b)** What does the `support` column tell you? *(2 points)*

**Model Answer:** The `support` column shows the number of actual instances of each class in the test set: 970 samples belong to class 0 and only 30 to class 1. This severe imbalance (97%/3%) explains the model's behavior — the model has learned that always predicting class 0 minimizes loss on the training data, since class 0 is so dominant. The model is exploiting the class imbalance rather than actually learning to distinguish the two classes.

**Rubric:**
- 1 pt — Correctly interprets support as the number of actual instances of each class
- 1 pt — Connects the imbalance (970 vs. 30) to the model's failure to learn class 1

---

**(c)** What metric would you recommend instead? *(2 points)*

**Model Answer:** Any of the following are acceptable with a reasonable justification: **Recall** (if missing class 1 is costly), **F1-Score** (balances precision and recall for imbalanced data), **ROC-AUC** (evaluates discriminative ability across all thresholds), or **MCC** (uses all four confusion matrix cells, robust to imbalance). Accuracy should be avoided entirely. The best answer identifies the business context as the deciding factor — e.g., if class 1 represents fraud or disease, Recall or F1 are most appropriate.

**Rubric:**
- 1 pt — Names a valid alternative metric (Recall, F1, ROC-AUC, MCC, Precision-Recall AUC)
- 1 pt — Provides a justification tied to the imbalanced nature of the dataset or the cost of misclassifying class 1

---

*End of Answer Key*