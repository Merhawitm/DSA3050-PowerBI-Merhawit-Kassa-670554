Output

# Section A: Dataset Selection & Understanding

## 1. Source of the Dataset
The dataset used is the **Online Retail II** dataset, originally published on the
**UCI Machine Learning Repository** (https://archive.ics.uci.edu/dataset/502/online+retail+ii)
and also mirrored on Kaggle. It is a real transactional dataset released for public research
and educational use.

## 2. What the Dataset Represents
The dataset contains **all transactions occurring between 01/12/2009 and 09/12/2011** for a
UK-based, registered, non-store online retailer that primarily sells unique all-occasion
giftware. Each row represents a single line item within a customer invoice/order — i.e. one
product purchased in one transaction, including its quantity, unit price, the customer who
purchased it, the date/time of purchase, and the country of the customer.

Key facts about the raw file used:
- **1,067,371 rows**, 8 columns
- Spans a full **two-year period** (Dec 2009 – Dec 2011)
- **43 countries**, 5,942 unique customers, 5,305 unique products

## 3. Why This Dataset Was Selected
This dataset was selected because it is a genuine, unaggregated transactional log rather than
a pre-cleaned summary table, which allows for meaningful data cleaning, modelling and DAX work
rather than simply visualizing numbers that are already business-ready. Specifically, it
contains real-world data quality issues that must be resolved before analysis, including:

- **243,007 missing Customer IDs** (~23% of rows) — many purchases cannot be tied to a
  registered customer
- **4,382 missing product Descriptions**
- **22,950 rows with negative Quantity** (returns/adjustments)
- **6,207 rows with zero or negative Price** (data entry errors or non-sale adjustments)
- **19,494 cancelled invoices** (Invoice numbers prefixed with "C")
- **34,335 fully duplicated rows**
- Inconsistent **StockCode** formats (purely numeric codes vs. alphanumeric codes such as
  "85132B") requiring standardization decisions

These issues make the dataset well suited to demonstrate the full breadth of Power Query
transformations required by this examination, rather than a simple import-and-load exercise.

## 4. Main Variables Available

| Column | Type | Description |
|---|---|---|
| Invoice | Categorical/Text | Unique invoice number; prefixed "C" indicates a cancellation |
| StockCode | Categorical/Text | Unique product/item code |
| Description | Categorical/Text | Product name |
| Quantity | Numeric | Number of units purchased (can be negative for returns) |
| InvoiceDate | Date/Time | Date and time the transaction occurred |
| Price | Numeric | Unit price of the product (£) |
| Customer ID | Categorical/Numeric ID | Unique identifier for the customer (many missing) |
| Country | Categorical/Text | Country of the customer |

An engineered field, **Revenue** (Quantity × Price), will be created during Power Query to
serve as the primary KPI base measure.

## 5. Business/Analytical Problem
The business problem investigated is: **How can this online retailer better understand its
sales performance, customer behaviour, and product/geographic trends in order to improve
revenue, reduce losses from cancellations/returns, and identify growth opportunities?**

The analysis moves from descriptive performance (what happened) through customer and
product-level detail (where/who) to diagnostic questions around cancellations and returns
(why performance dips occur).

## 6. Analytical Questions the Power BI Solution Should Answer
1. What is the overall revenue trend across the two-year period, and are there seasonal
   patterns (e.g. peaks around holiday periods)?
2. Which countries and customers generate the most revenue, and how concentrated is revenue
   among the top customers/countries?
3. Which products/product categories are the best and worst performers by revenue and
   quantity sold?
4. What proportion of transactions are cancellations or returns, and which
   products/countries/time periods have the highest cancellation rates?
5. How does year-over-year revenue growth compare between 2010 and 2011, and which
   months/quarters show the strongest growth or decline?
6. What is the average order value, and how does it vary by country or customer segment?
7. Are there identifiable customer segments (e.g. by purchase frequency or spend) that
   contribute disproportionately to revenue?
