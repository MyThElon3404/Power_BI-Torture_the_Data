- # Aggregation Functions -
Aggregation functions return a scalar value by applying an aggregation function to a column or to an expression evaluated by iterating a table expression.

### 1. AVERAGE - Returns the average (arithmetic mean) of all the numbers in a column.
- Syntax - AVERAGE ( table[column] )

### 2. AVERAGEX - Calculates the average (arithmetic mean) of a set of expressions evaluated over a table.
- Syntax -
AVERAGEX (
    table,
    table[column]
)
- ## Example -
```dax
DEFINE
    MEASURE Sales[AVG Quantity1] = AVERAGE ( Sales[Quantity] )
    MEASURE Sales[AVG Quantity2] = AVERAGEX ( Sales, Sales[Quantity] )
    MEASURE Sales[AVG Sales Amount] = AVERAGEX ( Sales, Sales[Quantity] * Sales[Net Price] )

EVALUATE
SUMMARIZECOLUMNS (
    'Date'[Calendar Year Number],
    "AVG Quantity1", [AVG Quantity1],
    "AVG Quantity2", [AVG Quantity2],
    "AVG Sales Amount", [AVG Sales Amount],
    "Sales Amount", [Sales Amount]
)
ORDER BY 'Date'[Calendar Year Number] ASC
```

### 3. COUNT - Counts the number of rows in the table where the specified column has a non-blank value.
- Syntax - COUNT ( table[column] )

### 4. COUNTX - Counts the number of values which result from evaluating an expression for each row of a table.
- Syntax -
COUNTX (
    table,
    table[column]
)

### 5. COUNTROWS - Counts the number of rows in a table.
- Syntax - COUNTROWS ( table )
- COUNTROWS ( DISTINCT ( table ) )
- COUNTROWS ( VALUES ( table ) )

### 6. COUNTBLANK - Counts the number of blanks in a column.
- Syntax - COUNTBLANK ( 'Table'[Column] )

### 7. DISTINCTCOUNT - Counts the number of distinct values in a column.
- Syntax - DISTINCTCOUNT ( table[column] )
- COUNTROWS ( DISTINCT ( table[column] ) )

- ## Example -
```dax
DEFINE
    MEASURE Customer[customers] = COUNTROWS ( Customer )
    MEASURE Customer[using count] = COUNT ( Customer[Name] )
    MEASURE Customer[using countx] = COUNTX ( Customer, Customer[Name] )
    MEASURE Customer[using calculate isblank] = CALCULATE ( COUNTROWS ( Customer ), NOT ISBLANK ( Customer[Name] ) )
    MEASURE Customer[distinct cust] = DISTINCTCOUNT ( Customer[Name] )

EVALUATE
SUMMARIZECOLUMNS (
    Customer[Continent],
    "Total Customers", [customers],
    "CustName Count", [using count],
    "CustName CountX", [using countx],
    "CustName calculate isblank", [using calculate isblank],
    "Distinct Customer", [distinct cust]
)
```

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
