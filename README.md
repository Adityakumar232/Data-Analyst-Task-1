# Data-Analyst-Task-1
import pandas as pd
import matplotlib.pyplot as plt

# Step 1: Create a synthetic raw sales dataset with common issues (missing values, duplicates, inconsistent text, mixed date formats)
raw_data = {
    "OrderNumber": [101, 102, 102, 104, None, 106, 107, 108, 109, 110],
    "QuantityOrdered": [5, None, 10, 7, 3, 8, None, 6, 2, 4],
    "PriceEach": [20.5, 15.0, 15.0, None, 12.5, 25.0, 18.0, None, 30.0, 22.0],
    "Sales": [102.5, 150.0, 150.0, None, 37.5, 200.0, 90.0, None, 60.0, 88.0],
    "OrderDate": ["01-02-2020", "2020/03/05", "2020/03/05", "05-04-2020", "2020-05-06",
                  "06-06-2020", "07/07/2020", "2020.08.08", "09-09-2020", "2020/10/10"],
    "Country": ["India", "india", "INDIA", "Usa", "USA", "usa", "U.S.A", "UK", "United Kingdom", "uk"],
    "CustomerName": [" Alice ", "bob", "Bob", "CHARLIE", "David", "Eva", " frank", "George", "Henry", "Isla"]
}

raw_df = pd.DataFrame(raw_data)

# Step 2: Clean the dataset
clean_df = raw_df.copy()

# Remove duplicates
clean_df = clean_df.drop_duplicates()

# Handle missing values
clean_df['QuantityOrdered'] = clean_df['QuantityOrdered'].fillna(clean_df['QuantityOrdered'].median())
clean_df['PriceEach'] = clean_df['PriceEach'].fillna(clean_df['PriceEach'].mean())
clean_df['Sales'] = clean_df['Sales'].fillna(clean_df['Sales'].median())
clean_df = clean_df.dropna(subset=['OrderNumber'])

# Standardize text
clean_df['Country'] = clean_df['Country'].str.upper().replace({
    "U.S.A": "USA", "UK": "UNITED KINGDOM"
})
clean_df['CustomerName'] = clean_df['CustomerName'].str.strip().str.title()

# Convert dates
clean_df['OrderDate'] = pd.to_datetime(clean_df['OrderDate'], errors='coerce', dayfirst=True)
clean_df['OrderDate'] = clean_df['OrderDate'].dt.strftime("%d-%m-%Y")

# Standardize column headers
clean_df.columns = [c.lower() for c in clean_df.columns]

# Step 3: Create side-by-side photo (Raw vs Cleaned preview)
fig, axes = plt.subplots(2, 1, figsize=(12, 6))

# Raw preview
axes[0].axis('off')
axes[0].set_title("Raw Sales Data (Sample with Issues)", fontsize=14, fontweight="bold")
axes[0].table(cellText=raw_df.head(8).values, colLabels=raw_df.columns, cellLoc='center', loc='center')

# Cleaned preview
axes[1].axis('off')
axes[1].set_title("Cleaned Sales Data (After Processing)", fontsize=14, fontweight="bold")
axes[1].table(cellText=clean_df.head(8).values, colLabels=clean_df.columns, cellLoc='center', loc='center')

plt.tight_layout()
plt.show()
