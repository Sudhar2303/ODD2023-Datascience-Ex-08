# Ex-08-Data-Visualization-
# AIM
To Perform Data Visualization on a complex dataset and save the data to a file.

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
## STEP 1
Read the given Data

## STEP 2
Clean the Data Set using Data Cleaning Process

## STEP 3
Apply Feature generation and selection techniques to all the features of the data set

## STEP 4
Apply data visualization techniques to identify the patterns of the data.

# CODE
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files
uploaded = files.upload()
df=pd.read_csv("SuperStore.csv",encoding='unicode_escape')
df
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/13be9ecc-c84b-431f-8290-dd96de44fc2c)
```
df.isnull().sum()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/ec6264e2-da86-4a4b-9a52-52335a1c2afc)
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/e579b951-7408-4af6-a606-87ac1daf46df)
```
#detecting and removing outliers in current numeric data
plt.figure(figsize=(8,8))
plt.title("Data with outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/742d42c5-4d31-4f89-b541-73758f737f97)
```
plt.figure(figsize=(8,8))
cols = ['Sales','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/96cd2c53-360a-4def-87d0-7509983c6c67)

## Which Segment has Highest sales?
```
sns.lineplot(x="Segment",y="Sales",data=df,marker='o')
plt.title("Segment vs Sales")
plt.xticks(rotation = 90)
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/2c101351-1313-4241-98b8-88ac906afb0d)
```
sns.barplot(x="Segment",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/c1589a1c-27ec-4105-bfd7-165e61a9df11)

## Which City has Highest profit?
```
df.shape
df1 = df[(df.Profit >= 60)]
df1.shape
```
```
plt.figure(figsize=(30,8))
states=df1.loc[:,["City","Profit"]]
states=states.groupby(by=["City"]).sum().sort_values(by="Profit")
sns.barplot(x=states.index,y="Profit",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("City")
plt.ylabel=("Profit")
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/5b56fcac-cbd7-4d41-83b8-fb78efec1641)

## Which ship mode is profitable?
```
sns.barplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/93df2be8-b5b1-46bd-aa5d-08b5364c7bd2)
```
sns.lineplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/167a1831-9d8f-40b9-891e-b2fdae4a8fdb)
```
sns.violinplot(x="Profit",y="Ship Mode",data=df)
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/1e84c8f6-ed92-4eea-aef3-2b47e48028d1)
```
sns.pointplot(x=df["Profit"],y=df["Ship Mode"])
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/5ab4b8ac-ec98-4cc4-a421-e59b0d7e5fe1)
## Sales of the product based on region.
```
states=df.loc[:,["Region","Sales"]]
states=states.groupby(by=["Region"]).sum().sort_values(by="Sales")
sns.barplot(x=states.index,y="Sales",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("Region")
plt.ylabel=("Sales")
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/c22e7e79-a144-4269-8f31-9dd4cbfa65de)
```
df.groupby(['Region']).sum().plot(kind='pie', y='Sales',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/ab24f48e-2bb4-4a22-99fd-738ff6a49bb3)

## Find the relation between sales and profit.
```
df["Sales"].corr(df["Profit"])
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/53ef4919-ec6e-4d67-8294-dbf89f85ee13)
```
df_corr = df.copy()
df_corr = df_corr[["Sales","Profit"]]
df_corr.corr()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/8e7735ff-b4ee-4304-84f5-2db0d6dd8738)
```
sns.pairplot(df_corr, kind="scatter")
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/b4eabbdf-22d6-4412-8f51-0cb1fe976cec)
## Heatmap
```
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()

```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/3fd03c1b-1882-4608-adf1-218e82d7087c)
## Find the relation between sales and profit based on the following category.

### Segment
```
grouped_data = df.groupby('Segment')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/dd931f9c-4f03-4e8a-bda7-2a7e3b07684d)

### City
```
grouped_data = df.groupby('City')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('City')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/65bd2936-f2d3-44f3-9743-dbfc68b26dde)
### States
```
grouped_data = df.groupby('State')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('State')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/2b8fe255-02e7-46a1-9352-d0a857924435)
### Segment and Ship Mode
```
grouped_data = df.groupby(['Segment', 'Ship Mode'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index='Segment', columns='Ship Mode', values=['Sales', 'Profit'])
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
pivot_data.plot(kind='bar', ax=ax)
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
plt.legend(title='Ship Mode')
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/3a764bf8-f836-4d0c-8ddd-702fd71d98d9)
### Segment, Ship mode and Region
```
grouped_data = df.groupby(['Segment', 'Ship Mode','Region'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index=['Segment', 'Ship Mode'], columns='Region', values=['Sales', 'Profit'])
sns.set_style("whitegrid")
sns.set_palette("Set1")
pivot_data.plot(kind='bar', stacked=True, figsize=(10, 5))
plt.xlabel('Segment-Ship Mode')
plt.ylabel('Value')
plt.legend(title='Region')
plt.show()
```
![image](https://github.com/Sudhar2303/ODD2023-Datascience-Ex-08/assets/133684710/480cb84a-2976-4ed4-9c7b-ecc90daa6dad)

# RESULT:
Thus, Data Visualization is performed on the given dataset and save the data to a file.
