---
title:  "[🇬🇧 English] 3) American Express Default (dimensionality reduction)"
layout: post
---

This Work © 2024 by "ProStepSky.github.io จัดทำโดย S.U."  
is licensed under [CC BY-NC-ND 4.0](http://creativecommons.org/licenses/by-nc-nd/4.0/)  
(อ้างอิงแหล่งที่มา ห้ามนำไปใช้เพื่อการค้า และห้ามดัดแปลง)

<a class='anchor' id='toc'></a>

# Applied Dimensionality Reduction to a 3 GB-Sized American Express Default Dataset – Reducing Computation Time and Boosting Performance

### Table of Contents
[Executive Summary](#bullet1)  
[Principal Component Analysis (PCA)](#bullet2)  
[Linear Discriminant Analysis (LDA)](#bullet3)  
[Models’ performance comparison](#bullet4)  
[Future Scopes](#bullet5)  
[Jupyter Notebooks (in Thai language)](#bullet6)  

Recently, industries have the big data that continuously growing in size.  Thus, to be able to take advantage from the big data efficiently is necessary. Ones of those methods are dimensionality reduction techniques by reduce number of variables in the dataset to reduce the size while maintain the performance. Which could reduce the computation time, and sometimes could even enhance the models’ performance than before applied the dimensionality reduction techniques.

This project has applied dimensionality reduction to a 3 GB-Sized American Express Default Dataset by utilising Principal Component Analysis (PCA) and Linear Discriminant Analysis (LDA) techniques, in order to reduce the number of variables in the dataset. 

Then, compare the performance of those 2 techniques, including Logistic Regression, Decision Tree, Naïve Bayes, and Random Forest in order to compare the performance before and after applied dimensionality reduction techniques.

(This project emphasises at dimensionality reduction techniques only, for Classification Models, please refer to the [Bank Customer Churn Prediction project](https://prostepsky.github.io/2_Customer_Churn_UK) for further information.)


<a class='anchor' id='bullet1'></a>
# Executive Summary
---

1. The application of dimensionality reduction to a 3 GB-Sized American Express Default Dataset could reduce the computation time significantly and enhance the models’ performance even more.
2. Dimensionality reduction by utilising Principal Component Analysis (PCA) to the Random Forest model yields the best results (both reduced computation time and enhanced the performance):
    - Reduced the computation time from 2 hours and 10 minutes to only 54 minutes.
    - Enhanced the performance in F1 Score of the Random Forest model from 79.5% to 80.0%.


<a class='anchor' id='bullet2'></a>
# Principal Component Analysis (PCA)
---

Dimensionality reduction by utilising Principal Component Analysis (PCA) technique will perform linear combination from features. This project has performed PCA at 30 components.

### Cumulative of Variance Ratio (Influence of Old Features to the New Principal Component (pc)) Chart

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/1.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/1.png)

If 30 components were used, there would be cumulative variance up to 95.7%. Therefore, if 30 components were used, they could capture enough information.

### The Influence of Old Features to the New Principal Component (pc) Chart

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/2.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/2.png)

The more influence of features to the principal component, the darker the colours. The red colour indicates the same direction of the influence. (A value is high; another one is also high.) The blue colour indicates the opposite direction of the influence. (A value is high; another one is low.)

**Conclusions:** This project has reduced the dataset’s dimensions by utilising Principal Component Analysis (PCA) from 181 features into 30 components.

<a class='anchor' id='bullet3'></a>
# Linear Discriminant Analysis (LDA)
---

Dimensionality reduction by utilising Linear Discriminant Analysis (LDA) technique will create new feature subspaces from features that would make the different data points from each class separate as far as possible.

### The Distribution of the Data Points and an LDA Component

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/3.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/3.png)

From the chart, found that the Linear Discriminant Analysis algorithm could separate 2 classes quite well.

**Conclusions:** This project has reduced the dataset’s dimensions by utilising Linear Discriminant Analysis (LDA) from 181 features into 1 component.


<a class='anchor' id='bullet4'></a>
# Models’ performance comparison
---

### The Comparison of the Accuracy, F1 Score, Precision, and Recall Metrics

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/4.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/4.png)

Red bars are baseline models, green bars are Principal Component Analysis (PCA) models, blue bars are Linear Discriminant Analysis (LDA) models.

After performed the PCA, found that F1 Score of:
- Tree-based models have better scores: Decision Tree (from 69.7% increase to 70.0%), Random Forest (from 79.5% increase to 80.0%)
- Other models have worse scores: Logistic Regression (from 75.1% decrease to 72.4%), Naïve Bayes (from 70.8% decrease to 51.2%)

After performed the LDA, found that F1 Score of:
- Models that have better scores: Naïve Bayes (from 70.8% increase to 75.2%)
- Models that have worse scores: Logistic Regression (from 75.1% decrease to 74.0%), Decision Tree (from 69.7% decrease to 65.5%), Random Forest (from 79.5% decrease to 65.6%)


### The Comparison of the Algorithms’ Computation Time

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/5.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/5.png)

After performing PCA and LDA techniques, all models utilised less computation time significantly:
- Logistic Regression originally utilised 5 minutes, after performing PCA and LDA the computation times were reduced to less than 1 minute.
- Naïve Bayes both before and after performing PCA and LDA utilised the computation times less than 1 minute. Since the algorithm use the Bayes’ Theorem, so it already performs very fast.
- Decision Tree originally utilised 33 minutes, after performing a PCA the computation time was reduced to 5 minutes, after performing an LDA the computation time was reduced to less than 1 minute.
- Random Forest originally utilised 130 minutes, after performing a PCA the computation time was reduced to 5 minutes, after performing an LDA the computation time was reduced to less than 1 minute.

(All algorithms were performed by using AMD Ryzen 5 PRO 3500U Processor.)

<a class='anchor' id='bullet5'></a>
# Future Scopes
---

1. Understanding the details and meanings of each feature (for instance, the bank employees who could access the bank’s databases) would make it be possible to substitute the missing values. This way could lead to more accuracy of the models. But this dataset is from American Express which has been anonymised in advance, which leads to the impossibility to substitute the missing values.
2. Consider utilising the Hyperparameter Tuning technique as in [Bank Customer Churn Prediction project](https://prostepsky.github.io/2_Customer_Churn_UK) to increase the accuracies of the models.
3. Consider to calculate the correlations to perform the feature selection to sort out the features that have low correlations before performing the dimensionality reduction.
4. Consider using Deep Learning techniques instead of Classification Model to assess whether they improve the accuracy.
5. Consider using another Dimensionality Reduction techniques to assess whether they improve the accuracy.


<a class='anchor' id='bullet6'></a>
# Jupyter Notebooks (in Thai language)
---

**Every file has the detailed explanations for every procedure and correctly follow the data science principles:**

- **For the data preparation,** please refer to [1_Data_Cleaning.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/1_Data_Cleaning.ipynb) for further information.

- **Baseline models before the dimensionality reduction,** please refer to [2_Baseline.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/2_Baseline.ipynb) for further information.

- **Principal Component Analysis (PCA),** please refer to [3_PCA.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/3_PCA.ipynb) for further information.

- **Linear Discriminant Analysis (LDA),** please refer to [4_LDA.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/4_LDA.ipynb) for further information.

- **For the models’ performance comparison,** please refer to [5_Comparison.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/5_Comparison.ipynb) for further information.

---
△ [Back to Top](#toc)
