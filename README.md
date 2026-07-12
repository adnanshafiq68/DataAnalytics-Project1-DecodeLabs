# DataAnalytics-Project1-DecodeLabs
# Project 1: Data Cleaning & Preparation — DecodeLabs

## 📌 Objective
This project is the foundation phase of the DecodeLabs Data Analytics Internship track. 
The goal was to take a raw e-commerce orders dataset and transform it into a clean, 
reliable, analysis-ready dataset by identifying missing values, checking for duplicates, 
and correcting data formats — using a fully reproducible workflow.

## 🛠️ Tools Used
- Microsoft Excel — **Power Query**

## 📂 Dataset Overview
- **Rows:** 1,200 order records
- **Columns:** 14 (OrderID, Date, CustomerID, Product, Quantity, UnitPrice, 
  ShippingAddress, PaymentMethod, OrderStatus, TrackingNumber, ItemsInCart, 
  CouponCode, ReferralSource, TotalPrice)

## 🔍 Cleaning Process (via Power Query)

### 1. Data Import
Loaded the raw dataset into Excel via **Data → Get Data → From File → From Workbook**, 
then opened it in the Power Query Editor for transformation.

### 2. Missing Value Handling
- Identified **309 blank values** in the `CouponCode` column.
- Since `CouponCode` is a categorical field (not numeric), mean/median imputation 
  was not applicable.
- Applied business logic: a blank value means the customer did not use a coupon.
- Replaced all blanks with **"No Coupon"** to preserve all 309 records rather 
  than deleting them (avoiding loss of statistical power).

### 3. Duplicate Check
- Ran **Remove Duplicates** on the `OrderID` column (the unique identifier).
- Result: **0 duplicate records found** — all 1,200 OrderIDs are unique.
- Also cross-verified using a full-row duplicate check — confirmed clean.

### 4. Data Format Correction
- Set explicit data types for every column using **Change Type → Using Locale**, 
  ensuring dates, numbers, and text were parsed correctly and consistently 
  (e.g., `Date` column parsed as proper Date type using the correct regional 
  locale, avoiding day/month misreads).
- Standardized numeric columns (`UnitPrice`, `TotalPrice`) to 2 decimal precision.
- Verified `TotalPrice = Quantity × UnitPrice` holds true across all 1,200 rows.
- Applied Trim and Proper Case formatting to text columns (`Product`, 
  `PaymentMethod`, `OrderStatus`, `ReferralSource`) to catch any hidden 
  whitespace or casing inconsistencies — confirmed already clean.

### 5. Load
Cleaned data was loaded to a new sheet (`cleaned_data`) via **Close & Load To**, 
keeping the original raw dataset fully intact and untouched for audit purposes.

## 📋 Change Log

| Change ID | Description | Impact | Status |
|-----------|-------------|--------|--------|
| CR001 | Filled 309 blank `CouponCode` values with "No Coupon" | Preserved 309 records for analysis | ✅ Resolved |
| CR002 | Verified 0 duplicate `OrderID` values across 1,200 rows | No action needed | ✅ Verified |
| CR003 | Set correct data types using Change Type → Using Locale | Ensured accurate date/number parsing | ✅ Resolved |
| CR004 | Verified `TotalPrice` = `Quantity` × `UnitPrice` for all rows | No pricing errors found | ✅ Verified |
| CR005 | Trimmed and standardized casing on text columns | No inconsistencies found | ✅ Verified |

## ✅ Result
- **0%** error rate on unique identifiers (duplicate OrderIDs)
- **0%** error rate on date formats
- **100%** of missing values handled with documented business logic
- Dataset is now production-ready for downstream analysis and reporting

## 📁 Files
- `raw_data.xlsx` — original, unmodified dataset
- `cleaned_data.xlsx` — cleaned dataset produced via Power Query

## 👤 Author
Adnan Shafq — Data Analytics Intern, DecodeLabs (Batch 2026)
