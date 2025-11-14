# 🛒 Customer Segmentation For Marketing Campaigns in A Retail Global SuperStore | Python

<img width="1024" height="448" alt="image" src="https://github.com/user-attachments/assets/88b86c69-3ab2-43e5-9868-af52e711f0f3" />

**Author:** Lê Gia Bảo

**Date:** October 2025

**Tools Used:** Python

## 📑 Table of Contents 
[📌 1. Background & Overview](#background-overview)<br>
[📂 2. Dataset Description & Data Structure](#dataset-description--data-structure)<br>
[🧹 3. Data Cleaning & Preprocessing](#data-cleaning--preprocessing)<br>
[🔍 4. Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)<br>
[🧮 5. Apply RFM Model](#apply-rfm-model)

## Background & Overview

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

## ❓ Business Questions

✔️ How can customers be segmented effectively using the RFM model?  
✔️ Which customer groups should be prioritized for retention and promotional campaigns?  
✔️ What insights can help improve marketing strategies and customer engagement?  
✔️ What strategies should be applied to each customer segment to maximize value?

👤 **Who is this project for?**  

✔️ Marketing & Sales Department  
✔️ Decision-makers & stakeholders  

### RFM Analysis Overview  

**🔎 Why use RFM?**  
RFM (Recency, Frequency, Monetary) is a customer analysis method that evaluates purchasing behavior. In this approach, each customer receives a score based on the three RFM components. These scores are then used to group customers into segments, helping businesses identify target audiences for focused marketing and sales strategies.

- **Recency**: Indicates how much time has passed since the customer’s most recent purchase.  
- **Frequency**: Reflects how often the customer makes purchases.  
- **Monetary**: Measures the total amount the customer has spent.

Using RFM allows businesses to segment customers based on their value and apply these insights to improve marketing activities and enhance customer engagement.

## Dataset Description & Data Structure

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

## Data Cleaning & Preprocessing

# 📊 Data Quality Summary & Validation Report

## Overview
During the initial data exploration phase, several data quality issues were identified. These must be addressed before conducting deeper analysis or building models:

- Negative values detected in `Quantity` and `UnitPrice`.
- Mismatch between the number of unique `StockCode` (4070) and `Description` (4223).
- Incorrect or inconsistent product descriptions in some orders.
- Transactions with negative quantities that are not marked as cancellations.

---

## ⚡ Key Issues Identified

<details>
  <summary>🧹 <b>Data Quality Overview (Click to expand)</b></summary>

---

### 1. Negative Values in `Quantity` and `UnitPrice`
- Negative values are not logically valid.  
- **Possible causes:**  
  - Data entry or ETL errors  
  - Refunds or cancellations  
- **Action:**  
  - Review, correct, or remove invalid rows

---

### 2. StockCode–Description Mismatch
- **Unique StockCode:** 4070  
- **Unique Description:** 4223  
- **Potential causes:**  
  - One `StockCode` mapped to multiple descriptions  
  - Descriptions not matching valid codes  
  - Missing / duplicated / incorrect values  
- **Recommendation:**  
  - Validate and standardize product descriptions

---

### 3. Manual Review Required
- Some orders contain incorrect or suspicious product descriptions  
- **Action:**  
  - Manually review and flag these entries

---

### 4. Data Validation: Negative Quantity Logic
- Verified cancellation rule:  
  → **InvoiceNo starting with `'C'` = Canceled order**

---

### 5. Identifying Invalid Transactions
- **Invalid Case A:**  
  - `Quantity < 0` **and** InvoiceNo **does not** start with `'C'`  
  → Data error → Remove  
- **Invalid Case B:**  
  - `UnitPrice < 0` **and** Description flagged incorrect  
  → Invalid transaction → Remove  

---

### 6. Columns Recommended to Convert to String
- `InvoiceNo`  
- `StockCode`  
- `Description`  
- `CustomerID`  
- `Country`

---

### 7. Cleaning Rule: Canceled Orders
- **Condition:**  
  - `Quantity < 0` **and** InvoiceNo starts with `'C'`  
- **Action:**  
  - Remove canceled invoices from dataset

---

</details>

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

## Exploratory Data Analysis (EDA)

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

## Apply RFM Model

#### 🛠 Step 1. Calculate RFM Score

**Recency (R)**  
- Labels: 5, 4, 3, 2, 1  
- Logic: smaller Recency = customer purchased more recently → higher score  
- Recency small → score 5 (good)  
- Recency large → score 1 (less desirable)  

**Frequency (F)**  
- Labels: 1, 2, 3, 4, 5  
- Logic: higher frequency = better → higher score  

**Monetary (M)**  
- Labels: 1, 2, 3, 4, 5  
- Logic: higher spending = better → higher score

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

#Outlier Recency
fig=plt.figure(1,figsize=(9,6))
plt.boxplot(data_join['Recency'])

#Outlier Frequency
fig=plt.figure(1,figsize=(9,6))
plt.boxplot(data_join['Frequency'])
```
[Out 9]:

### 🔹 Outliers

- **Left (Monetary):**
- **Middle (Recency):**
- **Right (Frequency):**

<p float="left">
  <img width="300" alt="image1" src="https://github.com/user-attachments/assets/315fcaea-352f-45d4-b7f8-2257484a8ce8" style="margin-right:5px"/>
  <img width="300" alt="image2" src="https://github.com/user-attachments/assets/b9afa80f-8a29-4303-84c6-4d6cc45511c4" style="margin-right:5px"/>
  <img width="300" alt="image3" src="https://github.com/user-attachments/assets/de585904-607e-4e2a-95c0-83a952ab5325"/>
</p>


#### 🛠 Step 5. Using IQR to handle outliers

- IQR is the **range of the middle 50% of the data**, representing the "typical" values in the dataset.
- IQR is used to **detect and remove outliers**, which are unusually high or low values that can skew analysis.  
- By focusing on the middle 50% of data, it helps make **analysis and predictions more accurate** and **insights more reliable**.

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
### 🔹After Outliers

- **Left (Monetary):**
- **Middle (Recency):**
- **Right (Frequency):**

<p float="left">
  <img width="300" alt="image4" src="https://github.com/user-attachments/assets/e966cef8-5fea-45c8-b6d0-6442fd049664" style="margin-right:5px"/>
  <img width="300" alt="image5" src="https://github.com/user-attachments/assets/aacac9f9-d63f-4ed6-a0be-6e7f76ec0bc2" style="margin-right:5px"/>
  <img width="300" alt="image6" src="https://github.com/user-attachments/assets/22d2cdab-da7f-427c-974e-f9497dbb5731"/>
</p>


## 5. 🔍 Which metrics is important R, F or M?
#### 🛠 Using correlation to find important metrics

The primary goal of using the **Pearson Correlation Coefficient** is to **determine how variables change together** (whether they increase together, or one increases while the other decreases).

| $r$ Value | Correlation Strength | Interpretation |
| :---: | :---: | :--- |
| Close to **+1** | **Strong Positive Correlation** | The two variables change **in the same direction** (as one increases, the other also tends to increase). |
| Close to **-1** | **Strong Negative Correlation** | The two variables change **in opposite directions** (as one increases, the other tends to decrease). |
| Close to **0** | **Weak Correlation** | There is **little or no clear linear relationship** between the two variables. |

---

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

| Core Segment | Weight | Constituent Customer Groups | Segment Summary | Key Action Strategy |
| :--- | :---: | :--- | :--- | :--- |
| **✅ High-Value** | **31.58%** | **Champions (8.39%)**<br>**Loyal Customers (9.34%)**<br>**Potential Loyalists (13.85%)** | The **best customers**, contributing the largest revenue share and showing high growth potential. | Build a **VIP program** with exclusive perks. Increase **AOV** by focusing on premium products or high-value bundles. |
| **⚠️ At-Risk/Inactive** | **37.57%** | **Hibernating Customers (22.07%)**<br>**Lost Customers (10.27%)**<br>**About to Sleep (5.23%)** | The **largest group**, currently dormant or at high risk of churning. Requires urgent re-engagement. | Send **special offers** (discounts, attractive vouchers). Implement **personalized re-engagement programs** (support, priority service). |
| **🌱 New & Developing** | **12.17%** | **New Customers (8.62%)**<br>**Promising (3.55%)** | New customers with great potential. Focus on solidifying the relationship and driving early repeat purchases. | Create a strong **first impression** (**welcome email**, guides). Encourage early repeat purchases with **reward points**, **subscription bundles**, or next-order incentives. |

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

| Segment Type                  | Segment Name        | % of Customers | Key Info / Action                           |
|--------------------------------|------------------|----------------|--------------------------------------------|
| 🔥 High-Revenue                | Champions         | 21.75%         | Frequent, high-value buyers → retention & upsell |
|                                | Loyal             | 19.35%         | Repeat buyers → upsell potential           |
|                                | Potential Loyalist| 9.85%          | Emerging → can become Loyal/Champion       |
| ⚠️ At-Risk but Valuable        | At Risk           | 15.52%         | Declining engagement → rescue campaigns    |
|                                | Need Attention    | 8.66%          | Previously active → promo/reactivate       |
|                                | Hibernating       | 10.52%         | Long inactive → vouchers/reactivation      |
| ❌ Low-Revenue                 | Lost              | 2.24%          | Almost churned → gentle remarketing        |
|                                | Cannot Lose       | 3.69%          | Edge of leaving → urgent retention         |
|                                | About to Sleep    | 1.80%          | Low activity → risk of churn               |
| 🌱 New & Potential             | New               | 2.21%          | First-time buyers → revenue not yet high   |
|                                | Promising         | 3.92%          | Bought a few times → growth potential     |


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


## ✅ Summary

| Customer Group | Where They Are on the Chart | What It Means (Insight) | What to Do (Action) |
| :--- | :--- | :--- | :--- |
| **🥇 Champions & Loyal** | **Top-Right** (Buy often + Spend a lot) | They are your **best customers**. They bring in steady cash. | **Keep Them Happy:** Give them **VIP treatment** and offer them **premium products** to buy more. |
| **⚠️ At Risk & Hibernating** | **Scattered High Value** (Spent a lot, but maybe **big dots** showing they haven't bought recently). | They were good spenders but are **starting to leave**. This is a critical group to save. | **Bring Them Back:** Send them **special deals** and **personalized messages** right away to encourage them to buy again. |
| **🌱 New & Promising** | **Lower-Middle** (New buyers, still small purchases) | They are new but have **potential to grow**. | **Help Them Grow:** Use **welcome emails** and offer **discounts on their next order** to encourage them to buy frequently. |
| **❌ Lost & Low-Revenue** | **Bottom-Left** (Buy rarely + Spend little) | They are not engaged and don't bring much money. | **Low Effort:** Only use **simple reminders** (like an email newsletter) and don't spend much money trying to win them back. |

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

## 📋 Consolidated Customer Strategy Groups Summary

| Strategy Group | Constituent Segments | Strategic Objective | Key Actions | Priority Level |
| :--- | :--- | :--- | :--- | :---: |
| **I. Retention & Growth** | Champions, Loyal, New Customers, Promising | To **maintain** stable revenue, **increase** LTV, and **nurture** new buyers. | **VIP programs/Exclusive offers**. **Upsell/Premium** bundles. **Onboarding** flows to encourage early repeat purchases. | **HIGHEST** |
| **II. Urgent Reactivation** | At Risk, Cannot Lose Them | To **prevent revenue loss** from high-value customers who are currently churning (High Monetary, High Recency). | **Highly personalized outreach** (direct calls, dedicated emails). Offer **premium vouchers/incentives** for retention. | **HIGH** |
| **III. Recovery & Nurturing** | Hibernating Customers, Lost Customers | To **recover** dormant customers and **optimize** marketing spend on low-return segments. | Use **"We miss you" campaigns** (deep discounts) for Hibernating. Use **light remarketing** for Lost Customers. | **MEDIUM** |

### 🎯 Purpose Average Recency by Segment

1.  **Risk Assessment:** To visually quantify the level of **churn risk** across all customer segments by comparing their average Recency values (bar heights).
2.  **Action Prioritization:** To quickly identify segments with **High Recency** (tall bars) that require **urgent reactivation efforts** to prevent revenue loss.

[In 20]:
```python
recency_mean = data_join.groupby('Segment', as_index=False)['Recency'].mean()
plt.figure(figsize=(16, 8))
ax = sns.barplot(x='Segment', y='Recency', data=recency_mean, palette='viridis')
plt.title('Average Recency by Segment')
plt.xlabel('Segment')
plt.ylabel('Average Recency')
plt.xticks(rotation=45, ha='right')
for i, v in enumerate(recency_mean['Recency']):
    ax.text(i, v + 1, f"{v:.1f}", ha='center', va='bottom', fontsize=11, fontweight='bold', color='black')
plt.tight_layout()
plt.show()
```
[Out 20]:

<img width="933" height="460" alt="image" src="https://github.com/user-attachments/assets/a7361ffb-14e5-4607-ad3b-3f921e60d0df" />

## 📋 Average Recency by Segment Analysis & Strategy Summary

| Risk Group | Segment | Avg. Recency (Days) | Core Issue | Recommended Action |
| :--- | :--- | :---: | :--- | :--- |
| **🚨 High Risk** | At Risk | 283.3 | **Very long inactivity**, urgent need for intervention. | Immediate **"Win-back" campaign** (e.g., 30% discount + Free Ship). |
| | Cannot Lose / Championship | 237.9 / 215.1 | **High-value customers** showing signs of disengagement. | **Personalized outreach** (Account Manager), exclusive/VIP rewards. |
| **🌟 Growth Potential** | New Customers | 32.4 | **Recent buyers**, crucial to retain from the start. | 30-day **Onboarding sequence**, special offer for the second purchase. |
| | Loyal Customers | 49.6 | **Steady and loyal**, easy to convert to Champions. | **VIP/Points program**, special gifts, Upsell opportunities. |
| **💎 Retention Focus** | Low Customers / Low 1 | 107.9 / 165.7 | **Moderate Recency**, need increased engagement efforts. | **Bi-weekly reactivation campaigns**, **Cross-selling** based on purchase history. |
## 📈 Measurement & Optimization

### Tracking KPIs:
- **Recency reduction** for "At Risk" group (target: -20% in 3 months)
- **Retention rate** for "New Customers" (target: >60% after 90 days)
- **Purchase frequency** for "Loyal Customers"

### A/B Testing Required:
- Different discount levels (20% vs 30% vs 40%)
- Communication channels (email vs SMS vs push notification)
- Message framing ("We miss you" vs "Special offer just for you")

## 🔄 Continuous Improvement

1. **Segment refinement**: Additional RFM analysis combined with CLV
2. **Personalization**: Based on browsing behavior and purchase history
3. **Automation**: Trigger-based campaigns when recency exceeds thresholds

## 🎯 Priority Ranking

| Priority | Customer Group | Action |
|----------|----------------|---------|
| 1 | At Risk & Cannot Lose | Critical - Immediate intervention |
| 2 | New Customers | Preventive - Retention focus |
| 3 | Championship & Loyal Customers | Maintenance - Optimization |
| 4 | Low Customers | Improvement - Reactivation |

### 🎯  Purpose Average Frequency by Segment

1.  **Assess Loyalty:** To **rank** the purchase frequency level of different segments.
2.  **Prioritize Strategy:** To identify segments with **HIGH** Frequency to focus resources on **retention and upselling**.

[In 21]:
```python

frequency_mean = data_join.groupby('Segment', as_index=False)['Frequency'].mean()
plt.figure(figsize=(16, 8))
ax = sns.barplot(x='Segment', y='Frequency', data=frequency_mean, palette='viridis')
plt.title('Average Frequency by Segment')
plt.xlabel('Segment')
plt.ylabel('Average Frequency')
plt.xticks(rotation=45, ha='right')
for i, v in enumerate(frequency_mean['Frequency']):
    ax.text(i, v + 1, f"{v:.1f}", ha='center', va='bottom', fontsize=11, fontweight='bold', color='black')
plt.tight_layout()
plt.show()
```
[Out 21]:

<img width="924" height="432" alt="image" src="https://github.com/user-attachments/assets/c7da55da-c0eb-4ae6-a2a9-44623b8ff2ed" />

# 📊 Average Frequency by Segment Analysis - Insights & Recommendations

## 🔍 Understanding Frequency Metrics

### **What Frequency Measures**
- **Frequency** = Average number of purchases made by customers in a specific time period
- **High Frequency** = Customers purchase regularly, strong buying habits
- **Low Frequency** = Customers purchase infrequently, irregular buying patterns

## 📈 Segment Performance Analysis

### **🏆 Top Performing Segments (High Frequency)**
- **"Championship Customers" (113.7)**: Elite customers with extremely high purchase frequency
- **"Loyal Customers" (99.1)**: Highly loyal customers with consistent purchasing behavior
- **"Cannot Lose" (69.9)**: Important customers with strong purchase frequency

### **⚠️ Segments Needing Improvement (Low Frequency)**
- **"New Customers" (11.1)**: New customers with low frequency (need habit-building time)
- **"At Risk" (21.7)**: At-risk customers with infrequent purchasing patterns
- **"Low Customers" (17.2)**: Low-engagement customers requiring attention

## 🔄 Integrated RFM Strategy

| Priority Level | R/F Combination (Recency/Frequency) | Equivalent Customer Group | Strategic Objective |
| :--- | :--- | :--- | :--- |
| **High Priority** | **High Frequency + Low Recency** | Gold Customers | **Retention & Growth:** Maintain engagement and maximize Lifetime Value (LTV). |
| **High Priority** | **Low Frequency + High Recency** | Win-back Focus | **Reactivation:** Rescue customers with the highest risk of churning. |
| **High Priority** | **High Frequency + High Recency** | Potential Champions | **Nurturing:** Personalized intervention to guide them back to regular purchasing behavior. |
| **Medium Priority** | **Medium Frequency + Medium Recency** | Growth Opportunities | **Development:** Focus on campaigns to increase purchase frequency and strengthen engagement. |

## 📋 Action Plan & Performance Tracking 

| Strategic Area | Key Metrics to Monitor (KPIs) | Core Actions (By Timeline) |
| :--- | :--- | :--- |
| **Performance Tracking** | Frequency improvement (for low segments), Retention rates (for high-frequency segments), Conversion rate (low to medium frequency), LTV by Frequency segment. | **Optimization Strategies:** A/B test frequency-building campaigns, Segment-specific communication frequency, Personalized product recommendations. |
| **Immediate Actions (0-30 days)** | Optimize **Recency & Frequency** | 1. Launch **reactivation campaigns** for the At Risk segment. 2. Implement **onboarding** for New Customers. 3. Develop **VIP program** for Championship customers. |
| **Medium Term (30-90 days)** | Enhance **Purchase Frequency** | 1. Create **frequency-building ladder** campaigns. 2. Develop segment-specific **communication strategies**. 3. Implement **loyalty program enhancements**. |
| **Long Term (90+ days)** | **Automation & Personalization** | 1. Advanced personalization based on frequency patterns. 2. **Predictive modeling** for frequency optimization. 3. Automate full **lifecycle marketing programs**. |

[In 22]:
```python
fig, ax1 = plt.subplots(figsize=(25,8))
bars = ax1.bar(grp_total['Segment'], grp_total['Count ID'], color='#A3C4F3', label='Customer Count')
ax2 = ax1.twinx()
line = ax2.plot(grp_total['Segment'], grp_total['Monetary'], color='#E07A5F', marker='o', label='Monetary Value')
for bar in bars:
    height = bar.get_height()
    ax1.text(bar.get_x() + bar.get_width()/2, height, f'{height:.0f}',
             ha='center', va='bottom', fontsize=10, color='#3A6EA5', fontweight='bold')
for i, v in enumerate(grp_total['Monetary']):
    ax2.text(i, v, f'{v:,.0f}', color='#E07A5F', fontsize=10, ha='center', va='bottom', fontweight='bold')
ax1.set_xlabel('Segment', fontsize=12, fontweight='bold')
ax1.set_ylabel('Customer Count', color='black', fontsize=12, fontweight='bold')
ax2.set_ylabel('Monetary Value', color='black', fontsize=12, fontweight='bold')
plt.title('Customer Count vs Monetary by Segment', fontsize=16, fontweight='bold')
plt.xticks(rotation=45, ha='right', fontsize=11, fontweight='bold')
lines, labels = ax1.get_legend_handles_labels()
lines2, labels2 = ax2.get_legend_handles_labels()
ax1.legend(lines + lines2, labels + labels2,
            loc='upper right', fontsize=11, frameon=True, facecolor='white',
            edgecolor='gray', title='Legend', title_fontsize=12)
plt.tight_layout()
plt.show()

```
[Out 22]:

<img width="913" height="312" alt="image" src="https://github.com/user-attachments/assets/ccd405a3-3633-4f7c-b085-f91d994678fd" />

### 📊 Chart Summary: Customer Count vs Monetary Value by Segment

The provided chart compares two key metrics—**Customer Count** (light blue bars) and **Monetary Value** (orange/red line) across 10 distinct customer segments.

---

### 🔑 Detailed Segment Analysis

The segments can be grouped based on their contribution and performance:

#### 1. High-Performance / High-Value Segments

| Segment | Customer Count | Monetary Value | Key Insight |
| :--- | :--- | :--- | :--- |
| **🏆 Champions** | 300 | **655,9** (Highest) | This group yields the **highest monetary value**, making them the most valuable in terms of revenue contribution. |
| **🥈 At Risk** | 369 | 453,380 (2nd Highest) | High value, but potentially unstable. Requires retention strategies. |
| **Loyal** | 334 | 566,604 (3rd Highest) | Very high value relative to the customer count, indicating high profitability per customer. |
| **🥇 Hibernating Customers** | **789** (Highest) | 319, (Moderate/High) | The **largest segment by count**, and still contributes a significant monetary value. They need reactivation efforts. |

#### 2. Potential and Moderate Segments

| Segment | Customer Count | Monetary Value | Key Insight |
| :--- | :--- | :--- | :--- |
| **Potential Loyalist** |  (2nd Highest) | 287,697 | A large group with good value. They are prime candidates for conversion into "Loyal" customers. |
| **New Customers** | 308 | 64,654 | Moderate count, but low value. Focus should be on onboarding and first purchase retention. |
| **About To Sleep** | 187 | 54,420 | Low count and low value, suggesting they are on the verge of becoming "Lost Customers." |
| **Need Attention** | 220 | 252,915 | Moderate value, but low count. Strategies are needed to prevent defection. |

#### 3. Lowest Performance Segments

| Segment | Customer Count | Monetary Value | Key Insight |
| :--- | :--- | :--- | :--- |
| **Cannot Lose Them** | **79** (Lowest) | 107,765 | The smallest segment, but the monetary value is not the absolute lowest, implying a high **value per individual** customer. They must be prioritized for special retention campaigns. |
| **Lost Customers** | 367 | **65,422** (Lowest) | A large group by count that currently provides very little value. |
| **Promising** | 127 | 114,517 | Very low count and low value. |

---

### 🚀 Key Takeaways

1.  **Focus on Value:** The **"Champions"** segment, while not the largest, drives the most revenue and should be highly prioritized.
2.  **Activate Volume:** The largest groups, **"Hibernating Customers"** and **"Potential Loyalist,"** represent the biggest opportunity for future growth if successfully engaged.
3.  **Prevent Churn:** Special attention is needed for **"At Risk"** and **"Cannot Lose Them"** customers, as they represent high value that could easily be lost.
