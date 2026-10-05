# Data Quality Methodology

## Purpose

Before analysing churn, I reviewed the dataset for consistency, accuracy, validity, structure and uniqueness. The aim was to make the data reliable enough for PivotTables, charts, slicers and dashboard reporting without losing visibility of the original source data.

## Cleaning workflow

### Partner and Dependents

**Issue:** values used a mixture of `Y`, `N`, `Yes` and `No`.

**Action:** standardised the values to `Yes` and `No`.

**Why it matters:** inconsistent categories can be split into separate groups in PivotTables and filters, producing misleading counts and churn rates.

### Customer ID and Gender

**Issue:** Customer ID and Gender were stored together in a single field.

**Action:** split the field into separate Customer ID and Gender columns.

**Why it matters:** customer identifiers should remain separate from attributes used for segmentation and filtering.

### Internet Service

**Issue:** some records contained `Fiber opticc` rather than `Fiber optic`.

**Action:** corrected the spelling so fibre optic customers formed one category.

**Why it matters:** a spelling variation would create a duplicate category and distort churn calculations.

### Online Security and Online Backup

**Issue:** the two services were stored in one combined field.

**Action:** split them into separate Online Security and Online Backup columns.

**Why it matters:** each service can then be tested independently against churn.

### Contract

**Issue:** contracts were represented by numeric codes rather than readable values.

**Action:** used the supplied contract lookup table to convert the codes into `Month-to-month`, `One year` and `Two year`.

### Payment Method

**Issue:** payment methods were coded numerically. The lookup table defined codes 1-4, but some rows contained code 5.

**Action:** mapped valid codes using the supplied lookup table. Code 5 was retained as `Unknown` and identified for stakeholder follow-up.

**Result:** 21 records contained the unsupported payment code.

### Total Charges

**Issue:** Total Charges required validation because some values did not align with tenure multiplied by monthly charge, and some values required numeric cleaning.

**Action:** created check fields and a cleaned Total Charges field. `TRIM` and `VALUE` were used where needed to convert cleaned text values into numbers.

**Important assumption:** the comparison to `tenure × monthly charge` is a validation assumption, not a confirmed billing rule. In a live project this would be checked with the stakeholder.

### Customer ID duplicates

Customer IDs were checked for uniqueness. No duplicate customer IDs were identified.

### Senior Citizen

The field used `0` and `1` codes. These were converted into `Yes` and `No` for reporting clarity.

### Tenure bands

Tenure was grouped into:

- 0-12 months
- 13-24 months
- 25-48 months
- 49+ months

This made it easier to compare churn across customer life stages.

## Excel techniques used

The pre-processing workbook uses:

- `TEXTBEFORE`
- `TEXTAFTER`
- nested `IF`
- `XLOOKUP`
- `TRIM`
- `VALUE`
- Excel Tables and structured references
- validation and check columns
- PivotTables
- slicers
- charts and KPI reporting

## Outcome

The cleaning process produced a clearer, more consistent analysis dataset while keeping the source and transformation stages separate. This improved confidence in the dashboard and recommendations produced later in the project.
