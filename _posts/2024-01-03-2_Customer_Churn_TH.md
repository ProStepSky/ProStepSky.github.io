---
title:  "🇹🇭 Thai [2] Bank Customer Churn (classification, random forest)"
layout: post
---

This work © 2024 by "ProStepSky.github.io จัดทำโดย S.U." is licensed under [CC BY-NC-ND 4.0](http://creativecommons.org/licenses/by-nc-nd/4.0/)  
(อ้างอิงแหล่งที่มา ห้ามนำไปใช้เพื่อการค้า และห้ามดัดแปลง)

<a class='anchor' id='toc'></a>

# ทำนายลูกค้าที่มีแนวโน้มจะเลิกใช้ (churn) ธนาคาร โดยพัฒนา Classification และ Random Forest Models

### สารบัญ  
[Executive Summary](#bullet1)  
[การเปรียบเทียบประสิทธิภาพของ models](#bullet2)  
[Exploratory Data Analysis เพื่อให้ได้ Insights](#bullet3)  
[Future Scopes](#bullet4)  
[Jupyter Notebooks](#bullet5)  

ในโลกธุรกิจที่มีการแข่งขันดั่งเช่นทุกวันนี้ เพื่อรักษาผลกำไรให้กับบริษัทการรักษาฐานลูกค้าไว้จึงเป็นสิ่งที่สำคัญอย่างมาก หนึ่งในสิ่งที่สามารถชี้วัดความสำเร็จของบริษัทได้คือความสามารถในการพยากรณ์แนวโน้มของลูกค้าที่จะยกเลิกบริการ (churn) ได้ล่วงหน้า เพื่อจะได้ดำเนินการมาตรการเชิงรุก (proactive measures) ในการรักษาหรือดึงดูดลูกค้าเอาไว้ก่อนที่ลูกค้าจะยกเลิกบริการ

นอกจากนี้ การวิเคราะห์จากกลุ่มลูกค้าที่ยกเลิกบริการ (churn) ยังสามารถให้ความเข้าใจเชิงลึก (insights) ทำให้บริษัททราบว่าควรต้องปรับปรุงสินค้าและบริการอย่างไรได้อีกด้วย

งานชิ้นนี้ได้พัฒนา Classification Models ทั้งหมด 6 ชนิด ได้แก่ Logistic Regression, K-Nearest Neighbours (KNN), Support Vector Machine (SVM), Naïve Bayes, Decision Tree, และ Random Forest เพื่อทำนายลูกค้าที่มีแนวโน้มจะเลิกใช้ธนาคาร โดยใช้ปัจจัย ได้แก่ Credit Score, อายุ, จำนวนปีที่ลูกค้าใช้บริการ (tenure), ยอดเงินในบัญชี, จำนวนบริการที่ลูกค้าใช้งาน, มีบัตรเครดิตหรือไม่, ยังคงใช้บริการ (active) อยู่หรือไม่, รายได้โดยประมาณ, เพศ, และ มาจากประเทศใด (ฝรั่งเศส, เยอรมณี, สเปน)

จากนั้นเปรียบเทียบประสิทธิภาพของ models ทั้ง 6 ชนิด โดยประเมินค่า Accuracy, F1 Score, Precision, และ Recall พร้อมการอภิปราย


<a class='anchor' id='bullet1'></a>
# Executive Summary
---

1. งานชิ้นนี้ได้ทำการวิเคราะห์ข้อมูล Exploratory Data Analysis (EDA) เพื่อให้ได้ความเข้าใจเชิงลึก (insights) โดยสรุปคือ
    - ลูกค้าจากเยอรมณีมียอดเงินในบัญชีโดยเฉลี่ยมากกว่าลูกค้าจากฝรั่งเศสและสเปนประมาณ 2 เท่า ถึงแม้ลูกค้าจากทั้ง 3 ประเทศ ได้แก่ ฝรั่งเศส, เยอรมณี, และสเปน จะมีรายได้โดยเฉลี่ยใกล้เคียงกัน (ซึ่งตรงกับความเป็นจริงว่าชาวเยอรมันมีนิสัยชอบเก็บออมเนื่องจากในอดีตเยอรมณีเคยประสบความยากลำบากทางเศรษฐกิจมาก่อน)
    - ลูกค้ารายได้สูงไม่จำเป็นต้องมีเงินฝากในบัญชีจำนวนมากเสมอไป
    - ลูกค้าที่เลิกใช้ธนาคารมีทุกช่วงรายได้และทุกช่วงยอดเงินในบัญชี
    - อายุของลูกค้าไม่มีผลต่อรายได้ (ลูกค้าทุกช่วงอายุสามารถมีรายได้ได้ทุกช่วงรายได้)
    - ลูกค้าที่เลิกใช้ธนาคารส่วนมากจะเกาะกลุ่มบริเวณอายุสูง ๆ
    - ลูกค้าเพศหญิงมีแนวโน้มเลิกใช้ธนาคารสูงกว่าเพศชาย
    - ลูกค้าประเทศเยอรมณีมีแนวโน้มที่จะเลิกใช้ธนาคารสูงกว่าประเทศสเปนและฝรั่งเศส
    - 50% ของลูกค้าทั้งหมด มีอายุระหว่าง 32-43 ปี
    - 50% ของลูกค้าทั้งหมดที่เลิกใช้ธนาคาร มีอายุระหว่าง 38-50
    - ลูกค้าส่วนใหญ่ของทุกประเทศ (มากกว่า 95%) ใช้บริการของธนาคาร 1-2 บริการ
    - ยิ่งลูกค้าใช้บริการหลายตัวยิ่งมีโอกาสเลิกใช้ธนาคาร ซึ่งขัดต่อ "ความรู้สึก" คือหากใช้บริการหลายตัวยิ่ง "ไม่น่าจะ" เลิกใช้ธนาคาร แต่ข้อมูลที่ได้นี้กลับตรงกันข้าม หากศึกษาบริบทอื่นเพิ่มเติมอาจได้ความเข้าใจเพิ่มขึ้น
2. ชุดข้อมูลนี้มีสัดส่วนข้อมูลไม่สมดุล (imbalanced dataset) เนื่องจากในชุดข้อมูลนี้ มีลูกค้าที่เลิกใช้ธนาคารประมาณ 20% และลูกค้าที่อยู่ต่อมีประมาณ 80% ดังนั้นการทำนายว่าลูกค้าจะเลิกใช้ธนาคาร (churn) ไหม จะยากกว่าการทำนายว่าลูกค้าจะอยู่ต่อไหม


<a class='anchor' id='bullet2'></a>
# การเปรียบเทียบประสิทธิภาพของ models
---

### เปรียบเทียบค่า Accuracy, F1 Score, Precision, และ Recall

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/1.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/1.png)

**สำหรับ dataset นี้:**

- Recall สำคัญกว่า Precision เพราะ Recall พิจารณา False Negative
    - Recall คือ จำนวนที่ทำนายถูกว่า churn จากความจริงที่เป็น churn ทั้งหมด
    - False Negative สำคัญ เพราะทำนายว่า non-churn แต่ความจริงคือ churn
        - ทำนายผิดแบบนี้ ธนาคารอาจไม่ดำเนินมาตรการรักษาหรือดึงดูดลูกค้าคนนี้จนเขาเลิกใช้ธนาคาร (churn) ได้
    - ต้องพยายามทำให้ False Negative ต่ำ ๆ และ True Positive สูง ๆ

**แต่ในขณะเดียวกัน:**

- Precision ก็สำคัญ เพราะ Precision พิจารณา False Positive
    - Precision คือ จำนวนที่ทายถูกว่า churn จากจำนวนที่ทายว่า churn ทั้งหมด
    - False Positive คือทำนายว่า churn แต่ความจริงคือ non-churn
        - ทำนายผิดแบบนี้ จะทำให้ธนาคารสูญเสียทรัพยากรไปกับมาตรการรักษาหรือดึงดูดลูกค้าที่เขาไม่ได้จะเลิกใช้ธนาคาร และยังอาจทำให้ลูกค้ารู้สึกรำคาญโดยไม่จำเป็นอีกด้วย

**นั่นคือ:**

-	สำหรับ dataset นี้ model ชนิด Decision Tree และ Random Forest ทำนายได้ดีที่สุดเนื่องจากค่า Recall และ Precision สูงทั้งคู่ และเมื่อพิจารณา F1 Score (ค่า balance ของ Recall และ Precision) ก็ให้ค่าที่สูงสุดเช่นกัน
    - ค่า F1 Score ของทั้ง Decision Tree และ Random Forest มีค่าอยู่ที่ประมาณ 60% ทั้งคู่
    - Model ชนิด Decision Tree จะได้ค่า Recall ที่สูงกว่า Random Forest อีกประมาณ 5%
    - Model ชนิด Random Forest จะได้ค่า Precision ที่สูงกว่า Decision Tree อีกประมาณ 3%

**หมายเหตุ:** churn คือ เลิกใช้ธนาคาร, non-churn คืออยู่กับธนาคารต่อไป ไม่เลิกใช้ธนาคาร

<a class='anchor' id='bullet3'></a>
# Exploratory Data Analysis เพื่อให้ได้ Insights
---
งานชิ้นนี้ได้ทำการวิเคราะห์ข้อมูลเพื่อให้ได้ความเข้าใจเชิงลึก (insights) โดยอภิปรายได้ดังต่อไปนี้

### 1) อัตราส่วนของลูกค้าที่เลิกใช้ธนาคาร กับลูกค้าที่ยังใช้ธนาคารอยู่

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/2.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/2.png)

ชุดข้อมูลนี้มีสัดส่วนข้อมูลไม่สมดุล (imbalanced dataset) เนื่องจากในชุดข้อมูลนี้ มีลูกค้าที่เลิกใช้ธนาคารประมาณ 20% และลูกค้าที่อยู่ต่อมีประมาณ 80% ดังนั้นการทำนายว่าลูกค้าจะเลิกใช้ธนาคาร (churn) ไหม จะยากกว่าการทำนายว่าลูกค้าจะอยู่ต่อไหม

การแก้ปัญหาโดยเก็บข้อมูลลูกค้าที่เลิกใช้ธนาคารเพิ่มเป็นไปได้ยากมาก เพราะปกติแล้วลูกค้ามักจะไม่เลิกใช้ธนาคาร


### 2) การวิเคราะห์ความสัมพันธ์ระหว่างปัจจัยต่าง ๆ ที่ส่งผลต่อกันและกัน

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/3.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/3.png)

ตัวแปรส่วนใหญ่ไม่พบสหสัมพันธ์:
- Credit Score ไม่สัมพันธ์กับตัวแปรใดเลย
- จำนวนปีที่ลูกค้าใช้บริการ ไม่สัมพันธ์กับตัวแปรใดเลย
- ลูกค้ามีบัตรเครดิตหรือไม่ ไม่สัมพันธ์กับตัวแปรใดเลย
- รายได้โดยประมาณ ไม่สัมพันธ์กับตัวแปรใดเลย

ตัวแปรที่พบสหสัมพันธ์มีดังนี้:
- อายุมาก มีแนวโน้มเลิกใช้ธนาคาร (มีค่าสหสัมพันธ์เท่ากับ +0.36 ซึ่งมีความสัมพันธ์พอสมควร)
- ยิ่งจำนวนบริการที่ลูกค้าใช้งานมาก มีแนวโน้มว่ายอดเงินในบัญชีน้อย (มีค่าสหสัมพันธ์เท่ากับ -0.31 ซึ่งมีความสัมพันธ์พอสมควร)
- ลูกค้าที่ยังคงใช้บริการอยู่ (active) มีแนวโน้มจะไม่เลิกใช้ธนาคาร (มีค่าสหสัมพันธ์เท่ากับ -0.14 ซึ่งมีความสัมพันธ์อย่างอ่อน ๆ)
- ลูกค้าจากฝรั่งเศส มีแนวโน้มว่าเงินในบัญชีน้อย (มีค่าสหสัมพันธ์เท่ากับ -0.23 ซึ่งมีความสัมพันธ์อย่างอ่อน ๆ)
- ลูกค้าจากเยอรมณี มีแนวโน้มว่าเงินในบัญชีมาก (มีค่าสหสัมพันธ์เท่ากับ +0.40 ซึ่งมีความสัมพันธ์พอสมควร)
- ลูกค้าจากสเปน มีแนวโน้มว่าเงินในบัญชีน้อย (มีค่าสหสัมพันธ์เท่ากับ -0.14 ซึ่งมีความสัมพันธ์อย่างอ่อน ๆ)


### 3) จำนวนลูกค้าจากแต่ละประเทศ

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/4.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/4.png)

พบว่ามีลูกค้าจากฝรั่งเศสประมาณครึ่งนึง และที่เหลือเป็นสเปนและเยอรมันอีกประมาณอย่างละครึ่ง

#### จำนวนลูกค้าจากแต่ละประเทศ (แยกตามเพศ)
![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/5.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/5.png)

พบว่าทุกประเทศมีลูกค้าเพศหญิงน้อยกว่าเพศชาย

### 4) ยอดเงินในบัญชี เทียบกับ รายได้โดยประมาณ

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/6.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/6.png)

พบว่าลูกค้ารายได้สูงไม่จำเป็นต้องมีเงินฝากในบัญชีเยอะเสมอไป

พบว่าลูกค้าที่เลิกใช้ธนาคารมีทุกช่วงรายได้และทุกช่วงยอดเงินในบัญชี


### 5) อายุ เทียบกับ รายได้โดยประมาณ

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/7.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/7.png)

พบว่าอายุของลูกค้าไม่มีผลต่อรายได้ (ลูกค้าทุกช่วงอายุสามารถมีรายได้ได้ทุกช่วงรายได้)

พบว่าลูกค้าที่เลิกใช้ธนาคาร (จุดสีส้ม) ส่วนมากจะเกาะกลุ่มบริเวณอายุสูง ๆ

<a class='anchor' id='bullet_a'></a>
### 6) ยอดเงินในบัญชีโดยเฉลี่ย (แยกตามประเทศ)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/8.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/8.png)

จากกราฟพบว่า:
- ลูกค้าจากฝรั่งเศส มียอดเงินในบัญชีโดยเฉลี่ยประมาณ 62,000 EUR
- ลูกค้าจากเยอรมณี มียอดเงินในบัญชีโดยเฉลี่ยประมาณ 120,000 EUR ซึ่งมากกว่าลูกค้าจากฝรั่งเศสและสเปนประมาณ 2 เท่า
- ลูกค้าจากสเปน มียอดเงินในบัญชีโดยเฉลี่ยประมาณ 61,000 EUR

ซึ่งสอดคล้องกับการวิเคราะห์สหสัมพันธ์ก่อนหน้าคือ ลูกค้าจากเยอรมณีมียอดเงินในบัญชีโดยเฉลี่ยมากกว่าลูกค้าจากฝรั่งเศสและสเปน

<a class='anchor' id='bullet_b'></a>
### 7) รายได้โดยเฉลี่ย (แยกตามประเทศ)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/9.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/9.png)

จากกราฟพบว่าลูกค้าจากทั้ง 3 ประเทศ (ฝรั่งเศส, เยอรมณี, สเปน) มีรายได้โดยเฉลี่ยใกล้เคียงกัน

จากข้อมูลทั้ง [ยอดเงินในบัญชีโดยเฉลี่ยตามประเทศของลูกค้า](#bullet_a) และ [รายได้โดยเฉลี่ยตามประเทศของลูกค้า](#bullet_b) ข้างต้นทำให้ทราบว่า:
-	ลูกค้าจากเยอรมณีมียอดเงินในบัญชีโดยเฉลี่ยมากกว่าลูกค้าจากฝรั่งเศสและสเปนประมาณ 2 เท่า ถึงแม้ลูกค้าจากทั้ง 3 ประเทศ (ฝรั่งเศส, เยอรมณี, สเปน) จะมีรายได้โดยเฉลี่ยใกล้เคียงกัน
-	ซึ่งตรงกับความเป็นจริงว่าชาวเยอรมันมีนิสัยชอบเก็บออมเนื่องจากในอดีตเยอรมณีเคยประสบความยากลำบากทางเศรษฐกิจมาก่อนคือภาวะเงินเฟ้อ และนิสัยนี้ได้ส่งต่อจากรุ่นสู่รุ่นจนถึงปัจจุบัน


### 8) ลูกค้าที่เลิกใช้ธนาคาร

#### ลูกค้าที่เลิกใช้ธนาคาร (แยกตามเพศ)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/10.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/10.png)

พบว่าลูกค้าเพศหญิงมีแนวโน้มเลิกใช้ธนาคารสูงกว่าเพศชาย

#### ลูกค้าที่เลิกใช้ธนาคาร (แยกตามประเทศ)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/11.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/11.png)

ร้อยละของลูกค้าที่เลิกใช้ธนาคารต่อจำนวนลูกค้าของประเทศนั้น ๆ:
- ประมาณ 16% ของลูกค้าในฝรั่งเศส เลิกใช้ธนาคาร
- ประมาณ 32% ของลูกค้าในเยอรมณี เลิกใช้ธนาคาร
- ประมาณ 16% ของลูกค้าในสเปน เลิกใช้ธนาคาร
จากข้อมูลข้างต้นพบว่า ลูกค้าประเทศเยอรมณีมีแนวโน้มที่จะเลิกใช้ธนาคารสูงกว่าประเทศสเปนและฝรั่งเศส


### 9) การแจกแจงอายุลูกค้า

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/12.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/12.png)

พบว่า 50% ของลูกค้าทั้งหมด มีอายุระหว่าง 32-43 ปี

#### การแจกแจงอายุลูกค้าที่เลิกใช้ธนาคาร

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/13.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/13.png)

พบว่า 50% ของลูกค้าทั้งหมดที่เลิกใช้ธนาคาร มีอายุระหว่าง 38-50

จากข้อสรุปที่ได้จากกราฟข้างต้น
- 50% ของลูกค้าทั้งหมด มีอายุระหว่าง 32-43 ปี
- 50% ของลูกค้าทั้งหมดที่เลิกใช้ธนาคาร มีอายุระหว่าง 38-50 ปี

สอดคล้องกับการวิเคราะห์สหสัมพันธ์คือ อายุมาก มีแนวโน้มเลิกใช้ธนาคาร (มีค่าสหสัมพันธ์เท่ากับ +0.36 ซึ่งมีความสัมพันธ์พอสมควร)


### 10) จัดกลุ่มลูกค้าแยกตามจำนวนบริการที่ลูกค้าใช้

#### จำนวนของลูกค้าทั้งเลิกและไม่เลิกใช้ธนาคาร (แยกตามจำนวนบริการที่ลูกค้าใช้)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/14.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/14.png)

พบว่าลูกค้าส่วนใหญ่ของทุกประเทศ (มากกว่า 95%) ใช้บริการของธนาคาร 1-2 บริการ

#### จำนวนของลูกค้าที่เลิกใช้ธนาคาร (แยกตามจำนวนบริการที่ลูกค้าใช้)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/15.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/15.png)

#### สัดส่วนของลูกค้าที่เลิกใช้ธนาคาร (แยกตามจำนวนบริการที่ลูกค้าใช้)

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/16.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/2_Customer_Churn/16.png)

#### จากข้อมูลข้างต้นพบว่า

ทุกประเทศ **ลูกค้าที่ใช้ 4 บริการ** มีจำนวนถึง **100%** ที่เลิกใช้ธนาคาร
- ลูกค้าที่เลิกใช้ธนาคาร: ฝรั่งเศส (28/28 คน), เยอรมณี (23/23 คน), สเปน (7/7 คน)

ทุกประเทศ **ลูกค้าที่ใช้ 3 บริการ** มีจำนวนประมาณ **77% - 89%** ที่เลิกใช้ธนาคาร
- ลูกค้าที่เลิกใช้ธนาคาร: ฝรั่งเศส (78/96 คน), เยอรมณี (80/90 คน), สเปน (48/62 คน)

ทุกประเทศ **ลูกค้าที่ใช้ 2 บริการ** มีจำนวนประมาณ **5% - 12%** ที่เลิกใช้ธนาคาร
- ลูกค้าที่เลิกใช้ธนาคาร: ฝรั่งเศส (126/2,271 คน), เยอรมณี (119/1,004 คน), สเปน (81/1,138 คน)

ทุกประเทศ **ลูกค้าที่ใช้ 1 บริการ** มีจำนวนประมาณ **21% - 43%** ที่เลิกใช้ธนาคาร
- ลูกค้าที่เลิกใช้ธนาคาร: ฝรั่งเศส (537/2,407 คน), เยอรมณี (550/1,290 คน), สเปน (250/1,157 คน)

**ข้อสังเกตุ:**

ยิ่งลูกค้าใช้บริการหลายตัวยิ่งมีโอกาสเลิกใช้ธนาคาร ซึ่งขัดต่อ "ความรู้สึก" คือหากใช้บริการหลายตัวยิ่ง "ไม่น่าจะ" เลิกใช้ธนาคาร แต่ข้อมูลที่ได้นี้กลับตรงกันข้าม หากทราบบริบทอื่นเพิ่มเติมอาจได้ความเข้าใจเพิ่มขึ้น

<a class='anchor' id='bullet4'></a>
# Future Scopes
---

1. ชุดข้อมูลนี้มีสัดส่วนข้อมูลไม่สมดุล (imbalanced dataset) และการแก้ปัญหาโดยเก็บข้อมูลลูกค้าที่เลิกใช้ธนาคารเพิ่มเป็นไปได้ยากมาก ในอนาคตอาจลองใช้ Deep Learning เพื่อดูว่าทำให้ model ทำนายได้แม่นยำยิ่งขึ้นอีกหรือไม่
2. อาจใช้เทคนิค Hyperparameter Tuning ขั้นสูงมากขึ้นกับ Random Forest เพื่อดูว่าจะได้ประสิทธิภาพที่มากกว่า Decision Tree อีกหรือไม่


<a class='anchor' id='bullet5'></a>
# Jupyter Notebooks
---

**ทุกไฟล์มีคำอธิบายทุกขั้นตอนการดำเนินการอย่างละเอียดและถูกหลักวิทยาศาสตร์ข้อมูล:**

- **การเตรียมข้อมูล** ท่านสามารถอ่านเพิ่มเติมได้ที่ [1_Data_Cleaning.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/1_Data_Cleaning.ipynb)

- **การวิเคราะห์ข้อมูลเพื่อให้ได้ความเข้าใจเชิงลึก (insights)** ท่านสามารถอ่านเพิ่มเติมได้ที่ [2_EDA.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/2_EDA.ipynb)

- **Models ทำนายลูกค้าที่มีแนวโน้มจะเลิกใช้ธนาคาร** ท่านสามารถอ่านเพิ่มเติมได้ที่ [3_Logit.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/3_Logit.ipynb), [4_KNN.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/4_KNN.ipynb), [5_SVM.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/5_SVM.ipynb), [6_Naive_Bayes.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/6_Naive_Bayes.ipynb), [7_Decision_Tree.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/7_Decision_Tree.ipynb), และ [8_Random_Forest.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/8_Random_Forest.ipynb)

- **การเปรียบเทียบประสิทธิภาพของ models**  ท่านสามารถอ่านเพิ่มเติมได้ที่ [9_Comparison.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/2_Customer_Churn/9_Comparison.ipynb)

---
△ [Back to Top](#toc)
