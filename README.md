# Credit Risk Analysis Project

## Overview
This project performs **Exploratory Data Analysis (EDA)** on a credit risk dataset to investigate the relationship between income levels, loan percentages, and default risk. The key finding reveals that when the **loan-to-income ratio exceeds 50%**, borrowers typically have very low income levels, indicating that **lower-income individuals tend to take on riskier loans**.

## Table of Contents
- [Dependencies](#dependencies)
- [Data Description](#data-description)
- [Features](#features)
- [Analysis Components](#analysis-components)
- [Key Findings](#key-findings)
- [Interactive Dashboard](#interactive-dashboard)
- [Installation and Usage](#installation-and-usage)
- [Contributing](#contributing)
- [License](#license)

## Dependencies
Install required packages using:

```bash
pip install pandas numpy scipy matplotlib seaborn panel hvplot holoviews statsmodels
```

## Data Description
The analysis uses a credit risk dataset (`credit_risk_dataset.csv`) containing information about borrowers, including:

- **Personal income**
- **Loan status** (default/non-default)
- **Loan percentage of income**
- **Other relevant financial metrics**

## Features
### 1. Data Preprocessing
- Income normalization using log transformation
- Outlier detection using z-score method
- Missing value handling
- Statistical computations of mean and standard deviation

### 2. Statistical Analysis
- Normality testing using Q-Q plots
- **ECDF** (Empirical Cumulative Distribution Function) computation
- Covariance analysis between income and loan percentages
- Quantile analysis of income distribution

### 3. Visualization Components
- **Distribution plots** for original and log-transformed income
- **Q-Q plots** for normality assessment
- **Interactive scatter plots** showing income vs. loan percentage
- **Violin plots** for income distribution by default status

## Analysis Components
### Income Analysis
```python
# Log transformation of income
df['log_person_income'] = np.log(df['person_income'])
```

### Outlier Detection
```python
def detect_outliers(data):
    outliers = []
    threshold = 3
    for i in data['person_income']:
        z_score = (i - mean_person_income) / std_person_income
        if np.abs(z_score) > threshold:
            outliers.append(i)
    return outliers
```

### Distribution Analysis
The project implements ECDF computation for analyzing income distribution:
```python
def compute_ecdf(group, column):
    ecdf = ECDF(group[column])
    return ecdf
```

### Risk Assessment
Covariance analysis for loan risk assessment:
```python
threshold = 0.50
covariance_matrix = df[df['loan_percent_income'] > threshold][['log_person_income', 'loan_percent_income']].cov()
```

## Interactive Dashboard
The project includes an **interactive dashboard** built with **Panel** that features:

### **Income Distribution Visualization**
- **Histogram** with adjustable income threshold
- **Log-transformed** income distribution

### **Risk Analysis Components**
- **Scatter plot** of income vs. loan percentage
- **Default status** highlighting
- **Violin plot** for income distribution by default status

### **Key Metrics Display**
- Default rate
- Median income
- Median loan percentage
- High-risk loan percentage

### **Threshold Analysis**
- **Adjustable loan/income threshold**
- **Dynamic risk metrics updates**

## Key Findings
The primary conclusion of the analysis reveals:
- A **significant correlation** between low income levels and high loan-to-income ratios
- When the **loan-to-income ratio exceeds 50%**, borrowers predominantly fall into **lower income brackets**
- This suggests a **potential systemic risk** where lower-income individuals are taking on proportionally larger loans

## Installation and Usage
1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/credit-risk-analysis.git
   ```
2. **Install required dependencies:**
   ```bash
   pip install pandas numpy scipy matplotlib seaborn panel hvplot holoviews statsmodels
   ```
3. **Run the analysis:**
   ```bash
   python credit_risk_analysis.py
   ```
4. **Access the dashboard:**
   ```bash
   panel serve credit_risk_analysis.py
   ```

## Contributing
Feel free to **fork** this repository and submit **pull requests**. For major changes, please open an issue first to discuss what you would like to change.

## License
This project is licensed under the **MIT License**.
