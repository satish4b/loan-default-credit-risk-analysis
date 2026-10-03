# Loan Default & Credit Risk Analysis

## Project Overview

**Dashboard:** Loan Default & Credit Risk Analytics Dashboard\
**Tools:** Python, Pandas, Matplotlib, Seaborn, Jupyter/VS Code, Power
BI, DAX\
**Dataset:** Loan_Credit_Risk_Cleaned.csv

This project analyzes customer and loan information to understand
loan-default patterns and credit-risk indicators. The workflow covers
data cleaning, exploratory analysis, visualization, Power BI dashboard
development, and documentation.

## Objectives

-   Analyze the distribution of loan defaults.
-   Measure the overall default rate.
-   Compare default rates across loan types and employment statuses.
-   Examine credit-score and income-group patterns.
-   Analyze loan amounts by loan type and region.
-   Explore annual income versus loan amount.
-   Provide a detailed loan-level risk explorer.

## Dataset Summary

The cleaned dataset contains **8,000 records** and **24 columns**.

Important fields include Customer_ID, Gender, Age, Education,
Employment_Status, Annual_Income, Credit_Score, Loan_ID, Loan_Type,
Loan_Amount, Loan_Term_Months, Interest_Rate, Monthly_Installment,
Debt_to_Income_Ratio, Employment_Years, Previous_Defaults,
Credit_History, Property_Ownership, Region, Loan_Status, and
Default_Status.

## Key Metrics

  Metric                                 Value
  ------------------------------ -------------
  Total Customers                        8,000
  Total Loans                            8,000
  Defaulted Loans                        1,126
  Non-Defaulted Loans                    6,874
  Default Rate                          14.07%
  Average Annual Income            \$54,913.69
  Average Credit Score                  660.13
  Average Loan Amount              \$80,127.50
  Average Interest Rate                 10.44%
  Average Debt-to-Income Ratio           37.58

## Data Preparation

1.  Numeric fields were converted to numeric data types.
2.  Missing numeric values were handled using median imputation in the
    cleaning workflow.
3.  Duplicate customer records were removed while retaining the first
    occurrence.
4.  The cleaned dataset was saved as `Loan_Credit_Risk_Cleaned.csv`.

## Risk Segmentation

### Credit Score Groups

-   Poor (\<580)
-   Fair (580-669)
-   Good (670-739)
-   Excellent (740+)

### Income Groups

-   Low Income (\<30,000)
-   Medium Income (30,000-59,999)
-   High Income (60,000-99,999)
-   Very High Income (100,000+)

## Descriptive Results

### Default Rate by Loan Type

  Loan Type          Default Rate
  ---------------- --------------
  Business Loan            32.50%
  Personal Loan            12.57%
  Home Loan                10.41%
  Education Loan            9.32%
  Auto Loan                 7.33%

### Default Rate by Employment Status

  Employment Status     Default Rate
  ------------------- --------------
  Unemployed                  42.09%
  Retired                     14.43%
  Self-employed               13.45%
  Salaried                    12.51%
  Business Owner              11.11%

### Default Rate by Credit Score Group

  Credit Score Group     Default Rate
  -------------------- --------------
  Poor (\<580)                 34.26%
  Fair (580-669)               16.16%
  Good (670-739)                7.00%
  Excellent (740+)              3.12%

### Default Rate by Income Group

  Income Group         Default Rate
  ------------------ --------------
  Low Income                 24.91%
  Medium Income              13.51%
  High Income                 9.59%
  Very High Income            5.77%

These results are descriptive for this dataset and should not be
interpreted as causal relationships.

## Power BI Dashboard Pages

1.  **Executive Risk Overview** --- KPI cards, loan default
    distribution, and employment default rates.
2.  **Loan & Regional Analysis** --- loan type and regional loan amount
    analysis and loan-type default rates.
3.  **Customer Credit Risk Analysis** --- credit-score distribution,
    credit-score groups, income groups, and income versus loan amount.
4.  **Loan Details & Risk Explorer** --- detailed loan table and
    interactive slicers.

## Power BI Measures

``` dax
Total Customers =
DISTINCTCOUNT(Loan_Credit_Risk_Cleaned[Customer_ID])
```

``` dax
Total Loans =
DISTINCTCOUNT(Loan_Credit_Risk_Cleaned[Loan_ID])
```

``` dax
Defaulted Loans =
CALCULATE(
    [Total Loans],
    Loan_Credit_Risk_Cleaned[Default_Status] = "Yes"
)
```

``` dax
Non-Defaulted Loans =
CALCULATE(
    [Total Loans],
    Loan_Credit_Risk_Cleaned[Default_Status] = "No"
)
```

``` dax
Default Rate % =
DIVIDE([Defaulted Loans], [Total Loans], 0)
```

``` dax
Average Loan Amount =
AVERAGE(Loan_Credit_Risk_Cleaned[Loan_Amount])
```

``` dax
Average Credit Score =
AVERAGE(Loan_Credit_Risk_Cleaned[Credit_Score])
```

``` dax
Average Annual Income =
AVERAGE(Loan_Credit_Risk_Cleaned[Annual_Income])
```

## Calculated Columns

### Credit Score Group

``` dax
Credit Score Group =
SWITCH(
    TRUE(),
    Loan_Credit_Risk_Cleaned[Credit_Score] < 580, "Poor (<580)",
    Loan_Credit_Risk_Cleaned[Credit_Score] < 670, "Fair (580-669)",
    Loan_Credit_Risk_Cleaned[Credit_Score] < 740, "Good (670-739)",
    "Excellent (740+)"
)
```

### Income Group

``` dax
Income Group =
SWITCH(
    TRUE(),
    Loan_Credit_Risk_Cleaned[Annual_Income] < 30000, "Low Income",
    Loan_Credit_Risk_Cleaned[Annual_Income] < 60000, "Medium Income",
    Loan_Credit_Risk_Cleaned[Annual_Income] < 100000, "High Income",
    "Very High Income"
)
```

## Dashboard Filters

Gender, Education, Employment Status, Loan Type, Region, Default Status,
Income Group, and Credit Score Group.

## Deliverables

-   `Loan_Credit_Risk_Cleaned.csv`
-   `Loan_Credit_Risk_Analysis.py`
-   `Loan_Default_Credit_Risk_Analysis_Report.pdf`
-   `README.md`
-   Power BI four-page dashboard

## Conclusion

The project demonstrates an end-to-end analytics workflow from cleaned
loan data to an interactive Power BI dashboard. The dashboard separates
executive monitoring, loan and regional analysis, customer credit-risk
analysis, and detailed loan exploration.

**Note:** This project is intended for analytical and educational use.
Dataset relationships should not be treated as proof of causation or as
an automated lending decision.
