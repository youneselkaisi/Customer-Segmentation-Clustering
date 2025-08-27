# Customer Segmentation for Targeted Marketing

## Project Overview
This project focuses on analyzing customer shopping trends and behaviour to identify distinct segments for **targeted marketing**. By applying clustering algorithms to real-world retail data, we aimed to uncover actionable insights that help businesses tailor promotions, increase engagement, and boost sales. The entire workflow was implemented in **KNIME**, a user-friendly, visual data analytics platform that allows easy integration of data prep, modeling, and visualization. KNIME is beneficial for its drag-and-drop interface, reproducibility, and seamless integration with various data sources.

## Instructions

You may have to download and import the dataset into the **CSV Reader node** for the workflow to run. Right-click the node, then browse files, and insert.


## Dataset

The dataset used for this project is **[Shopping Trends and Customer Behaviour](https://www.kaggle.com/datasets/sahilislam007/shopping-trends-and-customer-behaviour-dataset/data)** from Kaggle, containing **3,900 records and 16 attributes**.  

Key features include:  
- **Demographics:** Age, Gender  
- **Purchasing behaviour:** Product categories, Purchase amounts, Discounts, Purchase frequency  
- **Marketing interactions:** Subscription status, engagement metrics  

The dataset provides a rich foundation for analyzing consumer preferences, trends, and segment patterns. No significant outliers or missing values were observed in critical fields such as Age and Purchase Amount. Exploratory analysis revealed a median age of 44, median spending of $60, and a male predominance of 68%. Apparel emerged as the most purchased category, with most purchases occurring quarterly or annually.



## Data Exploration

We performed comprehensive data exploration to understand patterns and distributions:  
- Summary statistics for numeric and categorical features  
- Visualizations for demographic distributions and spending patterns  
- Correlation analysis to uncover relationships between variables  
- Identification of trends in subscription behaviour and purchase frequency  

**Summary Stats**

<img width="700" height="196" alt="image" src="https://github.com/user-attachments/assets/f6359fe6-83ba-4593-b701-d57a931beb5a" />


**Age and Purchase Amount box plots**


<img width="800" height="550" alt="image" src="https://github.com/user-attachments/assets/27e46580-e3a3-4ba4-a440-2de4957632de" />


**Items purchased by category**

<img width="750" height="550" alt="image" src="https://github.com/user-attachments/assets/84a6e057-49ae-4866-9baf-cb95df8b7dbd" />



**Frequency of purchases**

<img width="750" height="600" alt="image" src="https://github.com/user-attachments/assets/ce893a49-7e4a-45fd-9e73-16126fe51ccc" />


**Age distribution**

<img width="750" height="600" alt="image" src="https://github.com/user-attachments/assets/d84189fe-9009-40fa-8e4e-41002db094fd" />


**Gender breakdown**

<img width="700" height="550" alt="image" src="https://github.com/user-attachments/assets/a3438734-29bd-4755-975b-15eb0b97baf0" />



## Data Preparation

To prepare the data for clustering algorithms, the following steps were performed:  
- Median value imputation for any missing Age or Purchase Amount data  
- Removal of ineffective or redundant columns such as IDs  
- Conversion of categorical data into numerical form for modeling  
- Data shuffling to avoid sequence bias  
- Standardization using Z-score normalization  
- Dimensionality reduction with PCA for visualization purposes  

**Data prep workflow**

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/ca8b3ecb-12a1-4614-a9df-42143cbf254d" />



## Modeling

To segment customers effectively, we implemented three clustering techniques, each offering unique insights and advantages for different data characteristics. The goal was to uncover meaningful customer segments that could guide targeted marketing strategies.


- **K-Means Clustering:**  
  K-Means is a centroid-based algorithm that partitions the dataset into k clusters by minimizing the within-cluster sum of squared distances. It is highly efficient for large datasets and works well when clusters are roughly spherical and of similar size. For this project, we selected 3 clusters based on exploratory data analysis and PCA visualization of the feature space.  

  Parameters used:  
  - Number of clusters: 3  
  - Initialization method: k-means++  
  - Maximum iterations: 300  

  K-Means allowed us to identify distinct customer groups based on purchasing behaviour, subscription patterns, and demographic attributes.

<img width="700" height="550" alt="image" src="https://github.com/user-attachments/assets/f73edd0d-ba2b-422c-bab8-fc87b1c62945" />


- **Hierarchical Clustering:**  
  Hierarchical clustering builds a nested tree of clusters, called a dendrogram, which helps visualize similarities between customers at various levels of granularity. We used agglomerative clustering with Ward linkage to minimize the variance within clusters. This approach produced 2 main clusters after sampling and applying PCA for dimensionality reduction.  

  Parameters used:  
  - Linkage method: Ward  
  - Number of clusters extracted: 2  
  - Dimensionality reduction: PCA applied before clustering  

  The dendrogram provided insights into hierarchical relationships between customers, highlighting subgroups that shared similar purchase frequency, discount usage, and product preferences.


<img width="700" height="550" alt="image" src="https://github.com/user-attachments/assets/73d7afb9-8328-455b-89a1-eecd0ce72dab" />


<img width="900" height="600" alt="image" src="https://github.com/user-attachments/assets/04a723f8-bfc4-40da-9ad9-c53e86d9096e" />


- **DBSCAN (Density-Based Spatial Clustering of Applications with Noise):**  
  DBSCAN is a density-based algorithm that groups points closely packed together while marking points in low-density regions as outliers. This method is particularly effective for detecting clusters of arbitrary shape and identifying noise in the data.  

  Parameters used:  
  - Epsilon (eps): 3  
  - Minimum points (minPts): 5  

  DBSCAN allowed us to isolate irregular clusters and outlier customers who exhibited unusual purchasing patterns, such as extremely high discount usage or seasonal-only purchasing behavior.


<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/fe948b34-ef90-4336-92b5-f9a736a193d0" />



Each algorithm offered complementary insights: K-Means captured general cluster centers and size distributions, hierarchical clustering revealed nested customer relationships, and DBSCAN highlighted unusual customer behaviors and noise. 



## Model Evaluation

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/0dd5027a-b3a8-4511-9dd3-8167338f3d7a" />

- Overall clusters were reasonably separate & distinct for analysis
- However, scores were mostly lackluster, clusters weren’t very compact + noise
- Hierarchical provided best score with 0.19 followed by k-means at 0.12
- DBSCAN score was negative and didn’t provide much insight, but was useful for identifying noise 

**Insights (based on k-means clustering)**

After running the clustering algorithms, we filtered the dataset by each cluster to examine the behaviors, demographics, and purchasing patterns of the customers within that segment. By analyzing these patterns, we were able to identify actionable insights for each cluster and make targeted recommendations to improve marketing strategies.


<img width="267" height="283" alt="image" src="https://github.com/user-attachments/assets/6207bf76-45ef-4c57-9264-95bd6ccfb450" />


- Cluster 0 (Yellow) → Non-subscribers, use discounts, prefer faster shipping (express/2-day), 3:2 women to men. Men favor sneakers and hoodies, women favor sunglasses, jewelry, and sandals.  
  - Actions:  
    - Gender-specific promotions  
    - Express delivery perks  
    - Incentivize subscriptions (e.g., "1st month free")

- Cluster 1 (Red) → Only men, 63% subscribed, no discounts used, slightly above average spend, mostly credit card users, prefer express shipping.  
  - Actions:  
    - Loyalty perks for high spenders and ongoing subscriptions  
    - Promote full-price, quality male products  
    - Highlight new arrivals and luxury clothing

- Cluster 2 (Purple) → 100% discount users, low-to-moderate spend, seasonal purchase peaks (holidays), infrequent/occasional buyers, 56% women, purchase patterns similar to Cluster 0.  
  - Actions:  
    - Seasonal discount campaigns (e.g., "Holiday deals await!")  
    - Offer discounted bundles (BOGO)  
    - Incentivize account creation and discounted subscriptions



## Deployment

The customer segments identified through clustering can directly guide strategic marketing initiatives and business decisions:

1. **Customized email and direct mail campaigns:** Each segment can receive tailored messages that appeal to their preferences. For example, cluster 0 (non-subscribers using discounts) could receive emails highlighting introductory offers or first-month subscription discounts, while cluster 1 (high-spending male subscribers) could get updates on premium products and loyalty rewards.

2. **Personalized digital marketing and landing pages:** Website content, advertisements, and product recommendations can be dynamically adjusted based on segment behaviour. For instance, cluster 2 (seasonal discount shoppers) could see banners and landing pages promoting holiday deals or bundled discounts during peak shopping periods.

3. **Targeted discount offers and promotions:** Discounts, loyalty points, and promotional campaigns can be strategically deployed for maximum impact. Cluster-specific offers ensure that promotions are relevant, e.g., “Buy One Get One” campaigns for cluster 2, and premium product bundles for cluster 1.

4. **Integration into recommendation engines and analytics:** Segment data can feed into recommendation systems, improving product cross-selling and upselling strategies. By tracking purchase patterns within each cluster, businesses can better predict product interests, optimize inventory, and enhance overall customer lifetime value.

5. **Operational and strategic decision support:** Beyond marketing, segment insights can guide inventory planning, supply chain prioritization, and customer service customization. For example, products preferred by high-value clusters can be stocked proactively, and support resources can be aligned with cluster-specific needs (e.g., fast shipping for cluster 0).


## Use Cases

This segmentation framework can be leveraged by:  
- **Retailers**: To design targeted promotions and subscription incentives  
- **E-commerce platforms**: To enhance recommendation systems based on segment preferences  
- **Marketing teams**: To tailor campaigns for specific customer behaviours  
- **Data analysts**: To uncover trends and evaluate the effectiveness of past campaigns  


## Complete KNIME Workflow

<img width="900" height="757" alt="image" src="https://github.com/user-attachments/assets/3e2557d9-e9e6-418a-9066-1fb469699544" />


## Conclusion

Through clustering, we effectively segmented customers based on demographics and behavioural data, offering actionable insights for **targeted marketing** and improved ROI. While silhouette scores were modest, the results provide a solid foundation for future work. Future improvements could include larger datasets, hybrid clustering methods, parameter tuning, and more detailed behavioural indicators.



## Acknowledgments

We would like to thank **Professor Amit Agrawal** for guidance and support throughout the project. Additional thanks to my team members Yassin Elhakeem and Niko Jurincic for their collaboration, and to Kaggle for providing the dataset. The project also benefited from discussions on data preparation, model selection, and visualization techniques.



