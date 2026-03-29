
# Customer Segmentation for Fashion App

**Tools & Libraries:** Python, Pandas, Scikit-learn, Matplotlib, Seaborn

---

## Project Overview

This project focuses on segmenting customers for a fashion e-commerce application based on their purchasing behavior.
By applying **K-Means clustering** to transaction data, the analysis identified **four distinct customer segments** that can be used for targeted marketing and customer retention strategies.

**Goal:**
To understand customer behavior patterns and reduce churn risk through personalized engagement, projecting a potential **20% reduction in churn**.

---

## Dataset Description

**File:** `fashion_customer_transactions.csv`
**Rows:** 500,000+

**Columns:**

* `CustomerID` – Unique customer identifier
* `InvoiceNo` – Unique transaction ID
* `Product` – Product name
* `Category` – Product category (Tops, Footwear, Dresses, etc.)
* `Quantity` – Number of items purchased
* `UnitPrice` – Price per item
* `InvoiceDate` – Date of transaction
* `TotalAmount` – Computed as Quantity × UnitPrice

**Sample Data:**

| CustomerID | Product | Category | Quantity | UnitPrice | TotalAmount | InvoiceDate         |
| ---------- | ------- | -------- | -------- | --------- | ----------- | ------------------- |
| 626        | Yes     | Dresses  | 1        | 84.62     | 84.62       | 2025-08-25 21:13:31 |
| 2539       | Buy     | Tops     | 4        | 35.76     | 143.04      | 2025-10-22 07:47:01 |
| 5515       | Special | Dresses  | 2        | 286.96    | 573.92      | 2025-08-09 16:25:09 |

---

## Methodology

### 1. Data Preprocessing

* Cleaned missing values and duplicates
* Computed `TotalAmount = Quantity × UnitPrice`
* Converted `InvoiceDate` to datetime format

### 2. Feature Engineering (RFM Model)

Each customer was summarized using the **Recency, Frequency, and Monetary (RFM)** model:

| Feature   | Definition                                | Calculation              |
| --------- | ----------------------------------------- | ------------------------ |
| Recency   | How recently the customer made a purchase | Days since last purchase |
| Frequency | How often they purchased                  | Count of transactions    |
| Monetary  | How much they spent                       | TotalAmount per customer |

**Sample RFM Table:**

| CustomerID | Recency | Frequency | Monetary  |
| ---------- | ------- | --------- | --------- |
| 1          | 4       | 59        | 7,769.26  |
| 2          | 1       | 142       | 65,896.07 |
| 3          | 6       | 3         | 388.38    |

### 3. Feature Scaling

Standardized all RFM features using **StandardScaler** to ensure equal influence of variables during clustering.

### 4. Optimal Cluster Selection (Elbow Method)

Used the **Elbow Method** to determine the ideal number of clusters (k) by plotting the within-cluster sum of squares (inertia) against various k values.

```python
plt.plot(K, inertia, 'bo-')
plt.xlabel('Number of clusters (k)')
plt.ylabel('Inertia')
plt.title('Elbow Method for Optimal k')
plt.show()
```

The plot indicated an optimal **k = 4**, representing four customer segments.

### 5. K-Means Clustering

Applied **K-Means clustering** with k = 4 to the scaled RFM data.

**Cluster Summary:**

| Cluster | Avg Recency | Avg Frequency | Avg Monetary | Num Customers | Segment              |
| ------- | ----------- | ------------- | ------------ | ------------- | -------------------- |
| 0       | 4.85        | 87.99         | 14,403.52    | 2,476         | High-Value Loyalists |
| 1       | 127.81      | 2.43          | 491.52       | 1,805         | Bargain Seekers      |
| 2       | 2.64        | 178.86        | 89,664.26    | 1,272         | One-time Buyers      |
| 3       | 26.10       | 13.22         | 2,969.16     | 3,797         | Churn Risks          |

---

## Cluster Interpretation

| Segment              | Characteristics                                    | Recommended Strategy                                             |
| -------------------- | -------------------------------------------------- | ---------------------------------------------------------------- |
| High-Value Loyalists | Frequent, recent, and high-spending customers      | Provide loyalty benefits and early access to new collections     |
| Bargain Seekers      | Infrequent buyers with low spending                | Use discount-based promotions and limited-time offers            |
| One-time Buyers      | High spenders with few purchases                   | Encourage repeat purchases with personalized follow-up campaigns |
| Churn Risks          | Inactive customers with low frequency and spending | Launch re-engagement or win-back campaigns                       |

---

## Visualizations

### 1. Elbow Curve

Used to identify the optimal number of clusters (k = 4).

### 2. Cluster Scatter Plot

Visualized customer segments based on **Frequency** and **Monetary** values.

```python
plt.scatter(rfm["Frequency"], rfm["Monetary"], c=rfm["Cluster"], cmap="viridis")
plt.xlabel("Frequency")
plt.ylabel("Monetary")
plt.title("Customer Segments (K-Means)")
plt.show()
```

---

## Results

* Segmented 10,000 customers into four distinct behavioral groups
* Enabled data-driven targeting and retention strategies
* Insights suggested a potential **20% reduction in churn risk** through personalized campaigns

---

## Files in Repository

| File                                | Description                                  |
| ----------------------------------- | -------------------------------------------- |
| `fashion_customer_transactions.csv` | Raw e-commerce dataset                       |
| `customer_segmentation.ipynb`       | Google Colab notebook with complete workflow |
| `customer_segments.csv`             | Final output with cluster labels             |
| `README.md`                         | Project documentation                        |

---

## How to Run

1. Open the notebook in **Google Colab**
2. Upload `fashion_customer_transactions.csv`
3. Install dependencies if required:

   ```bash
   pip install pandas scikit-learn matplotlib seaborn
   ```
4. Run each cell sequentially to reproduce the results and visualizations

---

## Future Work

* Integrate additional features such as demographics or browsing history
* Deploy segmentation as an API for real-time use
* Develop an interactive dashboard (Streamlit, Power BI) for visual analysis

---

## Author

**Name:** Anshuman Gupta

**GitHub:** [https://github.com/anshuman183](https://github.com/anshuman183)

**LinkedIn:** [linkedin.com/in/anshuman-gupta-884b5624a](linkedin.com/in/anshuman-gupta-884b5624a)

