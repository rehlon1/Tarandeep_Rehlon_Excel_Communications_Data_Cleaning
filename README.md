# Excel Customer Churn Analysis

An end-to-end customer churn analysis built in **Microsoft Excel** using a fictional telecommunications scenario for **Horizon Communications**. The project covers data quality, cleaning, exploratory analysis, interactive dashboarding and business recommendations.

The objective was to answer one question:

> **What are the biggest drivers of customer churn, and which customer groups should Horizon prioritise for retention?**

![Excel customer churn dashboard](assets/dashboard.png)

## Project summary

| Metric | Result |
|---|---:|
| Total customers analysed | 7,043 |
| Churned customers | 1,869 |
| Overall churn rate | 26.5% |
| Monthly revenue at risk | £139,131 |
| Highest-risk combined segment | Month-to-month + Fibre optic |
| Churn rate for highest-risk combination | 54.6% |

The analysis found that churn was **concentrated rather than evenly spread**. Contract type, tenure, payment method and access to support services were the clearest retention signals.

## Tools and techniques

**Microsoft Excel** was used throughout the project, including:

- Excel Tables and structured references
- `TEXTBEFORE` and `TEXTAFTER` to split combined fields
- Nested `IF` statements for standardisation and tenure banding
- `XLOOKUP` to translate coded contract and payment values
- `TRIM` and `VALUE` to clean and convert numeric fields
- Data-quality and duplicate checks
- PivotTables and charts for exploratory analysis
- Slicers for interactive filtering
- KPI cards and an interactive dashboard
- Business-focused recommendations based on the analysis

## Data preparation and quality checks

The source data contained a number of quality issues that could have distorted the churn analysis. I created a separate pre-processing stage rather than editing the original data directly.

Key cleaning steps included:

| Issue | Action |
|---|---|
| Customer ID and gender stored in one field | Split into separate Customer ID and Gender columns |
| `Y`, `N`, `Yes` and `No` used inconsistently | Standardised to `Yes` / `No` |
| `Fiber opticc` spelling error | Corrected to `Fiber optic` |
| Online Security and Online Backup stored together | Split into separate service fields |
| Contract stored as numeric codes | Mapped to readable labels using a lookup table |
| Payment Method stored as numeric codes | Mapped valid values; code `5` flagged as `Unknown` |
| Blank / inconsistent Total Charges values | Created validation and cleaned charge fields |
| Customer IDs | Checked for duplicates; none were found |
| Tenure stored only as months | Created 0-12, 13-24, 25-48 and 49+ month bands |

The invalid payment code was not silently corrected. **21 records** were retained as `Unknown`, making the limitation visible in the analysis.

For more detail, see [Data Quality Methodology](documentation/data-quality-methodology.md).

## Workbook structure

The Excel workbook keeps the workflow separated into clear stages:

```text
Main_Data_Original
Main_Data_Pre-Processing
Main_Data_Clean
Documentation
payment_method
contract
EDA
Dashboard
```

This makes the analysis easier to audit: the original data is preserved, transformations are visible, cleaned data is separated from the source, and reporting is kept apart from preparation.

## Key findings

### 1. Contract and tenure are major churn drivers

- **Month-to-month customers:** 42.7% churn
- **Customers in their first 12 months:** 47.4% churn
- Churn falls sharply as tenure increases
- Two-year customers show substantially lower churn than month-to-month customers

![Contract and tenure analysis](assets/contract-and-tenure.png)

**Action:** create an early-life retention journey and encourage suitable month-to-month customers to move to longer contracts.

### 2. Payment method highlights a retention opportunity

Customers paying by **electronic check** had a **45.3% churn rate**, compared with approximately **15-17%** for automatic payment methods.

**Action:** make automatic payment easier to adopt through onboarding prompts, support and appropriate incentives.

### 3. Support and service add-ons are linked to churn

Customers without Tech Support, Online Security or Online Backup had churn rates around 40%. Fibre optic customers also showed elevated churn at **41.9%**.

**Action:** test bundles that combine fibre optic service with support, security and backup rather than treating these services only as optional extras.

### 4. Multiple risk factors matter

The highest-priority combination identified was:

**Month-to-month + Fibre optic → 54.6% churn**

Other elevated signals included:

- Senior citizens: 41.7%
- No partner: 33.0%
- No dependents: 31.3%
- Gender showed little meaningful difference

![High-risk customer segments](assets/high-risk-segments.png)

The analysis therefore supports **targeted retention activity based on combinations of risk factors**, rather than one broad campaign for all customers.

## Recommendations

1. **Contract conversion** — use appropriate loyalty incentives to move high-risk month-to-month customers onto longer contracts.
2. **Early-life retention** — introduce proactive contact and welcome checks during the first 12 months.
3. **Payment migration** — encourage electronic check customers to move to automatic payment methods.
4. **Service bundling** — test fibre optic packages bundled with support, security and backup.
5. **Targeted campaigns** — prioritise customers with multiple churn risk factors first.

A fuller breakdown is available in [Insights and Recommendations](documentation/insights-and-recommendations.md).

## Assumptions and limitations

One validation check compared **Total Charges** with `tenure × monthly charge`. This was treated as an analytical assumption to be raised with the stakeholder rather than an unquestioned business rule, because real billing totals may contain adjustments that are not visible in the dataset.

Payment method code `5` was also absent from the supplied lookup table. Those records were labelled `Unknown` rather than assigned to an unsupported category.

These decisions were documented so that the analysis remains transparent and repeatable.

## Project files

- [Excel workbook](workbook/customer-churn-analysis.xlsx)
- [Data quality and cleaning report - PDF](documentation/data-quality-cleaning-report.pdf)
- [Data quality and cleaning report - Word](documentation/data-quality-cleaning-report.docx)
- [Customer churn presentation - PDF](presentation/customer-churn-analysis-presentation.pdf)

## What this project demonstrates

This project demonstrates my ability to take a raw dataset through the complete analysis process: **understand the business question, identify data-quality problems, clean and validate the data, explore patterns, build an accessible dashboard and translate findings into practical recommendations.**

---

**Tarandeep Rehlon**  
Data Analyst / Trainee Data Consultant portfolio project
