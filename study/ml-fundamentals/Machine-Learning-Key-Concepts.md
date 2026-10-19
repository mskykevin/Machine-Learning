# Machine Learning Key Concepts

Key concepts from the **Machine Learning** chapter of *Ace the Data Science Interview*
(Nick Singh & Kevin Huo, 2021), written in my own words as a study and review sheet.

**How to use this file**
- Read a section, then answer its **Self-check** questions out loud without looking.
- When I can explain a concept simply, tick it off in the [checklist](#progress-checklist).
- Put code that tries an idea out in [`practice/`](practice/).

---

## Contents

1. [The math behind ML](#1-the-math-behind-ml)
2. [Model evaluation and selection](#2-model-evaluation-and-selection)
3. [Modeling techniques](#3-modeling-techniques)
4. [The end-to-end ML workflow](#4-the-end-to-end-ml-workflow)
5. [Progress checklist](#progress-checklist)

---

## 1. The math behind ML

### Linear algebra
- **Vectors and matrices:** data is stored as a matrix $X$ (rows = examples, columns = features).
  Most models are matrix operations on $X$.
- **Eigenvalues and eigenvectors:** for a square matrix $A$, an eigenvector $v$ only gets
  stretched (not rotated): $Av = \lambda v$. The eigenvalue $\lambda$ is how much it stretches.
  Used in PCA (eigenvectors of the covariance matrix are the principal components).
- **Matrix decomposition:** splitting a matrix into simpler pieces.
  - **Eigendecomposition:** $A = Q \Lambda Q^{-1}$ (square matrices).
  - **SVD (singular value decomposition):** $X = U \Sigma V^T$. Works on any matrix. Used for
    PCA, recommender systems, and compressing data.
- **Rank and invertibility:** if features are perfectly correlated, $X^TX$ can't be inverted,
  so linear regression has no unique solution (see multicollinearity).

### Gradient descent
- **Goal:** find the parameters $\theta$ that minimize a loss function $L(\theta)$.
- **Update rule:** $\theta \leftarrow \theta - \eta \nabla L(\theta)$, repeated until it stops
  improving. $\eta$ is the **learning rate**.
  - Too high: overshoots and diverges. Too low: very slow.
- **Variants:**
  - **Batch:** uses all data per step. Accurate but slow on big data.
  - **Stochastic (SGD):** one example per step. Fast and noisy; the noise can help escape bad spots.
  - **Mini-batch:** a small batch per step. The usual default in practice.
- **Convex vs. non-convex:** convex losses (linear and logistic regression) have one global
  minimum. Neural networks are non-convex and can get stuck in local minima or saddle points.
- **Improvements:** momentum, adaptive learning rates (Adam, RMSProp), learning-rate schedules.

> **Self-check:** What does the learning rate control? Why is SGD faster than batch gradient
> descent on large data? What is an eigenvector in one sentence?

---

## 2. Model evaluation and selection

### Bias–variance trade-off
- **Bias:** error from wrong assumptions. The model is too simple and **underfits**.
- **Variance:** error from being too sensitive to the training data. The model is too complex
  and **overfits**.
- **Expected error = bias² + variance + irreducible noise.**
- Lowering one usually raises the other. The goal is the sweet spot with the lowest total error.

| | Underfitting (high bias) | Overfitting (high variance) |
|---|---|---|
| Training error | High | Low |
| Test error | High | High |
| Fixes | More features, a more complex model, less regularization | More data, a simpler model, more regularization, dropout, early stopping |

### Model complexity and overfitting
- More parameters and features give more flexibility, and more risk of memorizing noise.
- **Signs of overfitting:** a big gap between training and validation performance.
- **Occam's razor:** prefer the simplest model that performs well enough.

### Regularization
Adds a penalty for large weights to the loss, to reduce overfitting.
- **L1 (Lasso):** penalty $\lambda \sum |w_i|$. Pushes some weights to exactly 0, so it also
  does **feature selection**.
- **L2 (Ridge):** penalty $\lambda \sum w_i^2$. Shrinks all weights smoothly, and handles
  correlated features well.
- **Elastic Net:** a mix of L1 and L2.
- **$\lambda$ (strength):** chosen with cross-validation. Bigger $\lambda$ means a simpler model.
- **Other forms:** dropout and early stopping (neural networks), pruning and max depth (trees).

### Interpretability and explainability
- **Interpretable models:** linear and logistic regression, small decision trees. You can read
  the weights or rules directly.
- **Black-box models:** large ensembles and neural networks. Explain them with **feature
  importance**, **SHAP values**, **LIME**, or **partial dependence plots**.
- Interviews often ask about the **trade-off**: accuracy vs. being able to explain decisions
  (e.g. loans, healthcare).

### Model training
- **Train / validation / test split:** train on one part, tune on validation, and report the
  final score on the test set **once**.
- **k-fold cross-validation:** split the data into $k$ folds, train on $k-1$, validate on the
  remaining fold, and rotate. Average the scores. Good for small data.
  - **Stratified** k-fold keeps the class balance in each fold.
  - **Time series:** use a forward-chaining (rolling) split. Never train on the future.
- **Bootstrapping:** resample the data *with replacement* to estimate uncertainty. It's also
  the basis of bagging and random forests.
- **Hyperparameter tuning:** grid search, random search, or Bayesian optimization, always
  scored on validation data.
- **Data leakage:** information from the test set or the future sneaks into training. This
  gives scores that look great but fail in real life.

### Training times and learning curves
- **Learning curve:** a plot of training and validation error as the training-set size (or
  number of epochs) grows.
  - Both errors high and close together → **high bias**. More data won't help; use a more
    complex model.
  - A big gap that shrinks as data grows → **high variance**. More data helps.
- **Training cost:** think about time and memory complexity (e.g. kNN is cheap to train but
  expensive to predict).

### Model evaluation metrics

**Regression**
- **MSE / RMSE:** squared error; punishes big mistakes. RMSE is in the target's units.
- **MAE:** absolute error; more robust to outliers.
- **$R^2$:** the share of variance explained (1 = perfect, 0 = no better than predicting the mean).

**Classification**
- **Confusion matrix:** true positives (TP), false positives (FP), true negatives (TN), and
  false negatives (FN).
- **Accuracy** = (TP + TN) / total. Misleading when classes are imbalanced.
- **Precision** = TP / (TP + FP): "of the cases I flagged, how many were right?"
- **Recall** = TP / (TP + FN): "of the real positives, how many did I catch?"
- **F1** = the harmonic mean of precision and recall.
- **ROC curve / AUC:** true-positive rate vs. false-positive rate across all thresholds. AUC is
  the chance that a random positive is ranked above a random negative.
- **Precision-recall curve:** better than ROC when positives are rare.
- **Log loss (cross-entropy):** scores predicted *probabilities*, and heavily punishes
  confident wrong answers.
- **Threshold choice** depends on the cost of errors. Fraud and disease screening favor
  recall; spam filtering favors precision.

**Class imbalance**
- Use precision, recall, F1, or PR-AUC instead of accuracy.
- Resample (oversample the minority class, e.g. SMOTE, or undersample the majority), use
  class weights, or move the decision threshold.

> **Self-check:** Explain bias vs. variance to a non-technical friend. When would you use L1
> instead of L2? Why is accuracy a bad metric for fraud detection? Give an example where
> recall matters more than precision.

---

## 3. Modeling techniques

### Linear regression
- **Model:** $y = \beta_0 + \beta_1 x_1 + \dots + \beta_p x_p + \varepsilon$, fit by
  **ordinary least squares (OLS)**, which minimizes the sum of squared residuals.
- **Assumptions:** linearity, independent errors, **homoscedasticity** (constant error
  variance), normally distributed errors, no perfect multicollinearity.
- **Heteroscedasticity:** the error spread changes with $x$. Coefficients stay unbiased but
  standard errors are wrong. Fix it with transforms (e.g. log) or robust standard errors.
- **Multicollinearity:** features strongly correlated with each other. Coefficients become
  unstable and hard to interpret. Detect it with **VIF**; fix it by dropping or combining
  features, or with Ridge/PCA.
- **Confounding variables:** a hidden variable drives both $x$ and $y$, so the coefficient
  shows correlation, not cause.
- **Reading a coefficient:** "holding the other features fixed, a 1-unit increase in $x_j$
  changes $y$ by $\beta_j$ on average."

### Generalized linear models (GLMs)
- Extend linear regression to other kinds of targets through a **link function** and an
  error distribution from the exponential family.
- Examples: **logistic regression** (binary target, logit link) and **Poisson regression**
  (count data, log link).

### Classification

**Logistic regression**
- Predicts a probability: $p = \sigma(w^Tx) = \frac{1}{1 + e^{-w^Tx}}$.
- Trained by minimizing **log loss** (maximum likelihood). Coefficients are changes in
  **log-odds**.
- A linear decision boundary. A fast, interpretable baseline.

**Naive Bayes**
- Applies Bayes' theorem with the "naive" assumption that features are **independent given the
  class**.
- Very fast and works well for text (spam filtering) even when the assumption is false.
- Use **Laplace smoothing** so an unseen word doesn't zero out the probability.

**Support vector machines (SVMs)**
- Find the boundary (hyperplane) with the **largest margin** between classes. The closest
  points are the **support vectors**.
- **Soft margin (C):** allows some mistakes. A smaller C gives a wider margin and more
  regularization.
- **Kernel trick:** RBF or polynomial kernels let SVMs draw non-linear boundaries without
  computing the new features explicitly.

**Decision trees**
- Split the data with yes/no questions, choosing at each step the split that makes groups
  "purest" (**Gini impurity** or **entropy / information gain**; variance for regression).
- Easy to explain and need little data preparation, but **overfit easily**. Control this with
  max depth, minimum samples per leaf, or pruning.

**Random forests (bagging)**
- Many trees, each trained on a **bootstrap sample** and a **random subset of features** at
  each split. Average their votes.
- Averaging lowers variance, so they're much less overfit than one tree. A strong default
  for tabular data.
- **Out-of-bag (OOB) error:** a free validation score from the rows each tree didn't see.

**Boosting**
- Trains trees **one after another**, each one fixing the previous ones' mistakes. This lowers
  bias.
- **AdaBoost:** gives misclassified points more weight.
- **Gradient boosting (XGBoost, LightGBM, CatBoost):** each new tree fits the remaining
  errors (the gradient of the loss).
- Often the most accurate option for tabular data, but more sensitive to hyperparameters
  (learning rate, number of trees, depth) and can overfit.

| | Bagging (random forest) | Boosting (XGBoost) |
|---|---|---|
| How trees are built | In parallel, independently | One after another, each fixing the last |
| Mainly reduces | Variance | Bias |
| Overfitting risk | Low | Higher; needs tuning |

### Dimensionality reduction
- **Curse of dimensionality:** with many features, data gets sparse and distances lose
  meaning, which hurts models like kNN and clustering.
- **PCA (principal component analysis):** finds new axes (principal components) in the
  directions of **maximum variance**. Keep the top components that explain most of the
  variance.
  - **Standardize features first**, because PCA is sensitive to scale.
  - Components are combinations of features, so they're harder to interpret.
- Others to know: t-SNE and UMAP (visualization), LDA (supervised).

### Clustering (unsupervised)

**k-means**
- Pick $k$ centers, assign each point to its nearest center, move each center to the mean
  of its points, and repeat until nothing changes.
- **Choosing k:** the elbow method or the silhouette score.
- **Weaknesses:** assumes round, similar-sized clusters; sensitive to scale, outliers, and
  the starting centers (use **k-means++**).

**Gaussian mixture models (GMMs)**
- Model the data as a mix of several Gaussian (bell-curve) distributions. Fit with the
  **EM (expectation–maximization)** algorithm.
- **Soft clustering:** each point gets a *probability* of belonging to each cluster. Clusters
  can be oval-shaped and different sizes.

### Neural networks
- **Layers of neurons:** each one computes a weighted sum, then applies a non-linear
  **activation function** (ReLU, sigmoid, tanh). Without non-linearity, the whole network
  would just be a linear model.
- **Backpropagation:** the chain rule computes the gradient of the loss for every weight,
  then gradient descent updates them.
- **Common problems:**
  - Vanishing or exploding gradients (helped by ReLU, good initialization, batch norm).
  - Overfitting (helped by dropout, weight decay, early stopping, data augmentation).
- **CNNs (convolutional neural networks):** small sliding filters detect local patterns
  (edges → shapes → objects). Pooling shrinks the image. Used for images.
- **RNNs and LSTMs (recurrent networks):** process sequences step by step, with memory. LSTMs
  and GRUs use gates to remember long-range information. Used for text and time series
  (largely replaced by **transformers** today).
- **Trade-offs:** need lots of data and compute, and are hard to interpret. On small tabular
  data, tree ensembles often win.

### Reinforcement learning
- An **agent** takes **actions** in an **environment**, gets **rewards**, and learns a
  **policy** that maximizes total reward over time.
- **Explore vs. exploit:** try new actions or stick with what works. **Multi-armed bandits**
  are the simple version, used in online experiments.
- Examples: game-playing (AlphaGo), robotics, recommendations.

> **Self-check:** What are the assumptions of linear regression, and what happens when each
> one breaks? Random forest vs. gradient boosting: which reduces variance, and which reduces
> bias? Why standardize before PCA? How does k-means differ from a GMM? Why do neural networks
> need activation functions?

---

## 4. The end-to-end ML workflow

The standard answer to "walk me through how you'd build a model for X":

1. **Clarify the problem:** what's the business goal, how will predictions be used, and what
   are the constraints (latency, interpretability, cost)?
2. **Define the success metric:** pick an ML metric (e.g. AUC) that ties to a business metric
   (e.g. fraud dollars caught).
3. **Understand the data sources:** what's available, how labels are created, and how much
   data there is.
4. **Explore the data (EDA):** distributions, missing values, outliers, class balance,
   correlations.
5. **Clean the data:** handle missing values, duplicates, outliers, and errors.
6. **Engineer features:** encode categories (one-hot, target encoding), scale numbers, create
   features from domain knowledge, and **check for leakage**.
7. **Select a model:** start with a **simple baseline**, then try stronger models and compare
   them fairly.
8. **Train and evaluate:** cross-validation, hyperparameter tuning, error analysis on the
   validation set, and a final check on the test set.
9. **Deploy:** batch or real-time serving, and an A/B test against the current system.
10. **Monitor and iterate:** watch for data and concept drift, and retrain when performance
    drops.

> **Self-check:** Walk through all 10 steps for "predict which customers will cancel their
> subscription next month."

---

## Progress checklist

- [ ] Linear algebra (eigenvectors, SVD)
- [ ] Gradient descent (batch, SGD, mini-batch)
- [ ] Bias–variance trade-off
- [ ] Regularization (L1, L2)
- [ ] Interpretability (SHAP, feature importance)
- [ ] Cross-validation and data leakage
- [ ] Learning curves
- [ ] Regression and classification metrics
- [ ] Class imbalance
- [ ] Linear regression and its assumptions
- [ ] GLMs and logistic regression
- [ ] Naive Bayes
- [ ] SVMs
- [ ] Decision trees, random forests, boosting
- [ ] PCA
- [ ] k-means and GMMs
- [ ] Neural networks, CNNs, RNNs
- [ ] Reinforcement learning
- [ ] End-to-end ML workflow

## Related

- Production-side ML (deployment, monitoring, MLOps): the *Designing Machine Learning Systems*
  chapter folders in [`study/`](../README.md).
- Reference: Nick Singh & Kevin Huo, *Ace the Data Science Interview*, 2021, the Machine
  Learning chapter.
