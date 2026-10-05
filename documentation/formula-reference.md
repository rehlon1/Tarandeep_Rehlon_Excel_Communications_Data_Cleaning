# Excel Formula Reference

This file summarises representative formulas used in the pre-processing stage.

## Split Customer ID from combined field

```excel
=TEXTBEFORE(A2,"-",-1)
```

## Extract Gender

```excel
=TEXTAFTER([@Customer_ID_sex],"-",-1)
```

## Standardise binary fields

```excel
=IF(D2=1,"Yes",IF(D2=0,"No",D2))
```

and for Y/N fields:

```excel
=IF(F2="Y","Yes",IF(F2="N","No",F2))
```

## Create tenure bands

```excel
=IF(J2<=12,"0-12 months",
 IF(J2<=24,"13-24 months",
 IF(J2<=48,"25-48 months","49+ months")))
```

## Correct internet service spelling

```excel
=IF([@InternetService]="Fiber opticc","Fiber optic",[@InternetService])
```

## Split Online Security / Online Backup

```excel
=TEXTBEFORE([@[OnlineSecurity/OnlineBackup]],"/")
```

```excel
=TEXTAFTER([@[OnlineSecurity/OnlineBackup]],"/")
```

## Map contract codes

```excel
=XLOOKUP([@Contract],contract_tbl[Type],contract_tbl[Contract],"Not found")
```

## Map payment method codes

```excel
=XLOOKUP([@PaymentMethod],Payment_tbl[Type],Payment_tbl[PaymentMethod],"Unknown")
```

## Clean Total Charges

```excel
=IF(TRIM(AD2&"")="",0,VALUE(TRIM(AD2&"")))
```

## Validation check

A comparison field was also used to test Total Charges against tenure multiplied by monthly charges:

```excel
=[@MonthlyCharges]*[@tenure]-[@[Total charges Pre-Processing]]
```

The relationship was treated as a validation assumption to be raised with the stakeholder rather than as a confirmed business rule.
