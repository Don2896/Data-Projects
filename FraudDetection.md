# Fraud Detection in Bank Transactions: A Data Analysis and Machine Learning Approach

> **Companion notebook:** `fraudDetection.ipynb`  
> **Tools:** Python, Pandas, Matplotlib, Seaborn, Scikit-learn  
> **Data:** Simulated bank transaction records — 2,512 transactions, 16 features

---

## Background Overview

Fraud is the deceptive practice intended to result in financial or personal gain at the expense of another party. In the banking sector, fraud takes many forms, including identity theft, transaction manipulation, account takeovers, and unauthorised payments. As digital transactions increase, so does the sophistication of fraudulent activities, making it crucial for banks to develop effective detection systems to safeguard customers and financial institutions from monetary losses, reputational damage, and regulatory consequences. This project aims to analyse transactional data to identify patterns and anomalies indicative of fraudulent activity. By leveraging data analytics and machine learning techniques, the goal is to characterise fraudulent behaviour in bank transactions, enabling counter-fraud agencies to enhance their detection and prevention strategies.

---

## Objective

This project addresses business questions that could be put forward to fraud detection analysts tasked with identifying potentially fraudulent transactions and using their findings to profile customers at risk of fraudulent activity. The business questions are as follows:
- What are the characteristics of fraudulent transactions?
- How can we profile customers at risk of fraudulent activity?
- Are there any identifiable trends within fraudulent transactions?
- How effective is the outlined process in identifying fraudulent transactions?

---

## Data Exploration & Feature Engineering

The dataset used in this project consists of simulated bank transaction records, providing insights into customer transaction behaviours and potential fraud patterns. It includes key attributes such as transaction amounts, timestamps, account details, locations, and fraud labels. By exploring this data, the project seeks to develop a systematic approach to distinguishing fraudulent transactions from legitimate ones.

The dataset is initially explored to understand the types of transactional information provided (columns) for each transaction (rows). Information was obtained on the number of columns present, the data type of each column, and whether any null values were present.

<img width="415" alt="image" src="https://github.com/user-attachments/assets/92768906-b637-46bf-8e0a-397e916e5874" />
<img width="452" alt="image" src="https://github.com/user-attachments/assets/d6a6894f-7480-4065-bac6-1a8cda12801a" />

The dataset is comprised of 2,512 rows and 16 columns. These columns are as follows:

- **TransactionID:** Unique alphanumeric identifier for each transaction.
- **AccountID:** Unique identifier for each account, with multiple transactions per account.
- **TransactionAmount:** Monetary value of each transaction, ranging from small everyday expenses to larger purchases.
- **TransactionDate:** Timestamp of each transaction, capturing date and time.
- **TransactionType:** Categorical field indicating Credit or Debit transactions.
- **Location:** Geographic location of the transaction, represented by U.S. city names.
- **DeviceID:** Alphanumeric identifier for devices used to perform the transaction.
- **IP Address:** IPv4 address associated with the transaction, with occasional changes for some accounts.
- **MerchantID:** Unique identifier for merchants, showing preferred and outlier merchants for each account.
- **AccountBalance:** Balance in the account post-transaction, with logical correlations based on transaction type and amount.
- **PreviousTransactionDate:** Timestamp of the last transaction for the account, aiding in calculating transaction frequency.
- **Channel:** Channel through which the transaction was performed (e.g., Online, ATM, Branch).
- **CustomerAge:** Age of the account holder, with logical groupings based on occupation.
- **CustomerOccupation:** Occupation of the account holder (e.g., Doctor, Engineer, Student, Retired), reflecting income patterns.
- **TransactionDuration:** Duration of the transaction in seconds, varying by transaction type.
- **LoginAttempts:** Number of login attempts before the transaction, with higher values indicating potential anomalies.

<img width="776" alt="image" src="https://github.com/user-attachments/assets/ea6bcc02-4232-41bb-bd11-59e486af365a" />

From the above, 2,512 transactions were made across 495 accounts. Transactions took place across 43 different locations. A quick check for correlations shows the strongest relationship is between customer age and account balance. Focusing on TransactionAmount, TransactionDuration, and LoginAttempts:

- TransactionAmount has a large standard deviation (291.95), which is expected given the wide range of transaction values. The interquartile range provides a more robust measure of spread and is used to identify outliers.
- LoginAttempts has a small standard deviation (0.62), consistent with low expected variance around the mean of 1.
- TransactionDuration also shows a large standard deviation. Given that standard deviations are sensitive to outliers and the distribution is likely skewed, the interquartile range is used as the primary measure for outlier detection.

A correlation check on the numerical columns confirmed the only notable relationship is the positive correlation between AccountBalance and CustomerAge — consistent with the expectation that older account holders tend to hold larger balances.

Before identifying transaction patterns over time, feature engineering is applied to the TransactionDate column to convert values to datetime format, enabling extraction of hour, day of week, month, and time between transactions.

<img width="573" alt="image" src="https://github.com/user-attachments/assets/868931cf-32f3-428b-b78a-e303a1f8fe1e" />

Once TransactionDates were converted to datetime, hour, day of week, month, and transaction time were extracted into separate columns and their frequencies determined. Key findings: 4pm was the most frequent transaction hour, Monday the most frequent day, October the most frequent month, Fort Worth the most frequent location, and Branch the most frequent channel.

The distribution of transaction amounts follows the expected pattern — smaller values transact far more frequently than larger ones. Any substantial deviation from this would warrant immediate investigation as a potential indicator of suspicious activity.

<img width="532" alt="image" src="https://github.com/user-attachments/assets/0f98e738-312f-48e7-bb96-cfd8d24664bd" />

Transaction volumes did not show clear seasonality. A slight peak towards year-end is consistent with increased consumer spending, but overall volumes varied considerably throughout the year.

<img width="762" alt="image" src="https://github.com/user-attachments/assets/9d6e30a8-4ef6-4c0c-8ada-10b16b9b4f3b" />

Fort Worth, Los Angeles, and Oklahoma City had the highest transaction volumes. Branch transactions outnumbered ATM and online transactions.

<img width="764" alt="image" src="https://github.com/user-attachments/assets/c3a69bc5-c16b-4164-bbda-abf2bb7c1a44" />
<img width="769" alt="image" src="https://github.com/user-attachments/assets/34dccf10-9277-4af9-85a7-f0fada8191ca" />

---

## Fraud Detection

Before a transaction can be definitively identified as fraudulent, a first pass is applied to flag suspicious transactions, narrowing the pool of cases requiring investigation. A transaction is flagged as suspicious if it meets any one of the following three conditions:

- **Suspicious timeframe:** the time elapsed since the previous transaction is less than 1,800 seconds and the location has changed.
- **Suspicious location:** the account has transacted from a number of unique locations above the 95th percentile threshold.
- **Suspicious amount:** the transaction value falls outside an established lower or upper bound based on 3 standard deviations.

Using these criteria, 2,378 of 2,512 transactions were identified as suspicious. Analysis comparing suspicious and non-suspicious transactions found:

- Suspicious transactions occur at a significantly higher volume than non-suspicious transactions across the observed time period.
- Both groups show a declining trend over time.
- The gap between suspicious and non-suspicious transaction volumes remains consistently large.

<img width="996" alt="Screenshot 2025-03-27 at 18 48 47" src="https://github.com/user-attachments/assets/a70934a6-4b5a-4f7b-9896-3a6c64350087" />
<img width="991" alt="Screenshot 2025-03-27 at 18 49 36" src="https://github.com/user-attachments/assets/5c2e42c0-436a-448d-9d5f-c55e20542dbf" />

The next step was to use the suspicious transaction flags to identify high-risk customer accounts — those with the highest cumulative number of flags raised. For example, an account flagged for both suspicious amount and suspicious location receives a total flag count of 2. Of the 428 accounts with at least one flag, total counts ranged from 3 to 25. A significant drop in flag count between the 25th and 26th ranked accounts was used to define the threshold for the high-risk customer group.

<img width="557" alt="Screenshot 2025-03-27 at 19 18 09" src="https://github.com/user-attachments/assets/ba78ca50-a38b-4863-999d-d0b7daf64cb3" />

Principal Component Analysis (PCA) was applied to identify underlying patterns in fraudulent transactions based on three key indicators: Suspicious_Amount, Suspicious_Location, and Suspicious_Timeframe. The first principal component (PC1) highlights a trade-off between high transaction amounts and unusual location behaviour. The second component (PC2) is primarily driven by timeframe anomalies. The third component (PC3) captures risk arising from both high amounts and unusual locations simultaneously. Reducing the dataset into these principal components enables clustering of transactions by fraud type.

<img width="486" alt="image" src="https://github.com/user-attachments/assets/2f53a75b-6b8b-4914-9ef2-4868710c6d2a" />

A 2D scatter plot of PC1 vs. PC2 reveals three clusters. Cluster 2 (red) is more spread out with some points at extreme PC1 values, indicating highly anomalous transactions. Cluster 0 (blue) is tightly grouped near the origin, suggesting a more uniform fraud pattern. Key inferences:

- PC1 captures the dominant fraud-related pattern (high transaction amounts or unusual location behaviour).
- PC2 captures timeframe anomalies.
- Cluster 1 represents high-risk transactions with multiple active flags.
- Cluster 0 represents lower-risk transactions flagged primarily on timeframe.
- Cluster 2 represents moderate-risk transactions with a mix of behavioural anomalies.

<img width="635" alt="Screenshot 2025-03-30 at 20 54 49" src="https://github.com/user-attachments/assets/4a2dea8e-0414-4242-aec3-fea7263dda66" />
<img width="758" alt="image" src="https://github.com/user-attachments/assets/ae4cf864-7a14-4162-adb9-8a7abb9038d2" />

DBSCAN clustering produced a similar spatial distribution to the PCA plot, confirming that the PCA transformation preserved the key fraud patterns and that the clusters reflect genuine behavioural groupings rather than noise.

<img width="635" alt="image" src="https://github.com/user-attachments/assets/437ab961-82f8-443b-8a0d-c1681ca0e819" />

---

A Fraud Risk Score was computed using the Euclidean distance from the origin in PCA space, providing a continuous, quantitative measure of how anomalous each transaction is. Transactions further from the centre represent more extreme combinations of fraud indicators. Transactions with a risk score above 0.8 were classified as high risk. The distribution of scores shows that the vast majority of transactions have scores below 0.2.

<img width="641" alt="image" src="https://github.com/user-attachments/assets/06d57c90-4e83-42a7-a1e2-3161cf9048c5" />

Three transactions received a Fraud Risk Score above 0.8, each falling into Cluster 2. Despite having only a single suspicious flag each, these transactions were identified as the highest-risk cases — demonstrating the value of the risk scoring approach, which surfaces extreme outliers that simple flag-counting would overlook.

---

## Findings

### What are the characteristics of fraudulent transactions?

The project explores the key characteristics of potentially fraudulent transactions using engineered features: Suspicious_Amount, Suspicious_Location, and Suspicious_Timeframe. PCA reduced these indicators into components highlighting underlying patterns in suspicious behaviour. PC1 revealed a contrast between unusually high transaction amounts and very short timeframes — both frequently associated with fraudulent activity. Cluster analysis grouped transactions with similar behaviours, identifying consistent patterns seen across fraud types.

### How can we profile customers at risk of fraudulent activity?

High-risk customer profiling was performed by aggregating suspicious activity across individual accounts. A Total_Flags score was created by summing the binary flags for each suspicious behaviour type per account. Accounts with high cumulative scores were flagged as potentially high-risk. Additionally, the Fraud Risk Score provided a scalable, quantitative measure for prioritising accounts based on the extremity of their behaviour in PCA space. This approach identified customers who consistently engage in patterns resembling known fraud profiles.

### Are there any identifiable trends within fraudulent transactions?

PCA and clustering revealed visible trends. Fraud-related transactions tend to cluster at high PC1 values, indicating behaviours such as large amounts combined with rapid repeat transactions. K-Means and DBSCAN both produced consistent cluster structures, strengthening the evidence of recurring fraud patterns. Visualisations in 2D and 3D PCA space made these trends interpretable.

### How effective is the outlined process in identifying fraudulent transactions?

The process proved effective at surfacing transactions with fraud-like characteristics without relying on pre-labelled data. The combination of feature engineering, dimensionality reduction, clustering, and risk scoring provided a multi-layered detection approach. High-risk clusters aligned with top-scoring transactions, demonstrating that the methods worked cohesively. While not a formal classification model, the approach functions as an unsupervised anomaly detection pipeline suitable for early detection and triage. Validation against labelled data would strengthen confidence in its predictive capability.

---

## Conclusion

This project demonstrates how unsupervised learning techniques — specifically PCA combined with clustering algorithms — can be used to detect potentially fraudulent bank transactions without labelled data. By engineering features capturing suspicious amounts, unusual locations, and abnormal timeframes, the analysis highlighted behaviours that deviate from normal transaction patterns.

PCA enabled dimensionality reduction and clearer visualisation of fraud patterns. When clustering was applied in this transformed space, distinct transaction groups emerged with varying risk profiles. Cluster 0 showed minimal red flags, suggesting largely legitimate behaviour, while Clusters 1 and 2 exhibited high rates of suspicious timeframes, locations, and monetary values, indicating different forms of potentially fraudulent activity.

The Fraud Risk Score — based on Euclidean distance from the origin in PCA space — provided a simple but interpretable metric for ranking transactions by risk and added a quantitative layer to complement the rule-based flagging approach.

Overall, this project presents a practical and scalable foundation for fraud detection, offering data-driven insights that can enhance existing monitoring efforts. With further tuning and automation, the framework could be extended to real-time applications and continuous fraud prevention.

---

## About This Project

This analysis was completed as an independent portfolio project to develop practical skills in financial data analysis, anomaly detection, and applied machine learning. The methodology — rule-based feature engineering, PCA, K-Means clustering, DBSCAN, and fraud risk scoring — reflects standard approaches used in fraud analytics and quantitative risk.

The full Python implementation is available in [`fraudDetection.ipynb`](./fraudDetection.ipynb).
