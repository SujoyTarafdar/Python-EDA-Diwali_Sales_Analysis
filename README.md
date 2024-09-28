import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns

sales_df=pd.read_csv('Diwali Sales Data.csv',encoding='unicode_escape')

sales_df.head()

sales_df.tail()

sales_df.shape

sales_df.info()

## Checking for Null Values in Columns

sales_df.isnull().sum()

## Dropping the Null Columns 'Status and unnamed1'

sales_df.drop(['Status','unnamed1'],inplace=True,axis=1)

sales_df.isnull().sum()

## Dropping the Null values from Entire Data Set 

sales_df.dropna(inplace=True)

sales_df.isnull().sum()

## Changing Amount Column Data Type from Float to int 

sales_df['Amount']=sales_df['Amount'].astype('int')

## Rechecking Data type of Amount Column

sales_df.info()

## Another way to Check Data Type of Particular Column

sales_df['Amount'].dtype

##Checking for Column Names 

sales_df.columns

## Changing Column Name without using inplace or asssigning it to any variable

sales_df.rename(columns= {'Marital_Status':'Shaadi'})

## Showing that Column name is still as Marital-Status as we did not use Inplace or assigned it to another variable name 

sales_df

##Checking the Stats Values of Numerical Columns 

sales_df.describe()

# Using describe() for specific columns

sales_df[['Age', 'Orders', 'Amount']].describe()



## Gender wise Analysis

# Plotting a Bar Chart for Gender and it's Count to know Gender wise who has spent more on Shopping

ax = sns.countplot(x = 'Gender',data = sales_df)
plt.title('Gender Count for Amount Spent')

for bars in ax.containers:
    ax.bar_label(bars)

# Plotting a Bar chart for Gender vs Total Amount Spent


sales_by_gender = sales_df.groupby(['Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

sns.barplot(x = 'Gender',y= 'Amount' ,data = sales_by_gender)
plt.title('Gender vs Total Amount Spent')



## From above Graphs we can see that most of the Buyers are Females and even the Purchasing Power of Females are Greater than Men

## AGE wise Analysis

ax = sns.countplot(data = sales_df, x = 'Age Group', hue = 'Gender')

for bars in ax.containers:
    ax.bar_label(bars)

## Age wise Total Amount Spent on Shopping 

sales_age = sales_df.groupby(['Age Group'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

sns.barplot(x = 'Age Group',y= 'Amount',data = sales_age)
plt.title('Age Group Vs Total Amount Spent on Shopping')
plt.figure(figsize=(10,9))

## From the above Graphs we can see that most of the buyers are of Age Group between 26-35 Years

## State wise Analysis

# Top 10 Sates by Total Orders

sales_state = sales_df.groupby(['State'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)

plt.figure(figsize=(15,5))
plt.title('Top 10 Sates by Total Orders')
sns.barplot(data = sales_state, x = 'State',y= 'Orders')

# Total Amount/Sales from Top 10 states

sales_state = sales_df.groupby(['State'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)

plt.figure(figsize=(15,5))
plt.title('Total Amount/Sales from Top 10 states')
sns.barplot(data = sales_state, x = 'State',y= 'Amount')

## From the above Graphs its clear that Total Order and Total Amount Per Order is more by States Uttar Pradesh followed by Maharashtra and Karnataka

## Marital Status wise Analysis

ax = sns.countplot(data = sales_df, x = 'Marital_Status')

plt.figure(figsize=(10,6))
for bars in ax.containers:
    ax.bar_label(bars)   

## Marital Status wise Amount Spent on Shopping

sales_state = sales_df.groupby(['Marital_Status', 'Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

plt.figure(figsize=(6,5))
plt.title('Marital Status wise Amount Spent on Shopping')
sns.barplot(data = sales_state, x = 'Marital_Status',y= 'Amount', hue='Gender')

## From above graphs we can see that most of the buyers are married (women) and they have high Purchasing power

## Occupation wise Analysis

## Occupation wise Spents

plt.figure(figsize=(20,5))
plt.title('Occupation wise Count of Spending Capacity')
ax = sns.countplot(data = sales_df, x = 'Occupation')

for bars in ax.containers:
    ax.bar_label(bars)

##

sales_state = sales_df.groupby(['Occupation'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

plt.figure(figsize=(20,5))
plt.title('Occupation wise Total Spending Capacity')
sns.barplot(data = sales_state, x = 'Occupation',y= 'Amount')

## From above Graphs we can see that most of the buyers are working in IT, Healthcare and Aviation Sector

## Analysis by Product Category

## Count of Products sold Category wise 

plt.figure(figsize=(20,5))
plt.title('Count of Products sold Category wise')
ax = sns.countplot(data = sales_df, x = 'Product_Category')

for bars in ax.containers:
    ax.bar_label(bars)

## Product Category Sold as per Amount

sales_state = sales_df.groupby(['Product_Category'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)

plt.figure(figsize=(20,5))
plt.title('Product Category Sold as per Amount')
sns.barplot(data = sales_state, x = 'Product_Category',y= 'Amount')

## From above graphs we can see that most of the sold products are from Food, Clothing and Electronics category

## Conclusion- Married Women age group between 26-35 years from Uttar Pradesh, Maharastra and Karnataka working in IT, Healthcare and Aviation are more likely to buy products from Food, Clothing and Electronics Category









