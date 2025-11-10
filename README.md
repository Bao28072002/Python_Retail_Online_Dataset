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
[In 1]:  
```python
df = pd.read_excel(ecommerce_retail_xlsx)
df.head(10)
```
[Out 1]:  

<img width="875" height="503" alt="image" src="https://github.com/user-attachments/assets/9ae6f480-ab40-43c6-a3af-8a02b9e47eef" />

[In 2]:  
```python
# Check the general information of df
df.info()
```
[Out 2]:  

<img width="882" height="252" alt="image" src="https://github.com/user-attachments/assets/d475964e-d330-43c8-bf02-8cec874e6b17" />

[In 3]:
```python
# Check Data Summary
df.describe()
```
[Out 3]:

<img width="540" height="263" alt="image" src="https://github.com/user-attachments/assets/c7954fa0-e5f9-469f-9a73-394810a9f7a0" />

# 📊 Data Quality Summary & Validation Report

## Overview
During the initial data exploration phase, several data quality issues were identified. These must be addressed before conducting deeper analysis or building models:

- Negative values detected in `Quantity` and `UnitPrice`.
- Mismatch between the number of unique `StockCode` (4070) and `Description` (4223).
- Incorrect or inconsistent product descriptions in some orders.
- Transactions with negative quantities that are not marked as cancellations.

---

## ⚡ Key Issues Identified

### 1. Negative Values in `Quantity` and `UnitPrice`
Negative values in these columns are not logically valid and require review.

**Possible actions:**
- Check for data entry or ETL errors.
- Verify whether negative values indicate **refunds** or **cancellations**.
- Remove or correct invalid data to ensure analytical accuracy.

---

### 2. StockCode–Description Mismatch
A discrepancy was observed:
- **StockCode count:** 4070  
- **Description count:** 4223  

**Potential causes:**
- A single `StockCode` may appear with multiple descriptions.
- Some descriptions may not correspond to valid stock codes.
- Data inconsistencies due to missing, duplicated, or incorrectly recorded values.

**Recommendation:**  
Conduct additional validation and cleaning to ensure consistency.

---

## ⚠ Manual Review Required
Some orders contain **incorrect or suspicious product descriptions**.  
These should be reviewed manually and flagged for further processing.

---

## 🔎 Data Validation & Error Identification

- **Description Consistency Check:**  
  Merged `description_check_update` with the main `ecommerce` dataset to detect description mismatches.

- **Negative Quantities & Cancellations:**  
  Verified whether negative `Quantity` values correspond to cancellations based on the rule:  
  `InvoiceNo` starting with `"C"` = cancellation.

- **Next Step:**  
  Review all flagged errors and verify cancellation logic to ensure data integrity.

---

## 🚨 Identifying Invalid Transactions
After identifying cancellation invoices, further validation is required:

- Detect transactions where `Quantity` is negative **but** `InvoiceNo` does *not* start with `"C"`.  
  → These indicate potential data errors and should be corrected or excluded.

---

## ✨ Conclusion & Recommendations

### Columns requiring conversion to **string** for better processing:
- `InvoiceNo`
- `StockCode`
- `Description`
- `CustomerID`
- `Country`
## 🧹 Data Cleaning Rules for Invalid Transactions

### ✅ Canceled Orders
**Condition:**  
- `Quantity < 0` **and** `InvoiceNo` starts with `'C'`

**Action:**  
- These transactions represent **canceled orders** and should be **removed** from the dataset.

---

### ❌ Negative Quantity with Non-Cancellation Invoice
**Condition:**  
- `Quantity < 0` **but** `InvoiceNo` does **not** start with `'C'`

**Action:**  
- These rows contain **incorrect product descriptions** or invalid entries and should be **excluded** from the dataset.

---

### ❌ Negative Unit Price + Incorrect Description
**Condition:**  
- `UnitPrice < 0` **and** description flagged as incorrect

**Action:**  
- These are **invalid transactions** and should also be **removed** during data cleaning.

---
## 4. 🔍 Exploratory Data Analysis (EDA)

### 🛠 Step 1. Convert to correct Data type
[In 4]:
```python
df['InvoiceNo'].astype(str).str.startswith('C')

# Remove all canceled invoices from the dataset.
df = df[~df['InvoiceNo'].astype(str).str.startswith('C')]
df
```
### 🛠 Step 2. Removing Invalid Transactions

[In 5]:

```python
Unit_Quan_0 = df[(df['UnitPrice'] <= 0) | (df['Quantity'] <= 0)]
Unit_Quan_0 
```
## 5. 🧮 Apply RFM Model
#### 🛠 Step 1. Calculate RFM Score
[In 6]:

```python
#Choose Date to start 
df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'])
current_date = datetime(2011, 12, 31)

# Create TotalAmount column 
df['TotalAmount'] = df['Quantity'] * df['UnitPrice'] 

# Create RFM df
df = df.groupby(['CustomerID']).agg(
    {'InvoiceDate': lambda x: (current_date- x.max()).days,
     'InvoiceNo':'count',
     'TotalAmount':'sum'
     }
)

#### 🛠 Step 2. Assign RFM scores using Qcut
[In 7]:
```python
r_labels = range(5, 0, -1)
f_labels = range(1,6)
m_labels = range(1,6)

df['R_score'] = pd.qcut(df['Recency'],5, labels=r_labels)
df['F_score'] = pd.qcut(df['Frequency'],5, labels=f_labels)
df['M_score'] = pd.qcut(df['Monetary'],5, labels=m_labels)
df['RFM Score'] = (
    df['R_score'].astype(str)+
    df['F_score'].astype(str)+
    df['M_score'].astype(str)
    ).astype('int')
df = df.reset_index()
df.head()
```
[Out 7]:

<img width="574" height="180" alt="image" src="https://github.com/user-attachments/assets/c070973c-e532-43f2-9426-72746e8f8590" />

#### 🛠 Step 3. Merge the segmentation table with the RFM table based on the 'RFM Score'  
[In 8]:
```python
seg_rank= pd.read_excel('/content/drive/MyDrive/Portfolio/Python/data/Final Project/ecommerce retail.xlsx',sheet_name='Segmentation')
seg_rank
     
seg_rank['RFM Score'] = seg_rank['RFM Score'].str.split(',')
seg_rank = seg_rank.explode('RFM Score').reset_index(drop=True)
seg_rank['RFM Score'] = seg_rank['RFM Score'].str.strip().astype(int)
seg_rank

data_join = df.merge(seg_rank, how='left', on='RFM Score')
data_join   
```
[Out 8]:

<img width="750" height="401" alt="image" src="https://github.com/user-attachments/assets/fd312e74-8535-4c45-842f-03d7375380ae" />

#### 🛠 Step 4. Data Cleaning & Check Outliers
[In 9]:
```python
#Outlier Monetary
fig=plt.figure(1,figsize=(9,6))
plt.boxplot(data_join['Monetary'])
```
[Out 9]:

<img width="781" height="491" alt="image" src="https://github.com/user-attachments/assets/315fcaea-352f-45d4-b7f8-2257484a8ce8" />

[In 10]:
```python
#Outlier Recency
fig=plt.figure(1,figsize=(9,6))
plt.boxplot(data_join['Recency'])
```
[Out 10]:

<img width="769" height="498" alt="image" src="https://github.com/user-attachments/assets/b9afa80f-8a29-4303-84c6-4d6cc45511c4" />

[In 11]:
```python
#Outlier Frequency
fig=plt.figure(1,figsize=(9,6))
plt.boxplot(data_join['Frequency'])
```
[Out 11]:

<img width="783" height="497" alt="image" src="https://github.com/user-attachments/assets/de585904-607e-4e2a-95c0-83a952ab5325" />

#### 🛠 Step 5. Using IQR to handle outliers
[In 12]:
```python
#Monetary
Q1 = data_join['Monetary'].quantile(0.25)
Q3 = data_join['Monetary'].quantile(0.75)
IQR = Q3 - Q1
data_join = data_join[(data_join['Monetary'] >= Q1 - 1.5*IQR) & (data_join['Monetary'] <= Q3 + 1.5*IQR)]

#Recency
Q1 = data_join['Recency'].quantile(0.25)
Q3 = data_join['Recency'].quantile(0.75)
IQR = Q3 - Q1
data_join = data_join[(data_join['Recency'] >= Q1 - 1.5*IQR) & (data_join['Recency'] <= Q3 + 1.5*IQR)]

#Frequency
Q1 = data_join['Frequency'].quantile(0.25)
Q3 = data_join['Frequency'].quantile(0.75)
IQR = Q3 - Q1
data_join = data_join[(data_join['Frequency'] >= Q1 - 1.5*IQR) & (data_join['Frequency'] <= Q3 + 1.5*IQR)]

#Plot box
fig=plt.figure(1,figsize=(9,6))
plt.boxplot(data_join['Monetary'])
fig=plt.figure(2,figsize=(9,6))
plt.boxplot(data_join['Frequency'])
fig=plt.figure(3,figsize=(9,6))
plt.boxplot(data_join['Recency'])
```
[Out 12]:

**Monetary**  
![Monetary](https://github.com/user-attachments/assets/e966cef8-5fea-45c8-b6d0-6442fd049664)

**Frequency**  
![Frequency](https://github.com/user-attachments/assets/aacac9f9-d63f-4ed6-a0be-6e7f76ec0bc2)

**Recency**  
![Recency](https://github.com/user-attachments/assets/22d2cdab-da7f-427c-974e-f9497dbb5731)

## 5. 🔍 Which metrics is important R, F or M?
#### 🛠 Using correlation to find important metrics
[In 13]:
```python
plt.figure(figsize=(8,4))
corr = data_join[['R_score', 'F_score', 'M_score']].corr()
sns.heatmap(corr, annot=True, cmap=sns.light_palette("#50c878", as_cmap=True),linewidths=0.5, linecolor='white')
plt.title('Correlation R, F, M', fontsize=12)
plt.tight_layout()
plt.show()
```
[Out 13]:

![Correlation](https://github.com/user-attachments/assets/058cf31e-5d5e-476b-9cf4-d72ae60ec559)

**Recommendation:** The Marketing department should focus on **Frequency (F)** and **Monetary (M)** metrics.

#### Each chart shows the frequency distribution of the RFM data.
[In 14]:
```python
features = ['Recency', 'Frequency', 'Monetary']
bins_dict = {'Recency': 40, 'Frequency': 40, 'Monetary': 40}
xlims = {
    'Recency': (0, 400),
    'Frequency': (0, 200),
    'Monetary': (0, 4000)
}
for col in features:
    plt.figure(figsize=(8, 4))
    data_join[col].hist(bins=bins_dict[col], color='#50c878', edgecolor='black')
    plt.title(f'{col} Distribution')
    plt.xlabel(col)
    plt.ylabel('Count')
    plt.xlim(xlims[col])
    plt.tight_layout()
    plt.show()
```

[Out 14]:

![RecencyDistribution](https://github.com/user-attachments/assets/c146eba0-5653-4fd8-ab03-a58510a5d83e)

![FrequencyDistribution](https://github.com/user-attachments/assets/ae2a43e6-e053-4f03-b9e1-b1c7f7a4d3c0)

![MonetaryDistribution](https://github.com/user-attachments/assets/201b8758-b9f8-4b0d-b7a8-69275bf69100)

## 6. 🔍 Overview Segmentation

[In 15]:
```python
grp_total = (data_join.groupby('Segment').agg({'CustomerID': 'count','Monetary': 'sum'}).reset_index())
grp_total['Customer Percent(%)'] = (grp_total['CustomerID'] / grp_total['CustomerID'].sum() * 100).round(2)
grp_total['Sales Percent(%)'] = (grp_total['Monetary'] / grp_total['Monetary'].sum() * 100).round(2)
grp_total = grp_total.rename(columns={'CustomerID': 'Count ID'})
grp_total
```

[Out 15]:

![Segmentation](https://github.com/user-attachments/assets/78308e02-298f-46dd-ae90-3093b6bebefe)

[In 16]:
```python
colors = sns.color_palette("YlGnBu", len(grp_total))
fig,ax = plt.subplots(1, figsize=(20,5))
sq.plot(sizes=grp_total["Count ID"],
              label=grp_total["Segment"],
              value=[f'{x}%' for x in grp_total["Customer Percent(%)"]],
              alpha=.8,
              color=colors,
              bar_kwargs=dict(linewidth=1.5, edgecolor="white")
              )
plt.title("Customer Size by Segment", fontsize=13)
plt.axis("off")
plt.show()
```

[Out 16]:

<img width="900" height="269" alt="image" src="https://github.com/user-attachments/assets/8ed6b785-85b8-494c-8143-fbf35da45fe7" />

## 📊 RFM Segment Summary & Strategic Actions

### ✅ **High-Value Segments (31.58%)**
Includes:
- **Champions (8.39%)** – Best customers with high purchase frequency and high order value  
- **Loyal Customers (9.34%)**  
- **Potential Loyalists (13.85%)**

**These three segments contribute the largest share of revenue.**

**Recommended Strategies:**
- Build a **VIP customer program** with exclusive perks, loyalty points, and premium benefits.  
- Personalize product recommendations.  
- Focus on **high-end products** or **high-value bundles** to increase average order value.

---

### ⚠️ **Inactive or At-Risk Segments (37.57%)**
Includes:
- **Hibernating Customers (22.07%)**  
- **Lost Customers (10.27%)**  
- **About to Sleep (5.23%)**

**These segments account for over one-third of customers who are no longer actively purchasing.**

**Recommended Strategies:**
- Send **special offers** (discounts, birthday gifts, cashback vouchers).  
- Implement **personalized re-engagement programs**, such as:
  - Post-purchase follow-up  
  - Technical support  
  - Priority customer service  

---

### 🌱 **New & Developing Customers (12.17%)**
Includes:
- **New Customers (8.62%)**  
- **Promising (3.55%)**

**These groups are in early stages with potential for growth.**

**Recommended Strategies:**
- Create a strong first impression with a **welcome email**, product guides, or next-order discounts.  
- Encourage early repeat purchases to move them into the **Potential Loyalist** segment through:
  - Reward points  
  - Subscription bundles  
  - Regular promotional packages  

[In 17]:
```python
fig,ax = plt.subplots(1, figsize=(20,5))
sq.plot(sizes=grp_total["Count ID"],
              label=grp_total["Segment"],
              value=[f'{x}%' for x in grp_total["Sales Percent(%)"]],
              alpha=.8,
              color=colors,
              bar_kwargs=dict(linewidth=1.5, edgecolor="white")
              )
plt.title("Sale by Segment", fontsize=13)
plt.axis("off")
plt.show()
```
[Out 17]:

<img width="887" height="253" alt="image" src="https://github.com/user-attachments/assets/73b6f20b-615f-455b-ae8e-6388d5bc474a" />

## 🔥 1. High-Revenue Segments

### **Champions – ~21.75%**
- Most valuable customers  
- Purchase frequently with high order value  
- The “backbone” of your revenue  

### **Loyal – ~19.35%**
- Consistently repeat purchases  
- Strong potential for upsell with the right incentives  

### **Potential Loyalist – ~9.85%**
- Emerging segment  
- Can easily be converted into Loyal or Champions  

👉 **These three segments contribute nearly 50% of total revenue → must prioritize retention & upsell.**

---

## ⚠️ 2. At-Risk but Valuable Segments

### **At Risk – ~15.52%**
- Significant revenue contribution  
- Showing declining engagement  
- Requires rescue campaigns  

### **Need Attention – ~8.66%**
- Previously active but now less engaged  
- A single promo or reminder can re-activate them  

### **Hibernating Customers – ~10.52%**
- Old customers who haven’t purchased for a long time  
- Send vouchers or run reactivation campaigns  

👉 **Nearly 35% of revenue is “sleeping” → reactivation can boost revenue quickly.**

---

## ❌ 3. Low-Revenue Segments

### **Lost Customers – ~2.24%**
- Almost churned completely  
- Minimal revenue → gentle remarketing only  

### **Cannot Lose Them – ~3.69%**
- At the edge of leaving but still valuable  
- Requires urgent retention efforts  

### **About to Sleep – ~1.80%**
- Low purchase activity and about to churn  

---

## 🌱 4. New & Potential Segments

### **New Customers – ~2.21%**
- First-time buyers  
- Revenue not yet high  

### **Promising – ~3.92%**
- Bought a few times  
- Strong potential for future growth  

👉 **Deliver a great onboarding experience to move them into the Potential Loyalist group.**

| Segment Group | Meaning | Priority Level |
|---------------|---------|----------------|
| **Champions, Loyal, Potential Loyalist** | Contribute the largest share of revenue | ⭐ Very High |
| **At Risk, Need Attention, Hibernating** | Significant revenue but currently at risk | ✅ High |
| **New, Promising** | Early-stage customers with potential to grow | ⚡ Medium |
| **Lost, About To Sleep, Cannot Lose Them** | Low contribution, high churn risk | ➖ Low |

[In 18]:
```python
plt.figure(figsize=(16,8))
sns.scatterplot(
    x='Frequency',
    y='Monetary',
    hue='Segment',
    size='Recency',
    sizes=(20, 200),
    alpha=0.6,
    data=data_join
)
plt.title("Monetary vs Frequency")
plt.xlim(0, 220)
plt.ylim(0, 4000)
plt.show()
```
[Out 18]:

<img width="927" height="479" alt="image" src="https://github.com/user-attachments/assets/924e37b6-0bde-4b47-9371-121e88848fa2" />

## 📊 Meaning of the "Monetary vs Frequency" Scatter Plot

### ✅ 1. Main Relationship
- There is a clear upward trend:  
  **Higher purchase frequency → Higher total spending (Monetary).**
- Loyal and high-value customers cluster on the **top-right** area of the chart.

---

## 🥇 2. Champions & Loyal Stand Out
- These segments appear mostly in the **upper-right quadrant** (high Frequency + high Monetary).
- They represent customers who purchase often and spend a lot.
- This is the ideal customer group.

---

## ⚠️ 3. At Risk & Hibernating: High Spending but Becoming Inactive
- Many orange and light-blue points are seen with:
  - **High Monetary**
  - **Low or moderate Frequency**
  - **Large bubble sizes** (high Recency → haven’t purchased for a long time)
- These customers used to spend a lot but are **falling inactive**.
- Critical group for reactivation campaigns.

---

## ❌ 4. Low-Revenue Segments (Lost, About To Sleep)
- Found mostly on the **bottom-left** (low Frequency + low Monetary).
- Small bubble sizes (low Recency).
- Represents customers who have low engagement or are about to churn.

---

## 🌱 5. New & Promising Customers
- Appearing in the **lower-mid area**:
  - Low Frequency (new buyers)
  - Moderate Monetary
- These groups show **future revenue potential**.

---

## ✅ Summary
- **Frequency and Monetary are positively correlated.**
- **Champions & Loyal** drive the highest revenue (top-right cluster).
- **At Risk & Hibernating** need targeted reactivation.
- **Lost & About To Sleep** contribute little revenue.
- **New & Promising** should be nurtured to move into high-value segments.

[In 19]:
```python
plt.figure(figsize=(16,8))
sns.scatterplot(
    x='Recency',
    y='Monetary',
    hue='Segment',
    size='Recency',
    sizes=(20, 200),
    alpha=0.6,
    data=data_join
)
plt.title("Monetary vs Recency ")
plt.xlim(0, 450)
plt.ylim(0, 4000)
plt.show()
```
[Out 19]:

<img width="899" height="474" alt="image" src="https://github.com/user-attachments/assets/f9efa992-57a3-4c78-a713-e033c75b9e30" />

# 📊 Meaning & Insights from the “Monetary vs Recency” Chart

## ✅ Overall Meaning
- **Recency (X-axis)**: number of days since last purchase  
  → Higher Recency = customer has not purchased for a long time  
- **Monetary (Y-axis)**: total spending  
- **Bubble size**: Frequency (number of purchases)  
- **Colors**: Different RFM segments  

The chart shows **no clear upward trend**, meaning:
**High-spending customers can still stop buying for a long period.**

---

# ✅ Insights by Segment

## 🟩 Champions
- Mostly at **low Recency (< 50 days)**  
- High Monetary and high Frequency  
✅ Must keep engaging this group with VIP programs.

---

## 🟦 Loyal
- Recency mostly under 100 days  
- Good spending and steady purchases  
✅ Easy to convert into Champions through upsell and loyalty points.

---

## 🟧 At Risk
- Recency spreads widely from 50–300+ days  
- Many have **high Monetary but long Recency**  
⚠️ These were valuable customers but are becoming inactive.

✅ Reactivation needed: personalized emails, vouchers, support calls.

---

## 🟪 Hibernating Customers
- High Recency (150–350+ days)  
- Medium to high Monetary  
⚠️ They “disappeared” for a long time.

✅ Use strong reactivation campaigns (discounts, “We miss you” messages).

---

## 🔴 Lost Customers
- Very high Recency (250–360+) and low Monetary  
❌ Low ROI if focusing on them.

✅ Use only light remarketing (monthly newsletters or soft reminders).

---

## 🟡 Cannot Lose Them
- High Recency but still had good Monetary  
⚠️ High-value customers on the edge of leaving.

✅ Consider urgent retention actions: direct calls, premium voucher.

---

## 🌱 New Customers & Promising
- Low Recency (recent buyers)  
- Low–medium Monetary  
✅ Important stage to build trust.

✅ Encourage second purchase using onboarding flows and next-order discounts.

---

# ✅ Key Strategic Insights

### ✅ 1. High Monetary + High Recency = **At Risk** → must prioritize
These customers brought high revenue but are now “silent”.

### ✅ 2. Champions & Loyal = stable revenue foundation
Maintain engagement through VIP benefits and personalized offers.

### ✅ 3. New & Promising = nurture early to grow future revenue
Guide them toward becoming Potential Loyalists.

### ✅ 4. Lost Customers = low priority
Do not invest heavily in this segment.

