#  Leukemia Gene Expression Analysis

This project was developed as part of the **Data Engineering coursework** for the **MSc in Advanced Computer Science program at The University of Manchester**.

This repository contains a Jupyter Notebook that conducts an in-depth analysis of a leukemia gene expression dataset. The primary goal is to preprocess the data, evaluate feature importance using a Decision Tree classifier, visualize decision boundaries for different models, and compare their training time and memory usage.

---

## 📖 Dataset

The dataset used is `genes-leukemia.csv`, which contains gene expression data from leukemia patients. The analysis focuses on a subset of this data where the "Treatment_Response" is not missing, resulting in a working dataset of 15 records.

### Data Pre-processing:
- **Missing Value Handling**: Records with missing "Treatment_Response" values were excluded from the predictive modeling tasks, as this is the target variable.
- **Feature Removal**: Features that had either all the same value or were entirely missing (e.g., 'CLASS', 'Gender', 'Source') were removed to clean the dataset. 'FAB_if_AML' was also removed for simplicity.
- **Encoding**: Categorical features like 'BM_PB' were converted into a numerical format using one-hot encoding to be used in the machine learning models.

---

## ⚙️ Key Analyses Performed

### 1. Feature Importance Analysis (Decision Tree)

A Decision Tree classifier was used to identify the most important features for predicting treatment response.

* **Methodology**:
    * A Decision Tree model was trained on the pre-processed data, and its performance was evaluated using leave-one-out cross-validation, achieving a mean accuracy of **80%**.
    * The feature with the highest importance was identified. The initial model showed that the gene **'U82759'** was the most critical predictor.
    * To demonstrate its importance, this feature was removed, and the tree was retrained. The accuracy dropped significantly from **75% to 25%**, confirming 'U82759' as a highly informative feature.
* **Generalizability**: The first tree (with 'U82759') was deemed more generalizable due to its simpler structure, higher accuracy, and clearer decision boundaries. The second, more complex tree was likely overfitting to the remaining, less predictive features.

### 2. Decision Boundary Visualization

The project visualized and compared the decision boundaries of three different classifiers to understand how they partition the feature space.

* **Models Compared**:
    1.  **ZeroR Classifier**: A baseline model that always predicts the most frequent class, achieving **50% accuracy**. Its decision boundary is a simple horizontal line, showing no feature-based separation.
    2.  **K-Nearest Neighbors (KNN)**: This model classifies data based on the majority class of its nearest neighbors. It achieved a high accuracy of **95%**, with a smooth, non-linear decision boundary that adapts to the local data structure.
    3.  **Decision Tree Classifier**: This model creates axis-parallel splits. It achieved a perfect accuracy of **100%** on this dataset. Its decision boundary is segmented and box-like, which, while effective here, can be prone to overfitting.

### 3. Training Time and Memory Usage Comparison

The scalability of `DecisionTreeClassifier` and `GaussianNB` was analyzed by measuring their training time and memory usage as the dataset size increased.

* **Training Time**:
    * `GaussianNB` maintained a consistently low and near-constant training time due to its linear time complexity O(n).
    * The `DecisionTreeClassifier`'s training time grew significantly and non-linearly, reflecting its O(n log n) complexity. This makes `GaussianNB` more suitable for very large datasets.
* **Memory Usage**:
    * The memory usage of the Decision Tree model showed a steady, near-linear increase with the data size. This is because larger datasets lead to deeper and more complex trees, requiring more memory to store the nodes and split conditions.

---

## 💡 Conclusion

This analysis successfully demonstrates key data engineering and machine learning concepts. It highlights the importance of feature selection, the trade-offs between different classification models in terms of performance and complexity, and the critical considerations of time and memory scalability when working with large datasets.

---

## 🛠️ Technologies Used

* **Python**
* **Pandas**: For data manipulation and pre-processing.
* **Scikit-learn**: For implementing the machine learning models (`DecisionTreeClassifier`, `KNeighborsClassifier`, `GaussianNB`, `DummyClassifier`).
* **Matplotlib**: For data visualization, including plotting decision boundaries and performance graphs.
* **Jupyter Notebook**: As the environment for conducting the analysis.
