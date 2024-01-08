---
title:  "[🇬🇧 English] 4) Customer Segmentation (clustering)"
layout: post
---
Copyright © 2024 ProStepSky.github.io จัดทำโดย S.U.

<a class='anchor' id='toc'></a>

# Customer Segmentation from Their Consumption Behaviours by Developing Clustering Models

### Table of Contents
[Executive Summary](#bullet1)  
[K-Means Clustering](#bullet2)  
[Hierarchical Clustering](#bullet3)  
[Conclusions](#bullet4)  
[Future Scopes](#bullet5)  
[Jupyter Notebooks (in Thai language)](#bullet6)  

Today, our world has different activities that proceed rapidly due to the development of information technologies. Many businesses try to find methods continually in order to make the business grow. One of these methods is analysing consumption behaviours to segment customers into different groups, which depend on the data-driven. It has very high potential to increase sales and earnings to the company.

This project has used the dataset from an online store in the UK which collected data for 2 years. The dataset could be segmented into 3 customer groups from consumption behaviours by developing clustering models including K-Means and Hierarchical Clustering.


<a class='anchor' id='bullet1'></a>
# Executive Summary
---

1. After the customer segmentation by using K-Means and Hierarchical Clustering, found that some customers are segmented into different groups, but the conclusions are in the same ways, as following.
    - Customer group 1: Spend less, buy recently, and buy moderate times.
        - Broad suggestions, such as offering a discount after 5 times bought, etc.
    - Customer group 2: Spend less, buy long ago, and buy few times.
        - Broad suggestions, such as notify when there are major yearly or seasonal promotions, for instance, 6th day of the 6th month, etc. 
    - Customer group 3: Spend more, buy recently, and buy many times.
        - Broad suggestions, such as offering many discounts once or twice in a while, but don’t offer the discounts often, etc.
These broad suggestions are rewards and can impress the customers which leads to increasing the brand loyalty.

2. This customer segmentation project could be utilised for further usages, that is, develop customised models for each customer segments which could gain more accurate insights and more accurate prediction, when compared to the models’ development for the general customers. From the section 1 which is the broad suggestion, by following this section 2, they would be suggestions that more satisfied specifically for each customer segments. For instance, if we are considering offering discounts, we will know which products are the most matching and most personalised to that customer segments, which cause more satisfaction and the company would gain more profits.

3. From section 2, the examples of further usages; for instance, analyse the markets for each customer segments to gain insights, personalised promotions, personalised discounts, personalised goods and services recommendations, etc.


<a class='anchor' id='bullet2'></a>
# K-Means Clustering
---

### The Customer Segmentation Chart

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/4_Customer_Segment/1.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/4_Customer_Segment/1.png)

Found that it is similar to the Hierarchical Clustering’s chart, some data points are segmented into different clusters.

### The Consumption Behaviours for Each Customer Segments Chart

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/4_Customer_Segment/2.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/4_Customer_Segment/2.png)

Description for each variable:
- TotalSum: Total summation for each customer.
- DaysSinceLastInvoice: Number of days since the last invoice for each customer.
- InvoiceCount: Number of invoices for each customer.


<a class='anchor' id='bullet3'></a>
# Hierarchical Clustering
---

### The Customer Segmentation Chart

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/4_Customer_Segment/3.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/4_Customer_Segment/3.png)

Found that it is similar to the K-Means Clustering’s chart, some data points are segmented into different clusters.

### Consumption Behaviours for Each Customer Segments Chart

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/4_Customer_Segment/4.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/4_Customer_Segment/4.png)

Description for each variable:
- TotalSum: Total summation for each customer.
- DaysSinceLastInvoice: Number of days since the last invoice for each customer.
- InvoiceCount: Number of invoices for each customer.


<a class='anchor' id='bullet4'></a>
# Conclusions
---

From the customer segmentation chart and consumption behaviours for each customer segments chart, the conclusions of consumption behaviours of 3 customer groups are the following:

| |Group 1 |Group 2 |Group 3 |
|:-:|:-:|:-:|:-:|
|**TotalSum**| Spend less | Spend less | Spend more |
|**DaysSinceLastInvoice**| Buy recently | Buy long ago | Buy recently |
|**InvoiceCount**| Buy moderate times | Buy few times | Buy many times |

Customer group 1: Spend less, buy recently, and buy moderate times.
Customer group 2: Spend less, buy long ago, and buy few times.
Customer group 3: Spend more, buy recently, and buy many times.

Both K-Means and Hierarchical Clustering could be concluded in the same ways.


<a class='anchor' id='bullet5'></a>
# Future Scopes
---

1. Instead of calculating the number of days since the last invoice (DaysSinceLastInvoice variable), it would be better to calculate the date duration between each purchase of customers and then find the average. That way would be more related to the reality.
2. This customer segmentation project could be used to develop customised models for each customer segments for the further usages. For instance, analyse the markets for each customer segments to gain insights, personalised promotions, personalised discounts, personalised goods and services recommendations, etc.


<a class='anchor' id='bullet6'></a>
# Jupyter Notebooks (in Thai language)
---

**Every file has the detailed explanations for every procedure and correctly follow the data science principles:**

- **For the data preparation,** please refer to [1_Data_Cleaning.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/4_Customer_Segment/1_Data_Cleaning.ipynb) for further information.

- **K-Means Clustering,** please refer to [2_Kmeans.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/4_Customer_Segment/2_Kmeans.ipynb) for further information.

- **Hierarchical Clustering,** please refer to [3_Hierarchical.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/4_Customer_Segment/3_Hierarchical.ipynb) for further information.

---
△ [Back to Top](#toc)
