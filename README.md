# Excel Customer Churn Analysis

An end-to-end customer churn analysis built in **Microsoft Excel** using a fictional telecommunications scenario for **Horizon Communications**. The project covers data quality, cleaning, exploratory analysis, interactive dashboarding and business recommendations.

The objective was to answer:

> **What are the biggest drivers of customer churn, and which customer groups should Horizon prioritise for retention?**

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
- `TEXTBEFORE` and `TEXTAFTER`
- Nested `IF` statements
- `XLOOKUP`
- `TRIM` and `VALUE`
- Data-quality and duplicate checks
- PivotTables and charts
- Slicers for interactive filtering
- KPI cards and an interactive dashboard
- Business-focused recommendations

For examples of the formula logic, see [Formula Reference](documentation/formula-reference.md).

## Data preparation and quality checks

The source data contained several issues that could have distorted the analysis, so I created a separate pre-processing stage rather than editing the original source directly.

| Issue | Action |
|---|---|
| Customer ID and gender stored together | Split into separate Customer ID and Gender columns |
| `Y`, `N`, `Yes` and `No` used inconsistently | Standardised to `Yes` / `No` |
| `Fiber opticc` spelling error | Corrected to `Fiber optic` |
| Online Security and Online Backup stored together | Split into separate service fields |
| Contract stored as numeric codes | Mapped to readable labels using a lookup table |
| Payment Method stored as numeric codes | Mapped valid values; code `5` flagged as `Unknown` |
| Blank / inconsistent Total Charges values | Created validation and cleaned charge fields |
| Customer IDs | Checked for duplicates; none were found |
| Tenure stored only as months | Created 0-12, 13-24, 25-48 and 49+ month bands |

The invalid payment code was not silently corrected. **21 records** were retained as `Unknown`, keeping the limitation visible.

See [Data Quality Methodology](documentation/data-quality-methodology.md) for the full cleaning approach.

## Workbook structure

The original workbook was organised into clear stages:

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

This separation preserves the source data, makes transformations traceable and keeps reporting separate from preparation. A sheet-by-sheet guide is available in [Workbook Guide](workbook/README.md).

## Key findings

### 1. Contract and tenure are major churn drivers

- **Month-to-month customers:** 42.7% churn
- **Customers in their first 12 months:** 47.4% churn
- Churn falls sharply as tenure increases
- Two-year customers show substantially lower churn than month-to-month customers

**Recommendation:** create an early-life retention journey and encourage suitable month-to-month customers to move to longer contracts.

### 2. Payment method highlights a retention opportunity

Customers paying by **electronic check** had a **45.3% churn rate**, compared with approximately **15-17%** for automatic payment methods.

**Recommendation:** make automatic payment easier to adopt through onboarding prompts, support and appropriate incentives.

### 3. Support and service add-ons are linked to churn

Customers without Tech Support, Online Security or Online Backup had churn rates around 40%. Fibre optic customers also showed elevated churn at **41.9%**.

**Recommendation:** test bundles that combine fibre optic service with support, security and backup.

### 4. Multiple risk factors matter

The highest-priority combination identified was:

**Month-to-month + Fibre optic → 54.6% churn**

Other elevated signals included:

- Senior citizens: 41.7%
- No partner: 33.0%
- No dependents: 31.3%
- Gender showed little meaningful difference

This supports **targeted retention activity based on combinations of risk factors**, rather than one broad campaign.

## Recommendations

1. **Contract conversion** — use appropriate loyalty incentives to move high-risk month-to-month customers onto longer contracts.
2. **Early-life retention** — introduce proactive contact and welcome checks during the first 12 months.
3. **Payment migration** — encourage electronic check customers to move to automatic payment methods.
4. **Service bundling** — test fibre optic packages bundled with support, security and backup.
5. **Targeted campaigns** — prioritise customers with multiple churn risk factors first.

See [Insights and Recommendations](documentation/insights-and-recommendations.md) for the detailed findings.

## Assumptions and limitations

One validation check compared **Total Charges** with `tenure × monthly charge`. This was treated as an analytical assumption to be raised with the stakeholder rather than an unquestioned business rule, because real billing totals may contain adjustments not represented in the dataset.

Payment method code `5` was absent from the supplied lookup table. Those records were labelled `Unknown` rather than assigned to an unsupported category.

## Repository contents

- [Data Quality Methodology](documentation/data-quality-methodology.md)
- [Insights and Recommendations](documentation/insights-and-recommendations.md)
- [Formula Reference](documentation/formula-reference.md)
- [Workbook Guide](workbook/README.md)

The full training workbook and presentation are retained separately rather than publishing the complete source dataset in this public repository.

## What this project demonstrates

This project demonstrates my ability to take a raw dataset through the complete analysis process: **understand the business question, identify data-quality problems, clean and validate the data, explore patterns, build an interactive dashboard and translate findings into practical recommendations.**

---

**Tarandeep Rehlon**  
Data Analyst / Trainee Data Consultant portfolio project
