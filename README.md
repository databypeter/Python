# Online Retail UK - Data Quality & Exploratory Analysis

## Project Overview

This project performs comprehensive data quality assessment and exploratory data analysis (EDA) on the Online Retail dataset from a UK-based non-store online retail company. The dataset contains transactional data from December 2010 to December 2011, including information about invoices, products, quantities, prices, customers, and countries.

The analysis focuses on:
- Data quality assessment and validation
- Outlier detection and treatment
- Missing value handling
- Data standardization and optimization
- Exploratory data analysis to uncover business insights

## Dataset Information

**Original Dataset:**
- **Records**: 541,909 transactions
- **Features**: 9 columns (InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, Country, Revenue)
- **Date Range**: December 1, 2010 - December 9, 2011
- **Source**: UK-based online retail company

**Key Columns:**
- `InvoiceNo`: Invoice number (categorical)
- `StockCode`: Product code (categorical)
- `Description`: Product name (categorical)
- `Quantity`: Quantity of items purchased (numerical)
- `InvoiceDate`: Date and time of transaction (datetime)
- `UnitPrice`: Price per unit (numerical)
- `CustomerID`: Customer identifier (categorical)
- `Country`: Customer's country (categorical)
- `Revenue`: Total revenue (Quantity × UnitPrice) (numerical)

## Key Analysis Steps

### 1. Data Quality Assessment

**Outlier Detection:**
- Used both IQR (Interquartile Range) and Z-score methods
- IQR method identified: 58,619 outliers in Quantity, 39,627 in UnitPrice, 44,997 in Revenue
- Z-score method (threshold > 3) identified: 346 outliers in Quantity, 374 in UnitPrice, 403 in Revenue
- Visualized outliers using boxplots and scatter plots

**Duplicate Records:**
- Detected and removed 5,268 duplicate rows

**Missing Values:**
- Original dataset: 1,454 missing values in Description, 135,080 in CustomerID
- After cleaning: All missing values handled

### 2. Outlier Handling

**Treatment Strategy:**
- Removed extreme outliers based on Z-score > 3 threshold
- Analyzed outlier patterns by:
  - Product descriptions (e.g., "DOTCOM POSTAGE", "Manual")
  - Customer IDs (identified high-frequency outlier customers)
  - Countries (United Kingdom had the most outlier transactions)
- Rows reduced from 541,909 to 540,997 after outlier removal

### 3. Missing Value Imputation

**Imputation Strategy:**
- **Description column**: Imputed with mode ("WHITE HANGING HEART T-LIGHT HOLDER")
- **CustomerID column**: Imputed with placeholder value "Unknown" for non-identifiable transactions

### 4. Data Standardization

**Text Standardization:**
- Converted Description, Country, and CustomerID to lowercase
- Stripped whitespace from text fields

**Numerical Standardization:**
- Applied StandardScaler to Quantity, UnitPrice, and Revenue
- Ensures all numerical features have mean ≈ 0 and standard deviation ≈ 1

**Data Type Optimization:**
- Converted InvoiceDate to datetime objects
- Converted categorical columns to category dtype for memory efficiency
- Properly typed numerical columns

### 5. Exploratory Data Analysis (EDA)

**Univariate Analysis:**
- Distribution analysis of numerical variables (Quantity, UnitPrice, Revenue)
- Frequency analysis of categorical variables
- Top 10 countries: United Kingdom dominates with 489,486 transactions
- Top products: "WHITE HANGING HEART T-LIGHT HOLDER" (3,785 occurrences)
- Top customers identified by transaction frequency

**Bivariate Analysis:**
- Correlation analysis between numerical variables:
  - Strong positive correlation (0.646) between Quantity and Revenue
  - Weak positive correlation (0.144) between UnitPrice and Revenue
  - Weak negative correlation (-0.080) between Quantity and UnitPrice
- Visualized relationships using scatter plots and heatmaps
- Box plots comparing distributions across top 10 countries

## Major Findings

### Data Quality Insights

1. **Outliers**: Both detection methods revealed significant outliers, with IQR being more sensitive. The Z-score method was chosen for removal to preserve more data while eliminating extreme values.

2. **Missing Customer IDs**: 24.9% of transactions had missing CustomerID values, suggesting anonymous purchases or data collection issues.

3. **Duplicates**: 0.97% of records were exact duplicates, indicating potential data entry issues.

4. **Data Reduction**: Final cleaned dataset contains 535,731 records (98.9% of original data retained).

### Business Insights

1. **Geographic Concentration**: 
   - United Kingdom accounts for ~91% of all transactions
   - Other significant markets: Germany (1.8%), France (1.6%), EIRE (1.5%)

2. **Product Popularity**:
   - Home décor and gift items dominate (t-light holders, cake stands, retrospot bags)
   - "WHITE HANGING HEART T-LIGHT HOLDER" is the most frequently purchased item

3. **Customer Behavior**:
   - Top customer (17841.0) made 7,812 transactions
   - Significant variance in customer purchase frequency

4. **Revenue Patterns**:
   - Revenue strongly correlates with quantity purchased
   - Unit price has minimal impact on total revenue correlation

## How to Run the Notebook

### Prerequisites

```python
pip install pandas numpy matplotlib seaborn plotly scikit-learn scipy
```

### Running in Google Colab

1. **Upload the Dataset**:
   - Open the notebook in Google Colab
   - Upload your `data.csv` file when prompted by the file upload widget
   - Ensure the file is saved as `/content/data.csv`

2. **Run the Cells**:
   - Execute cells sequentially from top to bottom
   - The notebook is organized into sections:
     - Setup and Data Cleaning
     - Data Overview
     - Data Quality Assessment & Outlier Detection
     - Outlier Investigation
     - Outlier Treatment Decisions
     - Missing Data Handling
     - Data Type Optimization & Standardization
     - Cleaned Data Validation
     - Exploratory Data Analysis (EDA)

3. **Export Cleaned Data** (Optional):
   - Uncomment the export line in the final cell:
     ```python
     df_cleaned.to_csv('cleaned_data.csv', index=False)
     ```
   - Download the cleaned dataset from Colab

### Key Libraries Used

- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing
- **matplotlib & seaborn**: Data visualization
- **plotly**: Interactive visualizations
- **scikit-learn**: StandardScaler for data normalization
- **scipy**: Statistical functions (Z-score calculation)

## Project Structure

```
Online-Retail-UK/
│
├── README.md                          # This file
├── Online_retail_UK.ipynb             # Main Jupyter notebook with analysis
├── data.csv                           # Original dataset (not included)
└── cleaned_data.csv                   # Cleaned dataset (generated after running notebook)
```

## Results Summary

**Before Cleaning:**
- 541,909 total records
- 1,454 missing descriptions
- 135,080 missing customer IDs
- 5,268 duplicate rows
- Significant outliers in all numerical columns

**After Cleaning:**
- 535,731 total records (98.9% retention)
- 0 missing values
- 0 duplicate rows
- Outliers removed (Z-score > 3)
- Standardized text and numerical data

**Key Metrics:**
- Data quality improved significantly
- All columns properly typed and optimized
- Ready for downstream analysis and modeling

## Future Work

1. **Customer Segmentation**: Apply clustering algorithms (K-means, DBSCAN) to identify customer segments
2. **Time Series Analysis**: Analyze seasonal trends and patterns in purchasing behavior
3. **Market Basket Analysis**: Identify frequently co-purchased products using association rules
4. **Predictive Modeling**: Build models to predict customer churn, revenue, or product demand
5. **Cohort Analysis**: Study customer retention and behavior over time

## License

This project is open source and available under the MIT License.

## Contact

For questions or feedback, please contact: tranquangduc242@gmail.com

## Acknowledgments

- Dataset source: UCI Machine Learning Repository - Online Retail Dataset
- Analysis performed as part of data quality and EDA practice project
