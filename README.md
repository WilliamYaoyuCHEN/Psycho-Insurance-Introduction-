# Psycho-Insurance-Introduction-
I have made codes repository private. If any dear members of admission committes would like to see the codes,  please contact me at c.yaoyu@wustl.edu
# Psycho-insurance: Understanding how psychology affects insurance risk score 

### Supervisor: Salih Tutun, PhD
Faculty and Researcher of Olin Business School, Washington University in St. Louis
### Lead Research Assistant: Yaoyu Chen (William)
Master of Science in Quantitative Finance \
Master of Science in Business Analytics (Candidate), Olin Business School, Washington University in St. Louis

## Overview
### Goal: 
Develop decision support systems using explainable AI and deep learning models for business applications. We design the artifact (an explainable AI framework) to predict and understand how psychological factors affect the insurance risk score. We used machine learning and network science to propose more explainable images. Experts can make predictions based on readable images without machine learning methods. 

### Data: 
We collected 1000 samples (for general insurance information and psychological information). Features include 90 questions in SCL-90-R and other insurance-related variables. 

### Methodology: 
Network science, deep learning, and Shapley values 

### Findings: 
-Provide solutions to prepare highly explainable images for predicting insurance risks. \
-Training using psychological features with insurance features had better accuracy than training using only insurance features. \
-The training result of images transferred from tabular data outperformed the original tabular data. \
-Certain psychological questions are highly correlated with insurance risks. 

## Structure Overview
![image](https://user-images.githubusercontent.com/106643421/209813558-cc927808-827d-4aec-af16-8ee5fc5c53db.png)\
Step 1: \
-90 psychological and other automobile insurance features are located in the 2-d image by applying Graph with weighted edges. \
Step 2: \
-Find the minimum bounding rectangular with the convex-hull algorithm. \
-Rotate the image based on the center of the minimum rectangular. \
-This is to confirm the positions of each feature in the Cartesian coordinate system. \
Step 3: \
-Input features in each sample into corresponding pixels in the form of pixels color. Each sample (client) will produce one image. \
Step 4: \
-Train images in CNN neural network. \
Step 5: \
-Calculate averaged shapley values for each feature to create a canvas. \
Step 6: \
-Create explainable images by blending shapley value canvas and image samples.

## Training Results
![image](https://user-images.githubusercontent.com/106643421/209813408-e9a892dc-7056-4d0e-994f-ad19c1d193bd.png)\

-The result without 90 psychological questions is terrible. It suggests that considering psychological factors can boost the training result. \
-If using tabular data for training instead of converted images, the test accuracy won’t surpass the training of images, while tabular data AI suffers from difficulty in explanation.

## Explainable AI: predict and understand insurance risk without ML methods
![image](https://user-images.githubusercontent.com/106643421/209815052-5f36f760-c573-4039-b3b2-71c697123544.png)\
(figure 1)

On the canvas of shapley values (figure 1): \
Red and green rectangles represent averaged shapley value of features. \
-Red means this feature, on average, contributes to the untrustworthiness category. While green means it contributes to the trustworthiness category. (If a customer is untrustworthy, then the insurance risk of this customer is high) \
-Deeper shade of red or green means its contribution is to a larger degree. \
-Through this canvas, experts can quickly know the degree and direction of the contribution of each feature.



![image](https://user-images.githubusercontent.com/106643421/209815061-3e5c7c56-b21c-4536-b9db-97cab0d8d7a5.png)\
(figure 2)

On this trustworthiness (negative) sample (figure 2): \
-Experts can make predictions based on such images. \
-Feature values of this sample (one row) are projected to the centers of red-green rectangles as grey or black dots. \
-All feature values are rescaled to 0-255. The greater the feature’s value in this sample, the deeper the dot’s shade. If a feature value is 0 (binary variables), its Shapley value won’t show up. \
-Therefore, the combination of a deep dot and deep red or green means that in this sample, this specific feature contributes to untrustworthiness or trustworthiness to a large degree, respectively. We call the combination of a deep dot and deep red square as “significantly positive feature” and the combination of a deep dot and deep green square as “significantly negative feature.” \
-We find some positive features would be “significantly positive features” only in untrustworthiness (positive) samples but not in trustworthiness (negative) samples. We call these decisive features “key features.” But not all features with positive shapley values can lead to untrustworthiness (positive), even if they are also significant. Actually, we find that the key features are 7 psychological features, which also implies that there are connections between psychological questions and insurance risk.


![image](https://user-images.githubusercontent.com/106643421/209815108-edd6258d-acde-4aa7-aea3-18161c4940d1.png)\
(the same negative sample as figure 2)

-Based on this, we can make the manual prediction. If we can find at least one key features in the sample, we can classify this sample as untrustworthiness (positive). If we can’t find any key features, then this is a negative sample. \
-For this sample, none of the key features shows up with high feature values (deeper dot, significance). We would give it a negative prediction result. \
-For example, one key feature, q83, which should have appeared in the purple circle, disappears from this sample. (if the value of this feature is 0, we will delete the shapley value square in this sample to simplify). And all other 6 key features are either not showing up or have lighter dots (not significant). In this case, we attribute this sample to negative. \
-The prediction accuracy of this method on the test dataset is 83.5%. \
-In the future, we will continue to increase the interpretability of images and find more relationships between psychological issues (psychological features we used are connected to mental disorders) and human behaviors.

