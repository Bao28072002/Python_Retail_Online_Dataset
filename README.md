# 🛒 Customer Segmentation For Marketing Campaigns in A Retail Global SuperStore | Python

![image](https://github.com/user-attachments/assets/b90b73a6-aaa6-44ad-9749-a798ebaf4632)

**Author:** Lê Gia Bảo

**Date:** October 2025

**Tools Used:** Python

## 📑 Table of Contents 

[📌 1. Background & Overview](#background--overview)  
[📂 2. Dataset Description & Data Structure](#dataset-description--data-structure)  
[🧹 3. Data Cleaning & Preprocessing](#data-cleaning--preprocessing)  
[🔍 4. Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)  
[🧮 5. Apply RFM Model](#apply-rfm-model)  
[📊 6. Visualization & Analysis](#visualization--analysis)  
[💡 7. Insight & Recommendation](#insight--recommendation)
## 1. 📌 Background & Overview

### Objective ###

📖 **What is this project about?**  

1. The Marketing team plans to launch personalized customer retention and acquisition campaigns for the holiday season. However, due to the large size of the dataset, manual segmentation is no longer feasible.

2. To address this challenge, the **RFM model** is applied using **Python (Colab)** to segment customers based on their purchasing behavior.

3. This project includes:
- Data preparation  
- RFM scoring  
- Customer segmentation  
- Visualization  
- Actionable recommendations to help the Marketing and Sales teams optimize their strategies

👤 **Who is this project for?**  

✔️ Marketing & Sales Department  
✔️ Decision-makers & stakeholders  

## ❓ Business Questions

✔️ How can customers be segmented effectively using the RFM model?  
✔️ Which customer groups should be prioritized for retention and promotional campaigns?  
✔️ What insights can help improve marketing strategies and customer engagement?  
✔️ What strategies should be applied to each customer segment to maximize value?

### RFM Analysis Overview  

**🔎 Why use RFM?**  
RFM (Recency, Frequency, Monetary) is a customer analysis method that evaluates purchasing behavior. In this approach, each customer receives a score based on the three RFM components. These scores are then used to group customers into segments, helping businesses identify target audiences for focused marketing and sales strategies.

- **Recency**: Indicates how much time has passed since the customer’s most recent purchase.  
- **Frequency**: Reflects how often the customer makes purchases.  
- **Monetary**: Measures the total amount the customer has spent.

Using RFM allows businesses to segment customers based on their value and apply these insights to improve marketing activities and enhance customer engagement.

## 2. 📂 Dataset Description & Data Structure

### 📌 Data Source  
- **Source**: Provided dataset for E-commerce retail analysis  
- **Size**: 541,910 rows × 8 columns (Sheet 1: E-commerce retail), additional segmentation details in Sheet 2  
- **Format**: .xlsx (Excel file with two sheets)  
## 📂 Data Structure & Relationships  

### 1️⃣ Tables Used  
The dataset consists of **two tables (sheets)**:  
- **Sheet 1: E-commerce Retail** – Contains transaction-level data, including order details, customer IDs, and purchase information.  
- **Sheet 2: Segmentation** – Stores customer segments along with their RFM scores.  

### 2️⃣ Table Schema & Data Snapshot  

#### 📌 Sheet 1: E-commerce Retail  
### 📋 Table Schema: E-commerce Retail  

<details>
  <summary>📂 **Dataset Schema** (Click to expand)</summary>

| Column Name  | Data Type         | Description  |  
|-------------|-----------------|--------------|  
| **InvoiceNo**  | `object`  | Unique invoice number for each transaction (6-digit). If it starts with 'C', it indicates a cancellation. |  
| **StockCode**  | `object`  | Unique product (item) code (5-digit). |  
| **Description**  | `object`  | Product (item) name. |  
| **Quantity**  | `int64`  | The number of units purchased per transaction. |  
| **InvoiceDate**  | `datetime64[ns]`  | Date and time when the transaction occurred. |  
| **UnitPrice**  | `float64`  | Price per unit of the product in sterling. |  
| **CustomerID**  | `float64`  | Unique 5-digit identifier for each customer. |  
| **Country**  | `object`  | Name of the country where the customer resides. |  

</details>

#### 📌 Sheet 2: Segmentation  
### 📊 Customer Segmentation & RFM Scores  

<details>
  <summary>📊 **RFM Segmentation Mapping** (Click to expand)</summary>

| **Segment**              | **RFM Score**  |  
|-------------------------|-----------------------------------------------------------|  
| **Champions**            | 555, 554, 544, 545, 454, 455, 445  |  
| **Loyal**                | 543, 444, 435, 355, 354, 345, 344, 335  |  
| **Potential Loyalist**   | 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323  |  
| **New Customers**        | 512, 511, 422, 421, 412, 411, 311  |  
| **Promising**            | 525, 524, 523, 522, 521, 515, 514, 513, 425, 424, 413, 414, 415, 315, 314, 313  |  
| **Need Attention**       | 535, 534, 443, 434, 343, 334, 325, 324  |  
| **About To Sleep**       | 331, 321, 312, 221, 213, 231, 241, 251  |  
| **At Risk**              | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124  |  
| **Cannot Lose Them**     | 155, 154, 144, 214, 215, 115, 114, 113  |  
| **Hibernating Customers** | 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211  |  
| **Lost Customers**       | 111, 112, 121, 131, 141, 151   |

</details>

## 3. 🧹 Data Cleaning & Preprocessing
 
