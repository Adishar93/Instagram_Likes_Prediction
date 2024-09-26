# Machine Learning Project Report

## Methodology

### 1. Data Preprocessing

- **Normalization and Standardization:**
  - Removed outliers in `no_of_comments` where the values were abnormally large (comprising 0.02% of the data). These were found to hinder model performance.
  - Used Gaussian Standardization for the numerical input features (`no_of_comments`, `follower_count_at_t`, `timestamp`) rather than normalization to preserve the distribution of the data.

- **Visualization:**
  - Plotted a pairwise scatterplot for the numerical features (`no_of_comments`, `follower_count_at_t`, `timestamp`) to understand the relationships between them.
  - Observed outliers in `no_of_comments` and removed those from the dataset.

### 2. Model Selection

Four different models were tested:

1. **Convolutional Neural Network (CNN):**
   - Used MobileNetV2 as a feature extractor for image inputs, combined with numerical features fed into a Neural Network.
   - Architecture included 3 fully connected layers with 512, 256, and 128 units respectively.
   - Initially observed poor accuracy when the target (likes) was not standardized. Accuracy improved significantly when `likes` was standardized.

2. **Linear Regression:**
   - Numerical inputs (`no_of_comments`, `follower_count_at_t`, `timestamp`) were fed into a linear regression model.
   - Gave good validation scores but poor test scores, indicating overfitting on the training data.

3. **Support Vector Machine (SVM) Regression:**
   - Numerical inputs were tested using SVM regression.
   - Provided good validation and reasonably good test scores.

4. **K-Nearest Neighbors (KNN):**
   - Applied KNN to the numerical inputs, yielding the best performance overall in terms of test scores.

### 3. Observations

- **Effect of Outliers:**
  - Removing outliers from `no_of_comments` improved the performance of the models, particularly linear regression.

- **Standardization:**
  - Standardizing only the input features provided minimal benefit. However, standardizing both the input features and the output (`likes`) led to significant improvements in accuracy across most models.

## Results

| Model                | Input Parameters                                 | Validation Loss (MSE) | Test Loss (MSE) | All Features Standardized |
|----------------------|--------------------------------------------------|-----------------------|-----------------|---------------------------|
| **Linear Regression** | `no_of_comments`, `follower_count_at_t`, `timestamp` | 0.6697                | 7.2903          | Yes                       |
| **KNN**              | `no_of_comments`, `follower_count_at_t`, `timestamp` | 0.3378                | 0.4201          | Yes                       |
| **SVM Regression**    | `no_of_comments`, `follower_count_at_t`, `timestamp` | 0.4146                | 0.4723          | Yes                       |
| **CNN**              | `no_of_comments`, `follower_count_at_t`, `timestamp`, `image` | 0.7048                | 5.9988          | Yes                       |

## Key Findings:

- **Best Performing Model:** KNN outperformed the other models in terms of test loss (MSE).
- **Importance of Standardization:** Standardizing the target feature (`likes`) significantly enhanced the performance of models such as CNN and SVM regression.
- **Outlier Removal:** The removal of outliers in `no_of_comments` positively impacted model accuracy, particularly for linear regression.
