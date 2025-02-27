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

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
