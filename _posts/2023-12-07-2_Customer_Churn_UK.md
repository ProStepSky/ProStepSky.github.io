---
title:  "[🇬🇧 English] Bank customer churn (Classification, Random Forest)"
layout: post
---

<a class='anchor' id='toc'></a>

# Bank Customer Churn Prediction by Developing Classification and Random Forest Models

### สารบัญ  
[Executive Summary](#bullet1)  
[Models’ Performance Comparison](#bullet2)  
[Exploratory Data Analysis to obtain Insights](#bullet3)  
[Future Scopes](#bullet4)  
[Jupyter Notebooks](#bullet5)  

In the competition of the business world like today, to maintain profits for the company, maintaining the customers base is very important. One thing that could indicate the success of the company is the ability to predict in advance if the customers are going to churn. So, the company will implement the proactive measures action to maintain or attract customers before they will churn from the company.

Besides, the exploratory data analysis could gain the insights which helps the company to acknowledge how to improve their products and services.

This project has developed total 6 classification models, Including Logistic Regression, K-Nearest Neighbours (KNN), Support Vector Machine (SVM), Naïve Bayes, Decision Tree, and Random Forest in order to predict the customers who likely to churn from the bank; by using the following factors: credit score, age, tenure, account balance, number of products that a customer use, has a credit card or not, still active or not, estimated salary, gender, and geography (French, Germany, Spain).

Then, compare the performance of the 6 models, by evaluate the Accuracy, F1 Score, Precision, and Recall metrics.


<a class='anchor' id='bullet1'></a>
# Executive Summary
---

1. This project has done the Exploratory Data Analysis (EDA) and gained the following insights in brief:
    - The customers from Germany have more average account balances than the customers from France and Spain approximately 2 times. Although the customers from the 3 countries including France, Germany, and Spain, would have the similar average salary. (Which according to the fact that Germans like to save money because in the past they used to encounter economic hardship.)
    - The high salary customers are not always necessary to have a lot of money in their saving accounts.
    - There are churned customers in every salary range and in every account balance range.
    - Customers’ ages have no effect on salary. (The customers from any age could have any salary range.)
    - Most of the churned customers would gather around higher ages.
    - Female customers are more likely to churn from the bank than male customers.
    - The customers from Germany are more likely to churn from the bank than the customers from Spain and France.
    - 50% of customers are between 32-43 years old.
    - 50% of churned customers are between 38-50 years old.
    - Most customers from all countries (more than 95%) use the bank products 1-2 products.
    - The more bank products customers use, the more likelihood they would churn. This is contrasted to the ‘Feeling’ that if someone use many bank products, they are ‘not likely’ to churn from the bank, but the information provided are contrasted. Studying from other contexts can provide more understanding.
2. This is an imbalanced dataset because this dataset contains 20% of churned customers and 80% of non-churned customers. Therefore, prediction of churn customers will be harder than prediction of non-churn customers.



<a class='anchor' id='bullet2'></a>
# Models’ Performance Comparison
---

### The Comparison of the Accuracy, F1 Score, Precision, and Recall Metrics

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/1.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/1.png)

**For this dataset:**

- Recall is more important than Precision, because Recall considers False Negatives.

    - Recall is the number of correctly predicted as churn from all the truth that churn.
    - False Negative is important, it means predicted as non-churn, but the fact is churn.
        - Wrong prediction like this, the bank would not implement the measure to maintain or attract customers until they could churn from the bank.
    - It’s important to try to reduce False Negatives and try to increase True Positives.

**Meanwhile:**

- Precision is also important, because Precision considers False Negatives.
    - Precision is the number of correctly predicted as churn from every predicted as churn.
    - False Positive means predicted as churn, but the fact is non-churn.
        Wrong prediction like this, the bank would waste resources to maintain or attract customers who would not churn from the bank, and might cause an unnecessary annoyance.


**Therefore:**

-	For this dataset, the Decision Tree and Random Forest models give the best prediction, because both Recall and Precision are high. And when consider the F1 Score (the balance between Recall and Precision), they also have the highest F1 Score.
    - The F1 Score of both Decision Tree and Random Forest equal 60% approximately.
    - Decision Tree has higher Recall than Random Forest at 5% approximately.
    - Random Forest has higher Precision than Decision Tree at 3% approximately.


<a class='anchor' id='bullet3'></a>
# Exploratory Data Analysis to Obtain Insights
---
This project has done the Exploratory Data Analysis (EDA) and gained the insights which can discuss in the following:

### 1) The Ratio of Churned Customers and Non-Churned Customers

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/2.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/2.png)

This is an imbalanced dataset because this dataset contains 20% of churned customers and 80% of non-churned customers. Therefore, prediction of churn customers will be harder than prediction of non-churn customers.

Solving the problem by collecting more data of churned customers is unlikely to be possible. Because, generally, the customers are unlikely to churn.


### 2) The Correlation Analysis Between Factors

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/3.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/3.png)

Most variables don’t have any correlations:
- Credit Score: No correlations were found.
- Tenure: No correlations were found.
- Has a credit card or not: No correlations were found.
- Estimated salary: No correlations were found.

Variables that have correlations:
- The higher age, the higher likelihood to churn from a bank. (A correlation is +0.36 which is a moderate relationship.)
- The higher number of products that a customer use, the higher likelihood of the low account balance. (A correlation is -0.31 which is a moderate relationship.)
- The customers who still active have higher likelihood to not churn from a bank. (A correlation is -0.14 which is a weak relationship.)
- The customers from France are likely to have the lower account balance. (A correlation is -0.23 which is a weak relationship.)
- The customers from Germany are likely to have the higher account balance. (A correlation is +0.40 which is a moderate relationship.)
- The customers from Spain are likely to have the lower account balance. (A correlation is -0.14 which is a weak relationship.)


### 3) The Number of Customers from Each Country

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/4.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/4.png)

Found that approximately half of the customers are from France. The remains are from Spain and German, approximately fifty-fifty.

#### The number of customers from each country (separated by gender)
![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/5.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/5.png)

Found that every country has female customers fewer than male customers.

### 4) Account Balances versus Estimated Salaries

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/6.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/6.png)

Found that the high salary customers are not always necessary to have a lot of money in their saving accounts.

Found that there are churned customers in every salary range and in every account balance range.


### 5) Ages versus Estimated Salaries

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/7.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/7.png)

Found that customers’ ages have no effect on salary. (The customers from any age could have any salary range.)

Found that most of the churned customers (orange points) would gather around higher ages.

<a class='anchor' id='bullet_a'></a>
### 6) Average Account Balances (Separated by Country)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/8.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/8.png)

From the chart, found that:
- The customers from France have the average account balances approximately 62,000 EUR.
- The customers from Germany have the average account balances approximately 120,000 EUR, which more than the customers from France and Spain approximately 2 times.
- The customers from Spain have the average account balances approximately 61,000 EUR

Which corresponds to the correlation analysis before, which is the customers from Germany have more average account balances than the customers from France and Spain.

<a class='anchor' id='bullet_b'></a>
### 7) Average Salaries (Separated by Country)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/9.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/9.png)

From the chart, found that the customers from the 3 countries (France, Germany, Spain) have the similar average salary.

From the information, both [average account balance (separated by country)](#bullet_a) and [average salary (separated by country)](#bullet_b) above informs that:
-	The customers from Germany have more average account balances than the customers from France and Spain, approximately 2 times; although the customers from the 3 countries (France, Germany, Spain) would have the similar average salaries.
-	Which according to the fact that Germans like to save money because in the past they used to encounter economic hardship that is inflation. And this behaviour has been passed down through generations until these days.


### 8) Churned Customers

#### Churned Customers (Separated by Gender)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/10.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/10.png)

Found that female customers are more likely to churn from the bank than male customers.

#### Churned Customers (Separated by Country)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/11.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/11.png)

Percentage of churned customers per all customers of that country:
- Approximately 16% of customers from France are churned from the bank.
- Approximately 32% of customers from Germany are churned from the bank.
- Approximately 16% of customers from Spain are churned from the bank.
From the above information, found that the customers from Germany are more likely to churn from the bank than the customers from Spain and France.


### 9) Age Distribution

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/12.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/12.png)

Found that 50% of customers are between 32-43 years old.

#### Age Distribution of Churned Customers

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/13.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/13.png)

Found that 50% of churned customers are between 38-50 years old.

From the conclusions gained from the above charts
- 50% of customers are between 32-43 years old.
- 50% of churned customers are between 38-50 years old.

Are corresponds to the correlation analysis which is the higher age, the higher likelihood to churn from a bank. (A correlation is +0.36 which is a moderate relationship.)


### 10) Customers Grouped by Number of Products

#### The Number of Both Churned and Non-Churned Customers (Separated by Number of Products)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/14.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/14.png)

Found that most customers from all countries (more than 95%) use the bank products 1-2 products.

#### The Number of Churned Customers (Separated by Number of Products)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/15.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/15.png)

#### The Proportion of Churned Customers (Separated by Number of Products)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/16.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/16.png)

#### From the above information, found that

For all countries, **the customers who use 4 products**, 100% of them are churned.
- Churned customers: France (28/28 customers), Germany (23/23 customers), Spain (7/7 customers)

For all countries, **the customers who use 3 products**, approximately 77% - 89% of them are churned.
- Churned customers: France (78/96 customers), Germany (80/90 customers), Spain (48/62 customers)

For all countries, **the customers who use 2 products**, approximately 5% - 12% of them are churned.
- Churned customers: France (126/2,271 customers), Germany (119/1,004 customers), Spain (81/1,138 customers)

For all countries, **the customers who use 1 product**, approximately 21% - 43% of them are churned.
- Churned customers: France (537/2,407 customers), Germany (550/1,290 customers), Spain (250/1,157 customers)

**Remark:**
The more bank products customers use, the more likelihood they would churn. This is contrasted to the ‘Feeling’ that if someone use many bank products, they are ‘not likely’ to churn from the bank, but the information provided are contrasted. Studying from other contexts can provide more understanding.


<a class='anchor' id='bullet4'></a>
# Future Scopes
---

1. This is an imbalanced dataset, and solving the problem by collecting more data of churned customers is unlikely to be possible. In the future, consider using Deep Learning techniques to assess whether they improve the accuracy.
2. Consider advanced Hyperparameter Tuning techniques with Random Forest to assess whether they improve more performance than Decision Tree.

<a class='anchor' id='bullet5'></a>
# Jupyter Notebooks (in Thai language)
---

**Every file has the detailed explanations for every procedure and correctly follow the data science principles:**

- **For the data preparation,** please refer to [1_Data_Cleaning.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/1_Data_Cleaning.ipynb) for further information.

- **For the Exploratory Data Analysis (EDA) to gain the insights,** please refer to [2_EDA.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/2_EDA.ipynb) for further information.

- **For the prediction models of the bank customers churn,** please refer to [3_Logit.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/3_Logit.ipynb), [4_KNN.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/4_KNN.ipynb), [5_SVM.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/5_SVM.ipynb), [6_Naive_Bayes.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/6_Naive_Bayes.ipynb), [7_Decision_Tree.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/7_Decision_Tree.ipynb), และ [8_Random_Forest.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/8_Random_Forest.ipynb) for further information.

- **For the models’ performance comparison,** please refer to [9_Comparison.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/9_Comparison.ipynb) for further information.

---
△ [Back to Top](#toc)
