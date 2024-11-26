# Workshop: Data Cleaning and Data Analysis

## Aim
The aim of this workshop is to equip participants with the fundamental skills and techniques needed for data cleaning and data analysis using Python. Participants will learn how to preprocess data, handle missing values, and perform basic exploratory data analysis (EDA) to extract insights from datasets.

## Procedure
1. **Introduction to Data Cleaning**
   - Importance of data cleaning in data analysis.
   - Common data quality issues: missing values, duplicates, inconsistent formatting.

2. **Tools and Libraries**
   - Introduction to Python and key libraries: 
     - `pandas` for data manipulation.
     - `numpy` for numerical operations.
     - `matplotlib` and `seaborn` for data visualization.

3. **Data Cleaning Techniques**
   - Loading datasets using `pandas`.
   - Identifying and handling missing values.
   - Removing duplicates.
   - Formatting and transforming data.

4. **Data Analysis**
   - Exploratory Data Analysis (EDA) techniques.
   - Visualizing data distributions and relationships.
   - Summary statistics and insights extraction.

5. **Hands-on Practice**
   - Participants will work on a sample dataset to apply data cleaning and analysis techniques learned.

## Program

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
data = pd.read_csv('/supermarket.csv')  # Replace with your actual file path

# 1. Perform Data Cleaning Process
print("Initial Data:")
print(data.head())
print("\nMissing Values:")
print(data.isnull().sum())

# Fill missing values for numerical columns with the mean
for col in data.select_dtypes(include=[np.number]).columns:
    data[col].fillna(data[col].mean(), inplace=True)

# Drop rows with missing values in significant categorical columns
# You can choose any significant column that makes sense for your data
data.dropna(subset=['Customer type'], inplace=True)  # Example column to drop NaN

# Remove duplicates
data.drop_duplicates(inplace=True)

print("\nCleaned Data:")
print(data.head())
print("\nMissing Values After Cleaning:")
print(data.isnull().sum())

# 2. Implement Boxplot Method to Detect Outliers
plt.figure(figsize=(12, 6))
sns.boxplot(data=data['Unit price'])  # Replace 'Unit price' with the column you want to analyze
plt.title('Boxplot to Detect Outliers for Unit Price')
plt.show()

# 3. Implement IQR Method to Remove Outliers
# Calculate the IQR for the chosen numerical column
Q1 = data['Unit price'].quantile(0.25)
Q3 = data['Unit price'].quantile(0.75)
IQR = Q3 - Q1

# Define the limits for outliers
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Filter the data to remove outliers
data_filtered = data[(data['Unit price'] >= lower_bound) & (data['Unit price'] <= upper_bound)]

print("\nFiltered Data Shape (Outliers Removed):")
print(data_filtered.shape)

# 4. Implement Count Plot Method for Univariate Analysis
plt.figure(figsize=(12, 6))
sns.countplot(x='Customer type', data=data_filtered)  # Replace 'Customer type' with the column to analyze
plt.title('Count Plot for Customer Type')
plt.xticks(rotation=45)
plt.show()

# 5. Implement DistPlot Method for Multivariate Analysis
plt.figure(figsize=(12, 6))
sns.histplot(data=data_filtered, x='Total', hue='Gender', kde=True, multiple="stack")  # Replace 'Total' and 'Gender'
plt.title('Distribution Plot for Total by Gender')
plt.show()
```
# Coding Output:
```
Initial Data:
    Invoice ID Branch       City Customer type  Gender  \
0  750-67-8428      A     Yangon        Member  Female   
1  226-31-3081      C  Naypyitaw        Normal  Female   
2  631-41-3108      A     Yangon        Normal    Male   
3  123-19-1176      A     Yangon        Member    Male   
4  373-73-7910      A     Yangon        Normal    Male   

             Product line  Unit price  Quantity   Tax 5%     Total       Date  \
0       Health and beauty       74.69         7  26.1415  548.9715   1/5/2019   
1  Electronic accessories       15.28         5   3.8200   80.2200   3/8/2019   
2      Home and lifestyle       46.33         7  16.2155  340.5255   3/3/2019   
3       Health and beauty       58.22         8  23.2880  489.0480  1/27/2019   
4       Sports and travel       86.31         7  30.2085  634.3785   2/8/2019   

    Time      Payment    cogs  gross margin percentage  gross income  Rating  
0  13:08      Ewallet  522.83                 4.761905       26.1415     9.1  
1  10:29         Cash   76.40                 4.761905        3.8200     9.6  
2  13:23  Credit card  324.31                 4.761905       16.2155     7.4  
3  20:33      Ewallet  465.76                 4.761905       23.2880     8.4  
4  10:37      Ewallet  604.17                 4.761905       30.2085     5.3  

Missing Values:
Invoice ID                 0
Branch                     0
City                       0
Customer type              0
Gender                     0
Product line               0
Unit price                 0
Quantity                   0
Tax 5%                     0
Total                      0
Date                       0
Time                       0
Payment                    0
cogs                       0
gross margin percentage    0
gross income               0
Rating                     0
dtype: int64

Cleaned Data:
    Invoice ID Branch       City Customer type  Gender  \
0  750-67-8428      A     Yangon        Member  Female   
1  226-31-3081      C  Naypyitaw        Normal  Female   
2  631-41-3108      A     Yangon        Normal    Male   
3  123-19-1176      A     Yangon        Member    Male   
4  373-73-7910      A     Yangon        Normal    Male   

             Product line  Unit price  Quantity   Tax 5%     Total       Date  \
0       Health and beauty       74.69         7  26.1415  548.9715   1/5/2019   
1  Electronic accessories       15.28         5   3.8200   80.2200   3/8/2019   
2      Home and lifestyle       46.33         7  16.2155  340.5255   3/3/2019   
3       Health and beauty       58.22         8  23.2880  489.0480  1/27/2019   
4       Sports and travel       86.31         7  30.2085  634.3785   2/8/2019   

    Time      Payment    cogs  gross margin percentage  gross income  Rating  
0  13:08      Ewallet  522.83                 4.761905       26.1415     9.1  
1  10:29         Cash   76.40                 4.761905        3.8200     9.6  
2  13:23  Credit card  324.31                 4.761905       16.2155     7.4  
3  20:33      Ewallet  465.76                 4.761905       23.2880     8.4  
4  10:37      Ewallet  604.17                 4.761905       30.2085     5.3  

Missing Values After Cleaning:
Invoice ID                 0
Branch                     0
City                       0
Customer type              0
Gender                     0
Product line               0
Unit price                 0
Quantity                   0
Tax 5%                     0
Total                      0
Date                       0
Time                       0
Payment                    0
cogs                       0
gross margin percentage    0
gross income               0
Rating                     0
dtype: int64
```

![image](https://github.com/user-attachments/assets/de36d3be-29fa-4108-be21-7fe4e81a6da3)

![image](https://github.com/user-attachments/assets/a19c7784-f371-4401-922a-6bd2b198684d)

![image](https://github.com/user-attachments/assets/e5b2b1fd-2ab0-48d0-8101-0fbc71556aee)


# Result:

Hence, data cleaning resulted in 920 entries after removing outliers from the Unit price, with visualizations showing customer type distributions and total sales by gender.
