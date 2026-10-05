# Workbook Guide

The Excel workbook was organised to preserve the original data and make the transformation process auditable.

| Sheet | Purpose |
|---|---|
| `Main_Data_Original` | Original source data retained for reference |
| `Main_Data_Pre-Processing` | Formula-driven cleaning and transformation stage |
| `Main_Data_Clean` | Cleaned dataset used for analysis |
| `Documentation` | In-workbook notes and supporting documentation |
| `payment_method` | Lookup table for payment method codes |
| `contract` | Lookup table for contract codes |
| `EDA` | Exploratory analysis and PivotTable outputs |
| `Dashboard` | Interactive KPI and visualisation layer |

## Examples of transformation logic

```excel
=TEXTBEFORE(A2,"-",-1)
=TEXTAFTER([@Customer_ID_sex],"-",-1)
=IF(D2=1,"Yes",IF(D2=0,"No",D2))
=IF(J2<=12,"0-12 months",IF(J2<=24,"13-24 months",IF(J2<=48,"25-48 months","49+ months")))
=XLOOKUP([@Contract],contract_tbl[Type],contract_tbl[Contract],"Not found")
=XLOOKUP([@PaymentMethod],Payment_tbl[Type],Payment_tbl[PaymentMethod],"Unknown")
=IF(TRIM(AD2&"")="",0,VALUE(TRIM(AD2&"")))
```

The workbook then uses PivotTables, charts and slicers to explore churn by customer profile, contract, tenure, service and payment method.

## Portfolio note

The full training workbook is retained separately. This public repository focuses on the analytical method, technical techniques, key findings and business recommendations rather than publishing the complete source dataset.
