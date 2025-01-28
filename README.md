# Fraud_Detection_Transactions

## INTRODUCTION
In today's fast-changing financial landscape, the diversification and growing digitization of transactions have led to a significant rise in financial fraud. This issue not only threatens individual consumers but also posses substantial risks to businesses and the overall financial system. In this context, identifying and implementing effective fraud detection and prevention measures has become increasingly critical. While traditional fraud detection methods have been effective in the past, their limitations have become more apparent as fraudulent techniques evolve and data volumes grow exponentially. As a result, there is a pressing need to adopt more efficient and intelligent solutions.

Machine learning, a key branch of artificial intelligence, is widely regarded as a powerful tool to tackle the challenges of financial fraud due to its advanced data processing and pattern recognition capabilities. In the face of an increasingly complex financial environment, machine learning has emerged as a vital technology for enhancing fraud detection. As data volumes surge and fraud tactics continuously adapt, traditional methods are struggling to keep pace. Machine learning, with its ability to process large datasets efficiently and identify patterns dynamically, offers a more flexible and adaptive approach to detecting and preventing financial fraud.

## DATA PROCESSING AND FEATURE ENGINEERING
In this section, the steps taken to preprocess the dataset and engineer relevant features to improve the performance of the fraud detection model is outlined. The dataset initially contained a variety of features, some of which were either redundant, irrelevant, or could be transformed into more meaningful representations for the task at hand.

### Feature Removal
To streamline the dataset and eliminate unnecessary or redundant information, several columns were dropped. These included personally identifiable information (PII) such as first, last, ssn, cc_num, and acct_num, which are not only irrelevant for fraud detection but also raise privacy concerns. Additionally, geographical features like merch_lat, merch_long, zip, and street were removed, as they did not contribute significantly to the predictive power of the model. Temporal features such as trans_time_secs and trans_time_hrs were also excluded, as they were either redundant or could be represented more effectively in other forms. The following code snippet demonstrates the removal of these features
 ![image](https://github.com/user-attachments/assets/f935e3a0-bc5e-4609-8683-02501ecca180)

### Data Type Conversion
To facilitate further analysis and feature engineering, certain columns were converted to more appropriate data types. Specifically, the dob (date of birth) and trans_date (transaction date) columns were converted from strings to datetime objects using the pd.to_datetime() function. This conversion allowed for the extraction of meaningful temporal features, such as the age of the customer, which is a more relevant predictor for fraud detection than the raw date of birth
 ![image](https://github.com/user-attachments/assets/2ba2dce5-ab58-434d-85d9-3d000ca29f7d)

## Feature Engineering: Age Calculation
To derive the age of each customer, a function named calculate_age was implemented. This function computes the age based on the difference between the current date and the customer's date of birth, adjusting for whether the birthday has occurred in the current year. The resulting age values were stored in a new column, age, which was added to the dataset. This feature is expected to provide valuable insights, as age can be a significant factor in identifying fraudulent behaviour
![image](https://github.com/user-attachments/assets/67fe6263-13c2-4fd9-81ce-230372134b08)


## EXPLORATORY DATA ANALYSIS
### Numerical Features
From the figure below, the age distribution in the dataset is right-skewed, with most individuals aged 20–50. This indicates younger users dominate, suggesting fraud detection models should focus on their transaction behaviours. Older age groups (60+) are less represented, requiring careful handling to avoid oversight.
Transaction amounts are also right-skewed, with most transactions being low-value (0–1,000), typical of everyday activities like retail purchases. High-value transactions (above 5,000) are rare but critical for fraud detection due to their higher risk. 
  ![image](https://github.com/user-attachments/assets/a8f4d9b6-bef9-4935-9157-46197df03146)
![image](https://github.com/user-attachments/assets/516bd2a1-c822-4a2d-a284-753bb02fdb94)

  
The age boxplot reveals that most individuals fall within the 20–60 years range, with a median around 43 years. A few outliers exist beyond the upper whisker, representing older individuals. This aligns with earlier findings that younger users dominate the dataset, but the presence of older outliers suggests their behaviors should not be overlooked in fraud detection.
The city population boxplot shows that most transactions occur in cities with populations below 1 million, with a median around 100,000. However, significant outliers represent major metropolitan areas with populations exceeding 2 million. This indicates that while smaller cities are the primary focus, high-population urban centers may exhibit distinct transaction patterns and fraud risks.
The transaction amount boxplot highlights that most transactions are low-value, concentrated below 10,000, with a median around 1,000. However, numerous outliers represent high-value transactions above 20,000. These outliers are critical for fraud detection, as they may indicate unusual or risky activities.
  ![image](https://github.com/user-attachments/assets/2571fa69-c9ad-4834-91c8-b13933abde5c)
![image](https://github.com/user-attachments/assets/62e3677d-e49a-454e-92bb-b67ff4e10944)
![image](https://github.com/user-attachments/assets/b5fe48ea-09f0-4f30-b6c7-e418870d3ac2)

 
### Categorical Features
The gender distribution reveals an almost equal number of male and female individuals participating in transactions. This balanced representation suggests that both genders are equally active in the financial activities captured by the dataset, which is important for ensuring that fraud detection models do not exhibit gender bias.

The transactions are heavily concentrated in certain regions, with cities in California, Texas, Florida, New York, and Peninsula recording the highest number of transactions. This geographical clustering indicates that these areas are major hubs of financial activity, potentially due to higher population densities or economic activity. Understanding these regional trends is crucial for identifying location-specific fraud patterns.
The categories of transactions predominantly include basic necessities and everyday items. This suggests that most transactions are related to routine purchases. However, the presence of high-value transactions within these categories could indicate potential fraudulent activities, as such transactions may deviate from typical spending patterns.
 ![image](https://github.com/user-attachments/assets/88d800c8-0343-4f5a-bd4d-dd985ff29423)


Moreover, it is crucial to analyze the cities and states where fraudulent transactions originate. The data reveals that cities with the highest overall transaction volumes also tend to have a higher number of fraudulent transactions. However, there is an interesting observation: some cities with relatively lower transaction volumes report a higher proportion of fraudulent activities compared to cities with larger transaction volumes. This could suggest that certain cities may have more robust systems or a culture of honesty, potentially due to the presence of more reputable or vigilant individuals. For instance, cities like Houston and Brooklyn stand out as having the highest number of fraudulent transactions, indicating that these areas may require closer monitoring.

Additionally, certain merchants recorded a significantly higher number of fraudulent transactions. These merchants should be alerted and encouraged to enhance their security measures, as they appear to be more vulnerable to fraudulent activities. By identifying these high-risk merchants and cities, we can implement targeted strategies to mitigate fraud and protect both consumers and businesses. This analysis underscores the importance of understanding regional and merchant-specific trends to develop more effective fraud prevention measures.
   ![image](https://github.com/user-attachments/assets/2fe82349-aed5-4539-93bc-894bbb8e433e)
![image](https://github.com/user-attachments/assets/0a71d6d5-7aa5-49e3-95e1-d34d1673198d)

It was observed that individuals in the age group of 50–59 had the highest number of fraudulent transactions. This finding raises an interesting question: why is this age group more susceptible to fraud? One possible explanation is that fraudsters may intentionally target or impersonate individuals in this age bracket. They might perceive that older individuals are treated with greater trust or fairness compared to younger people, making it easier to exploit this perception. Additionally, older individuals may be less familiar with modern digital security practices, making them more vulnerable to fraudulent schemes. This highlights the need for targeted awareness campaigns and enhanced security measures for this age group to reduce their risk of falling victim to fraud
![image](https://github.com/user-attachments/assets/bea5dd3b-f1b8-408d-ae25-82e138488b19)

 
## CLUSTERING ANALYSIS FOR FRAUD DETECTION 
Due to the large size of the dataset and computational constraints, a 10% random sample of the data was used for clustering which is 85,803. This approach ensures that the analysis remains efficient while still capturing the underlying patterns in the data. To determine the optimal number of clusters (k) for the K-means algorithm, the elbow method was employed. This technique involves plotting the within-cluster sum of squares (WCSS) against different values of k and identifying the "elbow point" where the rate of decrease in WCSS slows down. Based on this analysis, the optimal number of clusters was determined to be k=3
 ![image](https://github.com/user-attachments/assets/1c83d55f-a6fb-4c5a-b36f-03e0f5b66247)

K-means algorithm was applied, each data point was assigned to one of the three clusters based on its proximity to the cluster centroids. Additionally, the distance of each point to its cluster centroid was calculated to measure how well the points fit within their respective clusters. To identify potential fraudulent transactions, a distance threshold was applied. Transactions that were significantly far from their cluster centroids were flagged as potential frauds. The threshold was set at the 97th percentile of the distance distribution, meaning that the top 3% of transactions with the largest distances were considered outliers. These outliers were labeled as potential frauds because they deviated significantly from the normal transaction patterns represented by the clusters. 2575 transactions were identitfied as potential frauds
![image](https://github.com/user-attachments/assets/77d466c3-82ff-4778-acdb-d24926c64c64)

 
DBSCAN (Density-Based Spatial Clustering of Applications with Noise) was employed to identify clusters and outliers in the dataset. Unlike K-means, DBSCAN groups data points based on density, making it effective for detecting irregular patterns and noise, which are often indicative of fraudulent activities.  The analysis focused on key features such as transaction amount (amt), transaction category (category), and transaction time (unix_time). Features were standardized using StandardScaler to ensure equal weighting during clustering.
DBSCAN was configured with eps=1.5 (maximum distance between points in a cluster) and min_samples=5 (minimum points to form a cluster). The algorithm identified clusters based on dense regions of data points, labelling outliers as -1 (noise). Labels were mapped to descriptive names: -1: Fraud (Outliers), 0: Normal, 1-4: Suspicious Groups (potential fraud patterns). Transactions labeled as -1 (outliers) were flagged as potential frauds. The analysis detected X potential frauds (replace X with the actual number).
DBSCAN's ability to detect noise and irregular patterns makes it a powerful tool for identifying potential frauds in transactional data
![image](https://github.com/user-attachments/assets/cb609e7f-635f-4bc9-8002-192b653a3063)

 
## Fraudulent Transaction Predictive Modelling
A sample of 10% of the data was selected which was about 850,000. The gender category was one hot encoded, the numerical category were scaled using standard scaler while other categorical features were label encoded. The data was split into 80:20 train and test respectively. The 2-algorithm employed in this task were Logistic regression and gradient boosting classifier
Results:
 ![image](https://github.com/user-attachments/assets/c7989a4b-cd31-4534-8a24-5f74fbaa5947)
![image](https://github.com/user-attachments/assets/4c57634b-deba-4866-8935-2de0c2f072a2)

 
Logistic Regression model performs exceptionally well for non-fraudulent transactions (Class 0) but struggles with fraudulent transactions (Class 1) even though the overall accuracy is high. The precision, recall, and F1-score for Class 1 are very low, indicating that the model fails to detect most fraudulent transactions.

The Gradient Boosting Classifier outperforms Logistic Regression, achieving higher accuracy, precision, recall, and F1-score for both classes. For fraudulent transactions (Class 1), the model achieves a precision of 93.37% and a recall of 66.72%, which is significantly better than Logistic Regression. The F1-score for Class 1 is 77.83%, indicating a much better balance between precision and recall for detecting fraud.
Furthermore, Gradient Boosting Classifier is the better choice for this task, as it effectively balances the detection of both non-fraudulent and fraudulent transactions. Its ability to handle imbalanced data and capture complex patterns makes it a robust solution for fraud detection. Further improvements could involve hyperparameter tuning and exploring additional features to enhance performance due to computation power, the grid search took a longer time and as a result it was skipped and will be revisited to reduce the False positive and false negative so as to have the model performs very well
  ![image](https://github.com/user-attachments/assets/993d9df5-9ce2-4db9-8aee-76a07900fc3c)
![image](https://github.com/user-attachments/assets/ab0eaa18-bddd-4268-922e-f297ad25b95a)

The Gradient Boosting Classifier demonstrates strong predictive power, making it highly reliable for fraud detection.  The high AUC score suggests that the model is well-suited for handling imbalanced datasets, where fraudulent transactions are rare compared to non-fraudulent ones. 
Now to understand the classification better, we need to know the number of misclassifications that happened. From the result below, out of 171,606 instances, 698 were misclassified, the best way to reduce this is to tune the hyperparameters of the model and reduce the False negatives as much as possible as requested in the task
  ![image](https://github.com/user-attachments/assets/cae97094-5bd5-4cc5-96d5-4983aa619d62)

## GLOBAL AND LOCAL EXPLANATION WITH SHAP
The importance of this is to understand the model behaviour and how the prediction is made. In this case, the features contributing to the model prediction are show in the figure below with unix time, amount and category having the most impact
 ![image](https://github.com/user-attachments/assets/b80acde5-e8ae-4a89-a9f1-294928c0c776)

A high value of unix time increase the shap value from it base value while the high values of category and amount reduces the shap value as show by beeswarm. All other feature does not necessary contributed to the prediction, this indicates that further process like feature selection can be performed to ensure that only relevant feature were used for prediction
 ![image](https://github.com/user-attachments/assets/ac74cd70-463a-499d-b10e-a26d8573f826)

For local explanation of how the prediction of each instance is made, let’s consider the second instance in the test data. It is seen that the values of the amount and category pushes the prediction away from its baseline while gender and unix time further increases it. 
 ![image](https://github.com/user-attachments/assets/c1020564-1939-4a37-b438-3837893b9e20)

To further get the prediction whether it is fraudulent or not, the log odds were converted into probability using the formular below and any value less than 0.5 belongs to 0 (non-fraudulent) but if above 0.5, it belongs to 1 (fraudulent)

