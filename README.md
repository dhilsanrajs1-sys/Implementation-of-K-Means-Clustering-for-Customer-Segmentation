# Implementation-of-K-Means-Clustering-for-Customer-Segmentation

## AIM:
To write a program to implement the K Means Clustering for Customer Segmentation.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Jupyter notebook

## Algorithm
1.Import the necessary packages using import statement.
2.Read the given csv file using read_csv() method and print the number of contents to be displayed using df.head().
3.Import KMeans and use for loop to cluster the data.
4.Predict the cluster and plot data graphs.
5.Print the outputs and end the program 

## Program:
```
/*
Program to implement the K Means Clustering for Customer Segmentation.
Developed by: DHILSANRAJ S
RegisterNumber: 212225230058 
*/
```
```
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

# Load the data
df = pd.read_csv('Mall_Customers (1).csv')

# Display first few rows
print("First 5 rows of data:")
print(df.head())
print("\n" + "="*50)

# Convert gender to numbers (Male=0, Female=1)
df['Gender'] = df['Gender'].map({'Male': 0, 'Female': 1})

# Select features for clustering
# Using Annual Income and Spending Score
X = df[['Annual Income (k$)', 'Spending Score (1-100)']]

# Standardize the data (make all values on similar scale)
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Apply K-Means with 5 clusters
kmeans = KMeans(n_clusters=5, random_state=42)
df['Cluster'] = kmeans.fit_predict(X_scaled)

# Plot the clusters
plt.figure(figsize=(10, 6))

# Plot each cluster with different color
colors = ['red', 'blue', 'green', 'orange', 'purple']
for i in range(5):
    cluster_data = df[df['Cluster'] == i]
    plt.scatter(cluster_data['Annual Income (k$)'], 
                cluster_data['Spending Score (1-100)'],
                color=colors[i], 
                label=f'Cluster {i}',
                alpha=0.6)

plt.xlabel('Annual Income (k$)')
plt.ylabel('Spending Score (1-100)')
plt.title('Customer Segments using K-Means')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()

# Simple analysis of each cluster
print("\nCLUSTER ANALYSIS:")
print("-" * 50)

for i in range(5):
    cluster_data = df[df['Cluster'] == i]
    print(f"\nCluster {i}:")
    print(f"  Number of customers: {len(cluster_data)}")
    print(f"  Average Income: ${cluster_data['Annual Income (k$)'].mean():.1f}k")
    print(f"  Average Spending Score: {cluster_data['Spending Score (1-100)'].mean():.1f}")
    print(f"  Average Age: {cluster_data['Age'].mean():.1f} years")
    
    # Gender breakdown
    males = len(cluster_data[cluster_data['Gender'] == 0])
    females = len(cluster_data[cluster_data['Gender'] == 1])
    print(f"  Gender: {males} Male, {females} Female")

# Save the results to a new CSV file
df.to_csv('customer_segments.csv', index=False)
print("\n" + "="*50)
print("Results saved to 'customer_segments.csv'")
```

## Output:
<img width="975" height="577" alt="image" src="https://github.com/user-attachments/assets/3ea632d8-3f3e-489a-acdc-3365745c42e9" />
<img width="1066" height="666" alt="image" src="https://github.com/user-attachments/assets/68839126-581c-48e1-bac6-eb5aaa2a4c51" />
<img width="1062" height="611" alt="image" src="https://github.com/user-attachments/assets/9fb40a3b-2f65-4ef7-87d9-08fbb4566918" />
<img width="788" height="226" alt="image" src="https://github.com/user-attachments/assets/a20b3c30-985a-4705-9a86-60c347c36989" />




## Result:
Thus the program to implement the K Means Clustering for Customer Segmentation is written and verified using python programming.
