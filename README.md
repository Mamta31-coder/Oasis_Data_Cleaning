# 🧹 Retail Store Sales — Data Cleaning and Preprocessing

## 📌 Project Overview

This project focuses on cleaning and preprocessing a retail sales dataset using Python and Pandas. The objective is to identify data quality issues, investigate missing values, detect duplicate records, validate numerical data, and prepare a cleaned dataset for further analysis.

The project demonstrates a structured data-cleaning workflow, from initial data inspection to final validation and export.

## 🎯 Project Objectives

- Understand the structure and quality of the raw dataset.
- Identify and analyze missing values.
- Detect duplicate records and transaction IDs.
- Investigate invalid numerical values.
- Validate the relationship between unit price, quantity, and total spending.
- Apply appropriate missing-value handling techniques.
- Standardize column names and text values.
- Validate the cleaned dataset.
- Export the processed dataset for future analysis.

## 🛠️ Tools and Technologies

| Tool | Purpose |
|---|---|
| Python | Data cleaning and preprocessing |
| Pandas | Data manipulation and analysis |
| NumPy | Numerical operations |
| Jupyter Notebook | Interactive analysis and documentation |
| VS Code | Development environment |
| Git and GitHub | Version control and project hosting |

## 📂 Project Structure

```text
Oasis_Data_Cleaning/
│
├── data/
│   └── raw_data.csv
│
├── notebook/
│   └── data_cleaning.ipynb
│
├── processed/
│   └── cleaned_retail_data.csv
│
├── images/
│
├── .gitignore
├── README.md
└── requirements.txt
```

### Folder Description

- **data/** — Contains the original dataset.
- **notebook/** — Contains the Jupyter Notebook with the cleaning process.
- **processed/** — Contains the cleaned dataset exported as a CSV file.
- **images/** — Reserved for project visuals, if needed.
- **requirements.txt** — Lists the Python dependencies.
- **.gitignore** — Excludes virtual environments and temporary files from version control.

## 📊 Dataset Description

The dataset contains retail transaction information, including customer details, product categories, pricing, quantities, payment methods, locations, transaction dates, and discount status.

### Key Columns

| Column | Description |
|---|---|
| `transaction_id` | Identifier for a retail transaction |
| `customer_id` | Identifier for a customer |
| `category` | Product category |
| `item` | Item description |
| `price_per_unit` | Price of one unit |
| `quantity` | Number of units purchased |
| `total_spent` | Total transaction spending |
| `payment_method` | Payment method used |
| `location` | Transaction location or channel |
| `transaction_date` | Date of the transaction |
| `discount_applied` | Indicates whether a discount was applied |

## 🔍 Data Cleaning Workflow

### 1. Initial Data Inspection

- Loaded the raw CSV file using Pandas.
- Examined the dataset dimensions and column names.
- Reviewed data types and sample records.
- Identified columns containing missing values.

### 2. Missing-Value Analysis

Calculated the number and percentage of missing values in each column.

Special attention was given to the following columns:

- `item`
- `price_per_unit`
- `quantity`
- `total_spent`
- `discount_applied`

### 3. Column Name Standardization

Standardized column names by converting them to lowercase and replacing spaces with underscores.

This made the columns easier to reference and use in Python.

### 4. Date Conversion

Converted `transaction_date` into a proper datetime data type to support reliable date-based operations.

### 5. Text Standardization

Removed unnecessary leading and trailing spaces from text values.

Rows with unavailable item descriptions were labelled as `Unknown` rather than being removed unnecessarily.

### 6. Numerical Data Validation

Investigated the numerical columns:

- `price_per_unit`
- `quantity`
- `total_spent`

Checked for zero and negative values and examined whether total spending matched the expected calculation:

**Total Spent = Price Per Unit × Quantity**

The relationship was validated against records containing complete numerical values.

### 7. Price Recovery

Recovered missing `price_per_unit` values when both `quantity` and `total_spent` were available and the quantity was nonzero.

The calculation used was:

**Price Per Unit = Total Spent ÷ Quantity**

This approach used available transaction information instead of arbitrary imputation.

### 8. Handling Incomplete Transactions

Identified 604 rows where both `quantity` and `total_spent` were missing.

These rows were removed because neither value could be reliably reconstructed from the available information.

### 9. Duplicate Detection

Checked for:

- Completely duplicated rows.
- Duplicate transaction IDs.

No complete duplicate rows or duplicate transaction IDs were identified.

### 10. Discount-Value Investigation

Investigated missing values in `discount_applied` by category, payment method, and location.

The missing values were retained because the available information did not establish whether a discount had or had not been applied.

Missing values were not automatically replaced with `True` or `False`.

### 11. Final Validation

Performed final checks on the cleaned dataset, including:

- Dataset dimensions.
- Missing-value counts.
- Duplicate records.
- Duplicate transaction IDs.
- Numerical values.
- Transaction-date validity.
- Consistency between price, quantity, and total spending.

### 12. Exporting the Cleaned Dataset

Exported the cleaned dataset to:

`processed/cleaned_retail_data.csv`

The original dataset was retained separately to preserve the raw data.

## 📈 Cleaning Results

The following results summarize the cleaning process.

| Metric | Result |
|---|---:|
| Initial rows | 12,575 |
| Rows removed | 604 |
| Final rows | 11,971 |
| Total columns | 11 |
| Complete duplicate rows detected | 0 |
| Duplicate transaction IDs detected | 0 |
| Missing prices recovered | 609 |
| Unknown item values retained | 609 |
| Missing discount values retained | 3,988 |

### Final Dataset Dimensions

- **Initial dataset:** 12,575 rows × 11 columns
- **Cleaned dataset:** 11,971 rows × 11 columns
- **Rows removed:** 604

The cleaning process removed approximately 4.80% of the original records because both quantity and total spending were missing.

## ⚠️ Data Quality Considerations

### Unknown Item Descriptions

Some transactions contained unavailable item descriptions. These were retained using the label `Unknown` to preserve potentially useful transaction information.

### Missing Discount Information

The cleaned dataset still contains 3,988 missing values in `discount_applied`.

These values were intentionally preserved because missing information cannot automatically be interpreted as a negative discount status.

### Removed Transactions

Rows with both `quantity` and `total_spent` missing were excluded from the cleaned dataset because these essential numerical values could not be reliably reconstructed.

The original raw dataset remains separate so that the cleaning process can be reviewed and reproduced.

## 🚀 How to Run the Project

### Step 1: Clone the Repository

```bash
git clone <your-repository-url>
```

Replace `<your-repository-url>` with your GitHub repository URL.

### Step 2: Navigate to the Project Directory

```bash
cd Oasis_Data_Cleaning
```

### Step 3: Create a Virtual Environment

```bash
python -m venv .venv
```

### Step 4: Activate the Virtual Environment

**Windows PowerShell:**

```powershell
.\.venv\Scripts\Activate.ps1
```

### Step 5: Install Dependencies

```bash
python -m pip install -r requirements.txt
```

### Step 6: Run the Notebook

Open the project in VS Code, open `notebook/data_cleaning.ipynb`, select the project's Python environment, and execute the notebook cells in order.

The notebook uses the raw dataset in `data/raw_data.csv` and exports the cleaned dataset to `processed/cleaned_retail_data.csv`.

## 💡 Key Learnings

Through this project, I gained practical experience in:

- Inspecting and understanding raw datasets.
- Identifying missing values and duplicates.
- Applying appropriate missing-value handling strategies.
- Standardizing column names and text values.
- Converting date columns to datetime format.
- Validating numerical relationships.
- Recovering values using reliable calculations.
- Making data-cleaning decisions based on evidence.
- Performing final data validation.
- Exporting cleaned data for further analysis.
- Organizing a data analytics project for version control.

## 🔮 Future Improvements

Potential improvements include:

- Investigating the source of missing discount information.
- Examining additional data-quality rules for transaction records.
- Adding automated data validation checks.
- Creating a reusable Python cleaning script.
- Using the cleaned dataset for exploratory data analysis.
- Developing a sales analysis dashboard in a separate project.

## 👩‍💻 Author

**Mamta Choudhary**

Aspiring Data Analyst | Python | SQL | Pandas | Power BI

---

⭐ If you find this project useful, consider starring the repository!