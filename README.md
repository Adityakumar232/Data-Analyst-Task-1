# Data-Analyst-Task-1
Task 1: Data Cleaning & Preprocessing – Summary
🔹 Dataset Overview

Dataset: Sample Sales Data (10 rows, 7 columns)

Issues found: Missing values, duplicate rows, inconsistent text formats, mixed date formats, irregular column headers, wrong data types

🔹 Cleaning Steps Performed

Missing Values

QuantityOrdered → filled with median value

PriceEach → filled with mean value

Sales → filled with median value

Rows with missing OrderNumber → removed

Duplicates

Identified duplicate rows using OrderNumber + Product info

Removed duplicate entries (kept first occurrence)

Text Standardization

Country column → converted to uppercase and standardized (e.g., “U.S.A” → “USA”, “UK/uk” → “UNITED KINGDOM”)

CustomerName → trimmed spaces and converted to Proper Case (e.g., " alice " → "Alice")

Date Format Consistency

Converted all OrderDate values into dd-mm-yyyy format

Column Headers

Renamed headers to clean, lowercase, and underscore-separated (e.g., OrderNumber → ordernumber)

Data Types

Ensured QuantityOrdered, PriceEach, and Sales are numeric

OrderDate converted to datetime (then formatted as dd-mm-yyyy)

PostalCode and Phone kept as text to preserve leading zeroes

🔹 Final Outcome

Original dataset: 10 rows, 7 columns (with errors)

Cleaned dataset: 9 rows, 7 columns (duplicates + null rows removed)

Deliverables produced:

raw_sales_data.csv / raw_sales_data.xlsx (original)

cleaned_sales_data.csv / cleaned_sales_data.xlsx (processed)

summary.txt (this document)
