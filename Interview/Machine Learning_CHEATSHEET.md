# Machine Learning Algorithms Cheatsheet

<details>
<summary><b>Linear Regression</b> — Supervised</summary>

| Property              | Details                                  |
|:----------------------|:-----------------------------------------|
| `Best Use Case`       | Predicting continuous values             |
| `Key Formula`         | Y = b0 + b1X + b2X2 + ...                |
| `Assumptions`         | Linearity, independence                  |
| `Pros`                | Simple, interpretable, fast              |
| `Cons`                | Sensitive to outliers, non-linear limits |
| `When Not to Use`     | Data with strong non-linearity           |
| `Real-World Example`  | House price prediction                   |

</details>

<details>
<summary><b>Logistic Regression</b> — Supervised</summary>

| Property              | Details                         |
|:----------------------|:--------------------------------|
| `Best Use Case`       | Binary classification           |
| `Key Formula`         | P = 1/(1 + e^-(b0 + b1X + ...)) |
| `Assumptions`         | Log-odds linearity              |
| `Pros`                | Probabilistic, interpretable    |
| `Cons`                | Weak with non-linear boundaries |
| `When Not to Use`     | Data is highly non-linear       |
| `Real-World Example`  | Spam detection                  |

</details>

<details>
<summary><b>Decision Tree</b> — Supervised</summary>

| Property              | Details                       |
|:----------------------|:------------------------------|
| `Best Use Case`       | Classification and regression |
| `Key Formula`         | Recursive binary split        |
| `Assumptions`         | None                          |
| `Pros`                | Easy to interpret             |
| `Cons`                | Overfitting, unstable         |
| `When Not to Use`     | Noisy or complex datasets     |
| `Real-World Example`  | Loan default prediction       |

</details>

<details>
<summary><b>Random Forest</b> — Supervised</summary>

| Property              | Details                      |
|:----------------------|:-----------------------------|
| `Best Use Case`       | Ensemble accuracy            |
| `Key Formula`         | Bagging plus averaging trees |
| `Assumptions`         | Tree independence            |
| `Pros`                | High accuracy, robust        |
| `Cons`                | Slower, less interpretable   |
| `When Not to Use`     | Need real-time results       |
| `Real-World Example`  | Fraud detection              |

</details>

<details>
<summary><b>Gradient Boosting</b> — Supervised</summary>

| Property              | Details                        |
|:----------------------|:-------------------------------|
| `Best Use Case`       | High-performance modeling      |
| `Key Formula`         | Additive trees minimizing loss |
| `Assumptions`         | Sequential dependency          |
| `Pros`                | State-of-the-art accuracy      |
| `Cons`                | Overfitting, needs tuning      |
| `When Not to Use`     | When interpretability matters  |
| `Real-World Example`  | Credit scoring                 |

</details>

<details>
<summary><b>SVM</b> — Supervised</summary>

| Property              | Details                            |
|:----------------------|:-----------------------------------|
| `Best Use Case`       | Max-margin classification          |
| `Key Formula`         | Maximize margin using kernel trick |
| `Assumptions`         | Separability, scaling              |
| `Pros`                | Works in high dimensions           |
| `Cons`                | Slow on large data                 |
| `When Not to Use`     | Large noisy datasets               |
| `Real-World Example`  | Facial recognition                 |

</details>

<details>
<summary><b>KNN</b> — Supervised</summary>

| Property              | Details                      |
|:----------------------|:-----------------------------|
| `Best Use Case`       | Few-shot classification      |
| `Key Formula`         | Distance-based majority vote |
| `Assumptions`         | Feature scaling              |
| `Pros`                | Simple, no training phase    |
| `Cons`                | Slow, noise sensitive        |
| `When Not to Use`     | High-dimensional noisy data  |
| `Real-World Example`  | Recommender systems          |

</details>

<details>
<summary><b>Naive Bayes</b> — Supervised</summary>

| Property              | Details                                 |
|:----------------------|:----------------------------------------|
| `Best Use Case`       | Text classification                     |
| `Key Formula`         | Bayes theorem plus feature independence |
| `Assumptions`         | Independent features                    |
| `Pros`                | Fast, good with text data               |
| `Cons`                | Fails with correlated features          |
| `When Not to Use`     | Feature dependency present              |
| `Real-World Example`  | Sentiment analysis                      |

</details>

<details>
<summary><b>K-Means</b> — Unsupervised</summary>

| Property              | Details                         |
|:----------------------|:--------------------------------|
| `Best Use Case`       | Customer segmentation           |
| `Key Formula`         | Minimize intra-cluster distance |
| `Assumptions`         | Spherical, equal clusters       |
| `Pros`                | Fast, easy to implement         |
| `Cons`                | Needs K, sensitive to scale     |
| `When Not to Use`     | Non-spherical data              |
| `Real-World Example`  | Customer segmentation           |

</details>

<details>
<summary><b>Hierarchical Clustering</b> — Unsupervised</summary>

| Property              | Details                      |
|:----------------------|:-----------------------------|
| `Best Use Case`       | Data structure understanding |
| `Key Formula`         | Nested dendrogram            |
| `Assumptions`         | Distance metric              |
| `Pros`                | No need for K, visual        |
| `Cons`                | Memory and compute intensive |
| `When Not to Use`     | Very large datasets          |
| `Real-World Example`  | Gene expression analysis     |

</details>

<details>
<summary><b>PCA</b> — Dimensionality Reduction</summary>

| Property              | Details                           |
|:----------------------|:----------------------------------|
| `Best Use Case`       | Reducing feature dimensionality   |
| `Key Formula`         | Eigenvectors of covariance matrix |
| `Assumptions`         | Large variance important          |
| `Pros`                | Noise reduction, speed-up         |
| `Cons`                | Hard to interpret                 |
| `When Not to Use`     | All features are important        |
| `Real-World Example`  | Image compression                 |

</details>

<details>
<summary><b>Neural Networks (MLP)</b> — Supervised</summary>

| Property              | Details                                 |
|:----------------------|:----------------------------------------|
| `Best Use Case`       | Complex pattern modeling                |
| `Key Formula`         | Weighted sums plus activation functions |
| `Assumptions`         | Enough data, scaling                    |
| `Pros`                | Non-linear learning power               |
| `Cons`                | Needs large data and tuning             |
| `When Not to Use`     | Small data, low compute                 |
| `Real-World Example`  | Image classification                    |

</details>

<details>
<summary><b>CNN</b> — Supervised</summary>

| Property              | Details                         |
|:----------------------|:--------------------------------|
| `Best Use Case`       | Image, video, spatial data      |
| `Key Formula`         | Convolution plus pooling layers |
| `Assumptions`         | Grid-like spatial data          |
| `Pros`                | Excellent for images            |
| `Cons`                | High resource demand            |
| `When Not to Use`     | Sequence or text data           |
| `Real-World Example`  | Self-driving vision             |

</details>

<details>
<summary><b>RNN</b> — Supervised</summary>

| Property              | Details                    |
|:----------------------|:---------------------------|
| `Best Use Case`       | Sequence modeling          |
| `Key Formula`         | Feedback loops over time   |
| `Assumptions`         | Sequential structure       |
| `Pros`                | Time-series and text ready |
| `Cons`                | Vanishing gradient         |
| `When Not to Use`     | Long sequences             |
| `Real-World Example`  | Stock prediction           |

</details>

<details>
<summary><b>Transformer (BERT, GPT)</b> — Supervised / Self-supervised</summary>

| Property              | Details                                    |
|:----------------------|:-------------------------------------------|
| `Best Use Case`       | NLP tasks, chat, translation               |
| `Key Formula`         | Attention mechanism plus position encoding |
| `Assumptions`         | Large training data                        |
| `Pros`                | Long context, fast                         |
| `Cons`                | Heavy compute, large model                 |
| `When Not to Use`     | Small projects                             |
| `Real-World Example`  | ChatGPT, translation tools                 |

</details>

<details>
<summary><b>Autoencoders</b> — Unsupervised</summary>

| Property              | Details                                  |
|:----------------------|:-----------------------------------------|
| `Best Use Case`       | Compression and anomaly detection        |
| `Key Formula`         | Encoder-decoder plus reconstruction loss |
| `Assumptions`         | Symmetric network                        |
| `Pros`                | Effective denoising                      |
| `Cons`                | Can overfit, black-box                   |
| `When Not to Use`     | When no compression needed               |
| `Real-World Example`  | Fraud detection                          |

</details>

<details>
<summary><b>DBSCAN</b> — Unsupervised</summary>

| Property              | Details                        |
|:----------------------|:-------------------------------|
| `Best Use Case`       | Arbitrary shape clustering     |
| `Key Formula`         | Density-based region growing   |
| `Assumptions`         | Cluster density                |
| `Pros`                | Noise tolerant, shape-flexible |
| `Cons`                | Fails on varying density       |
| `When Not to Use`     | Sparse high-dimensional data   |
| `Real-World Example`  | Geo-spatial clustering         |

</details>