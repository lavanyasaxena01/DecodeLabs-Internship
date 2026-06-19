# Data Science Project 1: Advanced EDA & Feature Engineering

## Overview

This project focuses on performing Advanced Exploratory Data Analysis (EDA) and Feature Engineering on an E-Commerce Orders Dataset. The objective is to transform raw transactional data into a clean, structured, and machine-learning-ready dataset by handling missing values, treating outliers, and creating meaningful predictive features.

## Project Objectives

* Perform comprehensive exploratory data analysis.
* Identify and handle missing values.
* Detect and treat outliers using the Interquartile Range (IQR) method.
* Engineer new features to improve predictive capability.
* Prepare a clean dataset suitable for machine learning applications.

## Dataset Information

The dataset contains 1,200 e-commerce order records with 14 features.

### Features

| Column Name     | Description                 |
| --------------- | --------------------------- |
| OrderID         | Unique Order Identifier     |
| Date            | Order Date                  |
| CustomerID      | Unique Customer Identifier  |
| Product         | Product Purchased           |
| Quantity        | Quantity Ordered            |
| UnitPrice       | Price per Unit              |
| ShippingAddress | Shipping Location           |
| PaymentMethod   | Mode of Payment             |
| OrderStatus     | Current Order Status        |
| TrackingNumber  | Shipment Tracking ID        |
| ItemsInCart     | Number of Items in Cart     |
| CouponCode      | Discount Coupon Applied     |
| ReferralSource  | Customer Acquisition Source |
| TotalPrice      | Total Order Value           |

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Google Colab

## Data Cleaning Process

### Missing Value Treatment

The dataset contained missing values in the `CouponCode` column.

* Missing Values: 309
* Missing Percentage: 25.75%

Since the column is categorical, missing values were replaced with the category:

```python
df['CouponCode'] = df['CouponCode'].fillna('NoCoupon')
```

This preserves business meaning and distinguishes customers who did not use any coupon.

## Outlier Detection and Treatment

Outliers were detected using the Interquartile Range (IQR) method on numerical features:

* Quantity
* UnitPrice
* ItemsInCart
* TotalPrice

### IQR Formula

Lower Bound = Q1 − 1.5 × IQR

Upper Bound = Q3 + 1.5 × IQR

### Treatment Method

Winsorization was applied using `numpy.clip()` to cap extreme values while preserving all records.

Benefits:

* Retains dataset size
* Prevents information loss
* Reduces the impact of extreme observations

## Feature Engineering

Three new predictive features were created:

### 1. OrderMonth

Extracted from the Date column.

```python
df['OrderMonth'] = df['Date'].dt.month
```

Purpose:

* Captures seasonal purchasing behavior.

### 2. CouponUsed

```python
df['CouponUsed'] = np.where(df['CouponCode']=='NoCoupon',0,1)
```

Purpose:

* Indicates whether a discount coupon was used.

### 3. CartUtilization

```python
df['CartUtilization'] = df['Quantity'] / df['ItemsInCart']
```

Purpose:

* Measures the proportion of cart items that were purchased.

## Exploratory Data Analysis

The following analyses were performed:

* Dataset Overview
* Missing Value Analysis
* Statistical Summary
* Product Distribution
* Payment Method Distribution
* Order Status Analysis
* Correlation Heatmap
* Outlier Visualization using Boxplots

## Key Findings

* Most features were complete and required minimal cleaning.
* CouponCode was the only feature with missing values.
* Numerical variables showed limited outlier presence.
* Customer behavior patterns can be better understood using engineered features such as CouponUsed and CartUtilization.
* Feature engineering significantly enhanced the analytical value of the dataset.

## Project Structure

```text
Project/
│
├── Dataset for Data Analytics.xlsx
├── Decodelab Project_1.ipynb
├── README.md
└── Output/
    ├── Boxplots.png
    ├── Heatmap.png
    └── EDA_Visualizations.png
```

## Conclusion

This project successfully transformed raw e-commerce transaction data into a machine-learning-ready dataset through data cleaning, missing value treatment, outlier handling, and feature engineering. The final dataset is structured, consistent, and suitable for predictive analytics and machine learning applications.
