---
title:  "🇹🇭 Thai [3] American Express Default (dimensionality reduction)"
layout: post
---

This work © 2024 by "ProStepSky.github.io จัดทำโดย S.U." is licensed under [CC BY-NC-ND 4.0](http://creativecommons.org/licenses/by-nc-nd/4.0/)  
(อ้างอิงแหล่งที่มา ห้ามนำไปใช้เพื่อการค้า และห้ามดัดแปลง)

<a class='anchor' id='toc'></a>

# การลดขนาดมิติข้อมูล (Dimensionality Reduction) เพื่อลดเวลาประมวลผลและเพิ่มประสิทธิภาพให้กับชุดข้อมูลการผิดนัดชำระหนี้ของ American Express ซึ่งมีขนาด 3 GB

### สารบัญ  
[Executive Summary](#bullet1)  
[Principal Component Analysis (PCA)](#bullet2)  
[Linear Discriminant Analysis (LDA)](#bullet3)  
[การเปรียบเทียบประสิทธิภาพของ models](#bullet4)  
[Future Scopes](#bullet5)  
[Jupyter Notebooks](#bullet6)  

ในระยะหลังนี้อุตสาหกรรมต่าง ๆ มีอภิมหาข้อมูล (Big Data) ที่มีปริมาณมากขึ้นอย่างต่อเนื่อง ดังนั้นการมีวิธีในการใช้ประโยชน์จากข้อมูลปริมาณมหาศาลอย่างมีประสิทธิภาพจึงเป็นสิ่งจำเป็น หนึ่งในวิธีเหล่านั้นคือการลดขนาดมิติข้อมูล (Dimensionality Reduction) โดยลดจำนวนตัวแปรในชุดข้อมูลเพื่อให้ชุดข้อมูลนั้นมีขนาดลดลงแต่ยังคงประสิทธิภาพไว้ ส่งผลให้การสร้าง model ใช้ระยะเวลาที่ลดลงอย่างเด่นชัด และบางครั้งยังสามารถเพิ่มประสิทธิภาพของตัว models ให้มากขึ้นยิ่งกว่าก่อนใช้เทคนิคลดขนาดมิติข้อมูลอีกด้วย

งานชิ้นนี้ได้ประยุกต์ใช้การลดขนาดมิติข้อมูล (Dimensionality Reduction) กับชุดข้อมูลการผิดนัดชำระหนี้ของ American Express ซึ่งมีขนาด 3 GB โดยใช้เทคนิค Principal Component Analysis (PCA) และ Linear Discriminant Analysis (LDA) เพื่อลดจำนวนตัวแปรในชุดข้อมูล 

จากนั้นเปรียบเทียบประสิทธิภาพของทั้งสองเทคนิคโดยใช้ Classification Models ได้แก่ Logistic Regression, Decision Tree, Naïve Bayes, และ Random Forest เพื่อเปรียบเทียบประสิทธิภาพระหว่างก่อนและหลังการลดขนาดมิติข้อมูล

(งานชิ้นนี้เน้นอธิบายที่เรื่องการลดขนาดมิติข้อมูลเท่านั้น สำหรับการอธิบาย Classification Models ท่านสามารถอ่านเพิ่มเติมได้ที่ชิ้นงาน[การทำนายการเลิกใช้ธนาคาร](https://prostepsky.github.io/2_Customer_Churn_TH))


<a class='anchor' id='bullet1'></a>
# Executive Summary
---

1. การประยุกต์ใช้การลดขนาดมิติข้อมูลกับชุดข้อมูลการผิดนัดชำระหนี้ของ American Express ซึ่งมีขนาด 3 GB ส่งผลให้การสร้าง model ใช้ระยะเวลาลดลงอย่างเห็นได้ชัด นอกจากนี้ยังสามารถเพิ่มประสิทธิภาพของตัว model ให้มากขึ้นได้อีกด้วย
2. การลดมิติข้อมูลโดยใช้ Principal Component Analysis (PCA) กับ Random Forest ได้ผลลัพธ์ที่ดีที่สุด (ทั้งลดเวลาและเพิ่มประสิทธิภาพ):
    - ลดระยะเวลาการทำงานจาก 2 ชั่วโมง 10 นาที เหลือเพียง 54 นาที
    - เพิ่มประสิทธิภาพความแม่นยำ F1 Score ของ Random Forest จาก 79.5% เพิ่มเป็น 80.0%


<a class='anchor' id='bullet2'></a>
# Principal Component Analysis (PCA)
---

การลดขนาดมิติข้อมูลด้วยเทคนิค Principal Component Analysis (PCA) จะใช้การทำ linear combination จาก features ต่าง ๆ โดยงานชิ้นนี้ทำ PCA โดยกำหนดไว้ที่ 30 components

### กราฟแสดงค่า variance (อิทธิพลของ features เก่าต่อ Principal Component (pc) ใหม่) สะสม

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/1.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/1.png)

หากใช้ 30 components จะมี variance สะสมอยู่ใน components เหล่านั้นมากถึง 95.7% ดังนั้น หากใช้ 30 components ก็สามารถครอบคลุมความหมายของข้อมูล (capture information) ได้เพียงพอ

### กราฟแสดงค่าอิทธิพลของ features เก่าต่อ Principal Component (pc) ที่สร้างขึ้นมาใหม่

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/2.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/2.png)

ยิ่ง features ใดมีอิทธิพลต่อ principle component มาก สียิ่งเข้ม หากเป็นสีแดงแสดงว่ามีอิทธิพลไปในทิศทางเดียวกัน (ค่าหนึ่งเยอะ อีกค่าหนึ่งเยอะด้วย) หากเป็นสีน้ำเงินแสดงว่ามีอิทธิพลไปในทิศทางตรงกันข้าม (ค่าหนึ่งเยอะ อีกค่าหนึ่งน้อย)

**สรุป:** งานชิ้นนี้ได้ทำการลดมิติด้วย Principal Component Analysis (PCA) จาก 181 features เหลือ 30 components

<a class='anchor' id='bullet3'></a>
# Linear Discriminant Analysis (LDA)
---

การลดขนาดมิติข้อมูลด้วยเทคนิค Linear Discriminant Analysis (LDA) จะใช้การสร้าง feature subspaces ขึ้นมาใหม่ ที่จะทำให้จุดข้อมูลของ classes ที่ต่างกัน แยกห่างจากกันมากที่สุด

### กราฟแสดงการแจกแจงของจุดข้อมูลกับแกน component ใหม่ที่ได้จากการทำ LDA

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/3.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/3.png)

จากกราฟพบว่าอัลกอริทึม Linear Discriminant Analysis สามารถแยก 2 classes ออกจากกันได้ดีพอสมควร

**สรุป:** งานชิ้นนี้ได้ทำการลดมิติด้วย Linear Discriminant Analysis (LDA) จาก 181 features เหลือ 1 component


<a class='anchor' id='bullet4'></a>
# การเปรียบเทียบประสิทธิภาพของ models
---

### เปรียบเทียบค่า Accuracy, F1 Score, Precision, และ Recall

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/4.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/4.png)

กราฟสีแดงคือ baseline models, สีเขียวคือ Principal Component Analysis (PCA) models, และสีน้ำเงินคือ Linear Discriminant Analysis (LDA) models

หลังทำ PCA แล้วพบว่า F1 Score ของ:
- Model ตระกูล tree-based ทำคะแนนได้ดีขึ้น: Decision Tree (จาก 69.7% เพิ่มเป็น 70.0%), Random Forest (จาก 79.5% เพิ่มเป็น 80.0%)
- Model ตัวอื่นทำคะแนนได้แย่ลง: Logistic Regression (จาก 75.1% ลดเหลือ 72.4%), Naïve Bayes (จาก 70.8% ลดเหลือ 51.2%)

หลังทำ LDA แล้วพบว่า F1 Score ของ:
- Model ตัวที่ทำคะแนนได้ดีขึ้น: Naïve Bayes (จาก 70.8% เพิ่มเป็น 75.2%)
- Model ตัวที่ทำคะแนนได้แย่ลง: Logistic Regression (จาก 75.1% ลดเหลือ 74.0%), Decision Tree (จาก 69.7% ลดเหลือ 65.5%), Random Forest (จาก 79.5% ลดเหลือ 65.6%)

### เปรียบเทียบระยะเวลาที่อัลกอริทึมใช้ในการทำงาน

![https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/5.png](https://raw.githubusercontent.com/ProStepSky/ProStepSky.github.io/master/img/3_Dimension_Reduct/5.png)

ทุก models หลังทำ PCA กับ LDA แล้ว ใช้ระยะเวลาในการทำงานลดลงอย่างมาก:
- Logistic Regression จากเดิมใช้เวลา 5 นาที, หลังทำ PCA และ LDA ลดเหลือไม่ถึง 1 นาที
- Naïve Bayes ทั้งก่อนและหลังทำ PCA และ LDA ใช้เวลาไม่ถึง 1 นาที เนื่องจากอัลกอริทึมใช้หลักความน่าจะเป็นของ Bayes’ Theorem จึงทำงานได้เร็วมากอยู่แล้ว
- Decision Tree จากเดิมใช้เวลา 33 นาที, หลังทำ PCA ลดเหลือ 5 นาที, หลังทำ LDA ลดเหลือไม่ถึง 1 นาที
- Random Forest จากเดิมใช้เวลา 130 นาที, หลังทำ PCA ลดเหลือ 54 นาที, หลังทำ LDA ลดเหลือ 18 นาที

(ทดสอบอัลกอริทึมโดยใช้ CPU รุ่น AMD Ryzen 5 PRO 3500U)

<a class='anchor' id='bullet5'></a>
# Future Scopes
---

1. หากทราบรายละเอียดว่าแต่ละตัวแปร (feature) คือตัวแปรอะไรและมีความสำคัญหรือมีความหมายว่าอย่างไร (เช่น บุคลากรของธนาคารที่สามารถใช้งานฐานข้อมูลของธนาคารได้) จะทำให้สามารถแทนค่าที่หายไป (missing values) ได้ ซึ่งสามารถทำให้ model ทำนายได้แม่นยำขึ้น แต่สำหรับชุดข้อมูลนี้เป็นของ American Express ซึ่งได้ผ่านการทำให้เป็นแบบนิรนาม (anonymised) มาก่อน  ส่งผลให้ไม่สามารถทราบได้ว่าควรแทนค่าที่หายไป (missing values) อย่างไร
2. สามารถใช้เทคนิค Hyperparameter Tuning อย่างเช่นในงาน[การทำนายการเลิกใช้ธนาคาร](https://prostepsky.github.io/2_Customer_Churn_TH) เพื่อเพิ่มให้ models ทำนายได้แม่นยำขึ้น
3. อาจทำการหาค่าสหสัมพันธ์เพื่อทำการคัดเลือก features (feature selection) เพื่อคัด features ที่มีค่าสหสัมพันธ์ต่ำทิ้งไป ก่อนจะนำไปลดขนาดมิติข้อมูล
4. อาจลองใช้ Deep Learning แทน Classification Model เพื่อดูว่าทำให้ model ทำนายได้แม่นยำยิ่งขึ้นอีกหรือไม่
5. อาจใช้เทคนิค Dimensionality Reduction แบบอื่นเพื่อดูว่าทำให้ model ทำนายได้แม่นยำยิ่งขึ้นอีกหรือไม่


<a class='anchor' id='bullet6'></a>
# Jupyter Notebooks
---

**ทุกไฟล์มีคำอธิบายทุกขั้นตอนการดำเนินการอย่างละเอียดและถูกหลักวิทยาศาสตร์ข้อมูล:**

- **การเตรียมข้อมูล** ท่านสามารถอ่านเพิ่มเติมได้ที่ [1_Data_Cleaning.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/1_Data_Cleaning.ipynb)

- **การสร้าง baseline models ก่อนการลดขนาดมิติข้อมูล** ท่านสามารถอ่านเพิ่มเติมได้ที่ [2_Baseline.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/2_Baseline.ipynb)

- **Principal Component Analysis (PCA)** ท่านสามารถอ่านเพิ่มเติมได้ที่ [3_PCA.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/3_PCA.ipynb)

- **Linear Discriminant Analysis (LDA)** ท่านสามารถอ่านเพิ่มเติมได้ที่ [4_LDA.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/4_LDA.ipynb)

- **การเปรียบเทียบประสิทธิภาพของ models**  ท่านสามารถอ่านเพิ่มเติมได้ที่ [5_Comparison.ipynb](https://github.com/ProStepSky/Portfolio/blob/main/3_Dimension_Reduct/5_Comparison.ipynb)

---
△ [Back to Top](#toc)
