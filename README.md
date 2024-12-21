# Retail Sales Analysis Dashboard

## Project Objective
The goal of this project is to simulate the analysis of a real business with a dataset. The aim is to showcase skills in multiple 
tools and what I can achieve for a business. Specifically, an interactive dashboard will be developed to visualize the data, business 
situation across time, identify trends easily and extracting meaningful insights that will be useful for the company's board decisions.

## Tools Used
- **Python:** For data analysis and cleaning.
- **SQL:** For database management and querying.
- **Dash/Streamlit:** To build an interactive dashboard.
- **GitHub:** For version control and collaboration.

## Project Structure
- `data/`: Contains raw and processed data files.
- `notebooks/`: Jupyter notebooks for data exploration and analysis.
- `scripts/`: Python scripts for modular and reusable code.
- `visuals/`: Saved charts and visualizations.
- `dashboard/`: Code for the interactive dashboard.
- `reports/`: Final reports summarizing findings and insights.

## Dataset
- Source: Kaggle ([Tata Online Retail Dataset](https://www.kaggle.com/datasets/ishanshrivastava28/tata-online-retail-dataset))
- Description: Contains transaction data including InvoiceNo, StockCode, Product Descriptions, Quantity, Unit Price, CustomerID, and Country.

## Process documentation

In this section all of the process will be presented, along with any reasoning or explanations that are worth mentioning.

### Exploratory Data Analysis (EDA)
The dataset was analyzed to understand its structure, identify patterns, and uncover data quality issues. Below are the key observations and findings:

#### **1. Invoice Date Analysis**
The `InvoiceDate` column was split into separate columns:
- **Day**: Day of the month (e.g., 12).
- **Month**: Month of the year (e.g., 1 for January).
- **Year**: Year of the transaction (e.g., 2010).
- **Hour**: Hour of the transaction (e.g., 8 for 8:00 AM).

This allowed for easier seasonal and hourly analysis. Example rows after transformation:
| InvoiceDate           | Day  | Month | Year  | Hour |
|-----------------------|------|-------|-------|------|
| 2010-01-12 08:26:00  | 12.0 | 1.0   | 2010.0| 8.0  |
| 2010-01-12 08:26:00  | 12.0 | 1.0   | 2010.0| 8.0  |

---

#### **2. Missing Values**
Missing values were identified in the following columns:
| Column        | Missing Count | Percentage |
|---------------|---------------|------------|
| Description   | 1454          | 0.27%      |
| CustomerID    | 135080        | 24.93%     |
| InvoiceDate, Day, Month, Year, Hour | 308950 | 57.01% |

- **Action Plan**: `Description` has minimal missing values, but `CustomerID` has nearly 25% missing. Rows without `CustomerID` may need to be excluded for customer-specific analyses. Missing `InvoiceDate` entries will require further review.

---

#### **3. Discount Lines**
Rows where `UnitPrice` is 0 were identified as discounts:
- **Total Discount Rows:** 2,515 (0.46% of the dataset).
- Example rows:
  | InvoiceNo | StockCode | Quantity | UnitPrice | CustomerID | Country        |
  |-----------|-----------|----------|-----------|------------|----------------|
  | 536414    | 22139     | 56       | 0.0       | NaN        | United Kingdom |

- **Action Plan**: Discounts represent a small portion of the data and may be excluded unless specific discount-related analyses are planned.

---

#### **4. Negative Quantities**
Rows with negative `Quantity` values were identified, likely representing refunds:
- **Total Negative Quantity Rows:** 10,624 (1.96% of the dataset).
- Example rows:
  | InvoiceNo | Description                      | Quantity | UnitPrice | CustomerID | Country        |
  |-----------|----------------------------------|----------|-----------|------------|----------------|
  | C536379   | Discount                         | -1       | 27.50     | 14527.0    | United Kingdom |
  | C536391   | PACK OF 12 BLUE PAISLEY TISSUES  | -24      | 0.29      | 17548.0    | United Kingdom |

- **Action Plan**: These rows will be analyzed further to confirm patterns (e.g., matching refunds with original sales). Refund analysis can offer insights into return rates by product or customer.

---

#### **5. Product Purchase Patterns**
Using `CustomerID` and `InvoiceNo`, products likely to be bought together were grouped:
- Example combinations:
  | CustomerID | InvoiceNo | Products |
  |------------|-----------|----------|
  | 12346.0    | 541431    | [MEDIUM CERAMIC TOP STORAGE JAR] |
  | 12347.0    | 537626    | [BLACK CANDELABRA T-LIGHT HOLDER, AIRLINE BAG VINTAGE JET SET WHITE] |

- **Action Plan**: This data can be used for market basket analysis to identify frequently purchased combinations, aiding in cross-selling and personalized discount recommendations.




