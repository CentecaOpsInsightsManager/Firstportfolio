# Customer Behaviour Segmentation Using K-Means

## Exec Summary

Business problems and purpose: This project investigated how customer purchasing and engagement data could identify behavioural personas and support more targeted marketing activity.
Approach: Following data-quality assessment and transformation, K-means clustering was applied to standardised behavioural variables.
Main findings: Three customer personas were identified: Loyal Repeat Customers, High-Value Occasional Purchasers and Lower-Engagement Customers.
Model evaluation: Excluding age produced stronger cluster separation, with a maximum silhouette score of 0.37 compared with 0.26 when age was included.
Meaning of the findings: Behavioural characteristics provided a more useful basis for customer segmentation than age within this dataset. Lower-Engagement Customers formed the largest group, presenting the broadest opportunity for targeted activity intended to improve engagement and satisfaction.
Next steps and recommendations: Cluster profiles should be integrated into the customer database and refreshed periodically to monitor changes in customer behaviour.
Stakeholder considerations: Marketing stakeholders should measure changes in spending, engagement and satisfaction to establish realised value. Human oversight should also be maintained to prevent inferred personas from creating unfair or fixed customer classifications.


## Business Problem

Using the public dataset (Banerjee, 2023), the business problem was to identify behavioural profiles within the customer base so that marketing can improve inefficient promotional spending and target missed revenue opportunities. A K-means clustering model was used to identify customer profiles based on spending behaviour, purchase frequency, satisfaction and engagement.

K-means was selected because the business problem is identifying customer personas without an existing target label. Unlike supervised machine learning models, K-means can identify natural groupings using similarities across customer behavioural features. It was suitable for the numerical, transformed and standardised dataset and, as the report will explain, produced the personas required for the marketing team. Alternative clustering approaches may be suitable for irregular or overlapping groups (e.g. Hierarchical, DBSCAN or HDBSCAN), but K-means offered an appropriate balance of simplicity, interpretability and alignment with the project objective.

Afwan et al. (2024) also found that customer persona segmentation using K-Means clustering can support more targeted marketing strategies.


## Tools and Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Microsoft Fabric

## ETL and Structure

The project was completed within the Operational Insight Manager’s (OIM’s) restricted system access using Microsoft Fabric and Python, supported by Pandas and NumPy (Figure 1 and 9).

Microsoft Excel was considered, but Python was selected because it better supported repeatable preprocessing and machine-learning workflows.

To ensure the public dataset was a robust set of data and followed data governance guidelines, specifically data quality, the OIM followed the DAMA-DMBOK Framework (DAMA International, n.d.). These tests consisted of checking for null values, duplicates and any distribution anomalies (Figures 2-5).  The OIM used DAMA instead of the UK Government Data Quality Framework, as this is what is practised within the business.

The dataset was considered to be of a high standard. However, Figure 5 shows positive skew in transaction value and zero values in purchase frequency, which could have affected model performance.

To address these issues, transformations were applied (Figures 6–10). A constant of one was added to avoid zero values while preserving ordering and pairwise differences. A logarithmic transformation reduced positive skew and the influence of extreme values. Finally, behavioural features were created for modelling.

Following transformation, the distribution was re-evaluated. Figure 11 shows reduced skew in previous-purchase amount, making the feature more suitable for distance-based clustering.

## Analysis

The transformations had created five behavioural variables and a static attribute of age. Two models were therefore compared to assess the effect of including age (Figures 12–13).

The behavioural and static variables were standardised using StandardScaler to prevent scale-related bias, which is important to ensure more accurate results (Figures 14- 15).

To understand the number of clusters to use within the model, an elbow test and silhouette analysis were performed. This is the standard inertia-based elbow technique, with a silhouette scoring used as a supporting diagnostic. Other alternatives like automated knee detection and Calinski-Harabasz index were considered, however, elbow and silhouette analyses were considered sufficient because they provided interpretable evidence of diminishing improvement and cluster separation (Scikit-learn developers, n.d.-a).
The elbow method is run for both models, with Model 2 including age (Figure 16), both showing a reasonable bend at three clusters (K = 3) as shown in Figures 17 and 18, indicating at this point little difference between the two. 

Silhouette analysis was then conducted (Figure 19). Figure 20 shows stronger cluster separation without age, with a maximum score of 0.37 for Model 1 compared with 0.26 for Model 2.

Due to the results of both the elbow and silhouette a value of k = 3 was selected as the number of clusters as well as removal of age.

The fitted K-means model identified three distinct customer personas (Figure 21), highlighting the different behavioural characteristics of the customers within them.
The personas were decided based on the clusters themselves as shown in Figure 22, and are described as follows:

•	Cluster 0, “Loyal Repeat Customers,” had the highest average item rating, engagement score, and number of previous purchases. This suggests that customers in this cluster purchase more frequently and provide higher ratings than customers in the other two clusters. The cluster also had the highest average discount applied, indicating that these customers may be more responsive to discounted purchases. However, the difference in discount usage between the clusters was less pronounced than the differences in purchase frequency and engagement.

•	Cluster 1, “High-Value Occasional Purchasers,” had the highest recorded purchase amount and the highest engineered average-spend measure. This indicates that customers in this cluster tend to make higher-value purchases but purchase less frequently than Loyal Repeat Customers in Cluster 0. Consequently, the cluster had a lower engagement score than Cluster 0. However, because Cluster 1 had more previous purchases than Cluster 2, the term “occasional” is used comparatively rather than to suggest that these customers rarely purchase.

•	Cluster 2, “Lower-Engagement Customers,” had the lowest number of previous purchases, engagement score, item rating, and average discount applied. However, the cluster had a higher average-spend measure than Cluster 0, suggesting that these customers spend more per purchase than Loyal Repeat Customers despite purchasing less frequently. The combination of lower purchase frequency, lower ratings, and lower engagement supports the interpretation of this cluster as a lower-engagement customer persona.


To ensure that the correct representation of the data was used for the personas, Box plots of purchase amount and engagement were used to examine the distributions supporting the persona interpretations, as shown in Figure 27 and 28. 


A final test was done using a secondary model to test if age would make any impact on the model. Using the 3-cluster model while including the age variable results showed that they were extremely similar to the model without this variable, meaning the inclusion of age did not materially improve cluster separation in the tested specification as shown in Figure 24. 


## Results & Recommendations

With the conclusion of categorising the three customer personas, lists of the amount of each persona were formulated (Figure 23 and 25). The results showed that cluster 2, “Lower-Engagement Customers”, contained the largest proportion of customers, providing the broadest group for targeted marketing activity.

To help visualise this, a column chart was built, clearly showing the larger amount of cluster 2, as shown in Figure 26. 

Now that the customers have been split into 3 clusters, the first recommendation would be to integrate the model into the customer database, so that each present and future customer would have a profile assigned which would support targeted marketing.

It would also be advisable to rerun the model on a defined schedule to monitor cluster drift and changes in customer behaviour. Conducting benefit realisation by seeing an increase in the specific clusters spend and satisfaction can also be achieved afterwards, to ensure the marketing strategy is having an effect. 
It is important that the schedule is set at an appropriate time to allow the data to grow sufficiently enough as using data with only a small number of sales could lead to false conclusions or the K-Means to cluster ineffectively. 
Lastly in using a model to determine customer persona target marketing, implementation should consider the risk that inferred personas could produce unequal offers, reinforce proxy bias or become treated as fixed customer identities. Profiles should therefore be reviewed periodically and used with human oversight. Naz and Kashif (2025) argue that the use of Artificial Intelligence (AI) in predictive marketing raises important ethical concerns relative to bias, market concentration and consumer manipulation.



