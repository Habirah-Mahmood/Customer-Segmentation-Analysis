# Customer Segmentation Anlaysis
## Project Overview and Objective
In this data Analysis project, I get to perform customer segmentation analysis for an e-commerce company. 
I will group customers into distinct segments based on their social behavior and purchase patterns, extract some insights 
and use these insights to make informed decisions on targeted marketing strategies, improve customer satisfaction, and enhance overall business strategies.

## Data Source
The data set was downloaded from kaggle as a csv file.

## Tools 
- Pandas (Explaratory Data Analysis and other descriptive Analysis)
- Matplotlib (Data Visualization)
- Seaborn (Data Visualization)
- K-means modelling (Cluster Formation)

## Explatory Data Analysis
EDA involved exploring the data to answer key questions such as;
1. Checking for Null-values
   ```Pandas
   df.isna().sum()
   ```
2. Checking data types for each column
     ```
   df.info()
   ```
3. Finding number of unique entries for each column
  ```Pandas
   df.nunique()
  ```
## Descriptive Analysis
1. Calculating Mean, Frequency, Standard deviation and median for different columns
```Pandas
df.derscibe()
```
2. Calculating Modal Values
```Pandas
df.mode().dropna()
```
## Cluster Fromation.
1. I used the the Standardscaler to standardise my scales   
```from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
cols_to_cluster = ['Income', 'MntTotal', 'In_relationship', 'Education_status']
df_scaled = df.copy()
df_scaled[cols_to_cluster] = scaler.fit_transform(df[cols_to_cluster])
```
2. I then picked a range of values (1-10), and used the Elbow method to find the most suitable number of clusters
 ```X = df_scaled[cols_to_cluster]
inertia_list = []
for k in range(1,11):
    inertia = KMeans(n_clusters=k , n_init=10).fit(X).inertia_
    inertia_list.append(inertia)
```
**Visualization of the Elbow plot**

![1  Visualization of elbow plot](https://github.com/user-attachments/assets/91031b01-69c5-45f8-bd0d-8080e29864ee)

3. I then formed clusters based on the recommended number of clusters, below is a visualization

**Clustter Visualization**

![2  cluster visualization](https://github.com/user-attachments/assets/322be17c-4309-4ae3-b11d-603f7a2ca0f6)

## Cluster Analysis
1. Finding the population size of each cluster
```
customer_num = df_scaled.groupby('Cluster')['MntTotal'].count().reset_index()
```
**A bar plot of Number of customers per cluster**

![3  A bar plot of Number of customers per cluster](https://github.com/user-attachments/assets/743d1ef3-89e4-4c9d-9dda-a71cbe15268b)

2. Average income per cluster
```
df_clustered['Avg_income'] = df_clustered.groupby('Cluster')['Income'].mean()
```
**Visual representation of Average income per cluster**

![4  Visual representation of Average income per cluster](https://github.com/user-attachments/assets/2075281f-ee3a-44a0-99b4-1035a08152f0)

3. Average Product Consumption per cluster
```
Avg_Consumption = df_clustered.groupby('Cluster')[['MntWines', 'MntFruits', 'MntMeatProducts', 'MntFishProducts', 'MntSweetProducts','MntGoldProds', 'MntTotal']].mean().reset_index()
Avg_Consumption
```
**A bar plot showing Average amount of each product consumed by each Cluster**

![5  a bar representation of](https://github.com/user-attachments/assets/0dbacd56-1fba-4a07-ab84-ced5dbff282c)

## Recommendations
1. **Cluster 0**; This cluster has the highest number of customers belonging to it, but the mean Income is second lowest. They have also been showed to spend the least on the different Products. More marketing targetted towards this cluster should be done and also they should be offered trade discounts to encourage them to buy more as the cluster has numbers and therefore the opportunity to give the business more sales.

2. **Cluster 1**; Despite having the smallest population, the customers from this custer have the highestest purchasing power and also earn the seconf highest income on average. Clients from this have a minimum of Secondary education. With the desire to purchase and fairly high income. The business should focus on retaining the clients in this cluster through discounts, targetted marketing and running promotions.

3. **Cluster 2**; Customers within this cluster have the second highest purchasing power however much the average income is the least. The mininimum level of Education is also 2. These clients are limited but their income but are a great group to target at the beginning/end of the month to maximise sales.

4. **Cluster 3**; This cluster earns the highest income but their desire to purchase is just low. This could be due to failure of the business to sufficiently influence these customers. The business should therefore try to convert these clients into paying customers as they have a huge potential through offers, special discounts etc.

In conclusion, each cluster presents unique opportunities for growth. By targeting Cluster 0’s numbers, retaining Cluster 1’s high-value customers, strategically timing offers for Cluster 2, and converting Cluster 3’s high earners, the business can maximize sales, improve engagement, and optimize marketing strategies effectively.
