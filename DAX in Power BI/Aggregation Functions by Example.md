- # Aggregation Functions -
Aggregation functions return a scalar value by applying an aggregation function to a column or to an expression evaluated by iterating a table expression.
    
### 1. AVERAGE 
- Returns the average (arithmetic mean) of all the numbers in a column.
- Syntax - AVERAGE ( table[column] )

### 2. AVERAGEX 
- Calculates the average (arithmetic mean) of a set of expressions evaluated over a table.
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

### 3. COUNT 
- Counts the number of rows in the table where the specified column has a non-blank value.
- Syntax - COUNT ( table[column] )

### 4. COUNTX 
- Counts the number of values which result from evaluating an expression for each row of a table.
- Syntax -
COUNTX (
    table,
    table[column]
)

### 5. COUNTROWS 
- Counts the number of rows in a table.
- Syntax - COUNTROWS ( table )
- COUNTROWS ( DISTINCT ( table ) )
- COUNTROWS ( VALUES ( table ) )

### 6. COUNTBLANK 
- Counts the number of blanks in a column.
- Syntax - COUNTBLANK ( 'Table'[Column] )

### 7. DISTINCTCOUNT 
- Counts the number of distinct values in a column.
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
    MEASURE Customer[# Countries 1] = COUNTROWS ( DISTINCT ( Customer[CountryRegion] ) )

EVALUATE
SUMMARIZECOLUMNS (
    Customer[Continent],
    "Total Customers", [customers],
    "CustName Count", [using count],
    "CustName CountX", [using countx],
    "CustName calculate isblank", [using calculate isblank],
    "Distinct Customer", [distinct cust],
    "# Countries 1", [# Countries 1]
)
```

### 8. MAX 
- Returns the largest value in a column, or the larger value between two scalar expressions. Ignores logical values. Strings are compared according to alphabetical order.
- Syntax - MAX ( table[column] )

### 9. MAXX 
- Returns the largest value that results from evaluating an expression for each row of a table. Strings are compared according to alphabetical order.
- Syntax - MAXX (
    table,
    table[column]
)

### 10. MIN 
- Returns the smallest value in a column, or the smaller value between two scalar expressions. Ignores logical values. Strings are compared according to alphabetical order.
- Syntax - MIN ( table[column] )

### 11. MINX 
- Returns the smallest value that results from evaluating an expression for each row of a table. Strings are compared according to alphabetical order.
- Syntax - MINX (
    table,
    table[column]
)

### 12. PRODUCT 
- Returns the product of given column reference.
- Syntax - PRODUCT ( table[column] )

### 13. PRODUCTX 
- Returns the product of an expression values in a table.
- Syntax - PRODUCTX (
    table,
    table[column]
)

- ## Example -
```dax
DEFINE
    MEASURE Sales[MAX_Price] = MAX ( Sales[Net Price] )
    MEASURE Sales[MAXX_Price] = MAXX ( Sales, Sales[Net Price] )
    MEASURE Sales[MIN_Price] = MIN ( Sales[Net Price] )
    MEASURE Sales[MINX_Price] = MINX ( Sales, Sales[Net Price] )
    MEASURE Sales[PRODUCT_Price] = CALCULATE ( PRODUCT ( Sales[Net Price] ), Sales[Quantity] < 3 )
    MEASURE Sales[PRODUCTX_Price] = CALCULATE ( PRODUCTX ( Sales, Sales[Net Price] ), Sales[Quantity] < 3 )
    MEASURE Sales[SUM_Price] = SUM ( Sales[Net Price] )
    MEASURE Sales[SUMX_Price] = SUMX ( Sales, Sales[Net Price] )

EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Color],
    "Max_Price", [MAX_Price],
    "MaxX_Price", [MAXX_Price],
    "Min_Price", [MIN_Price],
    "MinX_Price", [MINX_Price],
    "Product_Price", [PRODUCT_Price],
    "ProductX_Price", [PRODUCTX_Price],
    "Sum_Price", [SUM_Price],
    "SumX_Price", [SUMX_Price]
)

```
