# Machine Learning Math Roadmap

Most people think ML requires years of Math. In reality, most ML relies on just three areas.

```mermaid
pie title MMMath Study Distribution (Interview-Oriented)
    "Probability & Statistics" : 50
    "Linear Algebra" : 35
    "Calculus" : 15
```

---

## Recommended Learning Order
Follow this sequence:
1. Probability
2. Statistics
3. Linear Algebra
4. Calculus
5. ML-specific concepts built on top of the math.

---

## Probability (Most Important)
Probability forms the foundation of prediction, uncertainty, and modeling in ML. </br>
Many ML algorithms assume probabilistic interpretations. </br>
**Examples**:
- Naive Bayes 
- Logistic regression 
- Bayesian models 
- Generative models 

### Topics to Learn
Start with these concepts:

<details>
<summary><strong>Core Concepts</strong></summary>

- Random variables (discrete vs continuous)
- Probability distributions 
- Joint, marginal, and conditional probability 
- Bayes' theorem
</details>


<details>
<summary><strong>Statistical Quantities</strong></summary>

- Expectation 
- Variance 
- Covariance 
- Correlation
</details>


<details>
<summary><strong>Important Theorems</strong></summary>

- Law of Large Numbers 
- Central Limit Theorem
</details>

<details>
<summary><strong>Important Distributions</strong></summary>

- Normal distribution 
- Bernoulli distribution 
- Binomial distribution 
- Poisson distribution 
- Exponential distribution 
- Uniform distribution
</details>


<details>
<summary><strong>Advanced (Optional, but Useful)</strong></summary>

- Probability inequalities 
- Markov chains 
- Markov Chain Monte Carlo (MCMC)
</details>

### Best Resources

| Resource                     | Links                                                                                                                                                                      |
|:-----------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Book (Free PDF)`            | [Introduction to Probability — Harvard](https://uni.dcdev.ro/y2s2/ps/Introduction%20to%20Probability%20by%20Joseph%20K.%20Blitzstein,%20Jessica%20Hwang%20(z-lib.org).pdf) |
| `Course`                     | [Harvard edX Probability Course](https://www.edx.org/learn/probability/harvard-university-introduction-to-probability)                                                     |
| `Video (Best intuition)`     | [StatQuest](https://www.youtube.com/c/joshstarmer)                                                                                                                         |                      |                                                                                                                                                                            |
                                                                                                                                                            |
---

## Statistics
Statistics helps us **evaluate models, analyze experiments, and interpret results**.

It is extremely important in:
- ML experiment
- Model Validation
- A/ B Testing
- Product Analytics

### Topics to Learn

<details>
<summary><strong>Descriptive Statistics</strong></summary>

- Mean 
- Median 
- Mode 
- Variance 
- Standard deviation 
- Skewness 
- Kurtosis

</details>



<details>
<summary><strong>Sampling</strong></summary>

- Sampling Techniques
- Sampling Bias
- Population vs Sample
</details>



<details>
<summary><strong>Inferential Statistics</strong></summary>

- Confidence Intervals
- Hypothesis Testing
</details>



<details>
<summary><strong>Statistical Tests</strong></summary>

- `t-test`
- `z-test`
- `Chi-square test`
- `Analysis of Variance (ANOVA)`
</details>




<details>
<summary><strong>Errors in Testing</strong></summary>

- Type I Error
- Type II Error
- Statistical power
</details>


### ML-Relevant Statistical Concepts
These appear frequently in ML system:
* Maximum Likelihood Estimation (MLE)
* Maximum A Posteriori (MAP)
* Bias–variance tradeoff 
* Cross-validation 
* Overfitting vs underfitting 
* Feature importance 
* A/B testing 
* Evaluation metrics

Evaluation Metrics include:
* Accuracy
* Precision
* Recall
* F-1 Score
* ROC-AUC

### Best Resources

| Resource         | Links                                                                                                                   |
|:-----------------|:------------------------------------------------------------------------------------------------------------------------|
| `Website`        | [Probability](https://www.probabilitycourse.com/) </br> Focus particulary on Chapter 8 (classical statistical methods)/ |
| `Video Resource` | [StatQuest](https://www.youtube.com/c/joshstarmer)                                                                      |
| `Statistics`     | [Khan Academy](https://www.khanacademy.org/math/statistics-probability)                                                 |

---

## Linear Algebra
Linear algebra powers almost every ML Model.

Neutral networks are essentially **large matrix operations**.

Understanding linear algebra helps explain:
* Embeddings
* PCA
* Neural Networks
* Dimensionality Reduction

### Topics to Learn

<details>
<summary><strong>Vectors</strong></summary>

- Vector Operations
- Dot Product
- Norms
</details>


<details>
<summary><strong>Matrices</strong></summary>

- Matrix Multiplication
- Matrix Transpose
- Matrix Inverse
</details>



<details>
<summary><strong>Linear Transformation</strong></summary>
</details>



<details>
<summary><strong>Eigen Values and Eigen Vectors</strong></summary>
</details>



<details>
<summary><strong>Projections</strong></summary>
</details>



<details>
<summary><strong>Orthogonality</strong></summary>
</details>

<details>
<summary><strong>Singular Value Decomposition (SVD)</strong></summary>
(Conceptual Understanding is enough)
</details>

### Best Resources

| Topic                                  | Resource                                                                                                                                                                         |
|:---------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Visual Learning (Highly Recommended)` | [ 3Blue1Brown &mdash; Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)                                                       |
| `Course`                               | [Khan Academy Linear Algebra](https://www.khanacademy.org/math/linear-algebra)                                                                                                   |
| `Advanced Course`                      | [UT Austin &mdash; Linear Algebra Foundation to Frontiers](https://www.edx.org/learn/linear-algebra/the-university-of-texas-at-austin-linear-algebra-foundations-to-frontiers)   |

---

## Calculus (Optimization)

Calculus helps explain how ML models learn. </br>
Training neural networks involves optimization using gradients.</br>
Fortunately, you need a subset of calculus.

### Topics to Learn

| Topic                                                                                                                                                                                    | Resource                                                                                                                                                                                         |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Books`                                                                                                                                                                                  | [Mathematical for Machine Learning Book (Free)](https://mml-book.github.io/book/mml-book.pdf) </br> [Multivariable Calculus (Free Textbook)](https://www.whitman.edu/mathematics/multivariable/) |
| `Videos`                                                                                                                                                                                 | [Khan Academy Calculus](https://www.khanacademy.org/math/calculus-1)                                                                                                                             |

---

## ML Concepts Built on This Math

Once you learn the above math, the following ML Concepts become much easier.

<details>
<summary><strong>Regression</strong></summary>

- Linear Regression
- Ordinary Least Square (OLS)
- Regression assumptions
- Multicollinearity
- Residual Analysis
- Heteroskedasticity
</details>


<details>
<summary><strong>Regularization</strong></summary>

- L1 Regularization (Lasso)
- L2 Regularization (Ridge)
</details>


<details>
<summary><strong>Classification</strong></summary>

- Logistic regression
- Decision Boundaries
- Sigmoid Function
</details>


<details>
<summary><strong>Model Evaluation</strong></summary>

- Cross-Validation
- Bias &mdash; variance tradeoff
- Overfitting vs underfitting
</details>


<details>
<summary><strong>ML Metrics</strong></summary>

- Accuracy
- Precision
- Recall
- F1-Recall
- ROC-AUC
</details>


---
## Bonus: Best Series to Understand Neural Networks
This series explains neural networks from scratch.</br>
Highly recommended.

[Andrej Karpathy — Neural Networks: Zero to Hero](https://www.youtube.com/watch?v=VMj-3S1tku0)

---

## Final Advice

The most effective learning strategy is:








