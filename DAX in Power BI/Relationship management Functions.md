# Filter Functions
Filter functions manipulate table and filter contexts.

### 1. ALL
- Returns all the rows in a table, or all the values in a column, ignoring any filters that might have been applied.
- Syntax - ALL ( Customer )
ALL ( Customer[Country], Customer[State] , Customer[City] )

## Example -
```dax
DEFINE
    MEASURE Sales[color Sales Amount] =
        CALCULATE ( SUMX ( Sales, [Sales Amount] ), ALL ( 'Product'[Color] ) )
    MEASURE Sales[Red Sales Amount] =
        CALCULATE (
            SUMX ( Sales, [Sales Amount] ),
            FILTER ( ALL ( 'Product'[Color] ), 'Product'[Color] = "Red" )
        )
    MEASURE Sales[ONLY Red Sales Amount] =
        IF (
            SELECTEDVALUE ( 'Product'[Color] ) = "Red",
            CALCULATE (
                SUMX ( Sales, [Sales Amount] ),
                FILTER ( ALL ( 'Product'[Color] ), 'Product'[Color] = "Red" )
            ),
            0
        )
EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Color],
    "Color Sales Amount", [color Sales Amount],
    "Sales Amount", [Sales Amount],
    "Red Sales Amount", [Red Sales Amount],
    "ONLY Red Sales Amount", [ONLY Red Sales Amount]
)
```

### 2. ALLEXCEPT
- Returns all the rows in a table except for those rows that are affected by the specified column filters.
- Syntax - ALLEXCEPT(TableName, ColumnName1, ColumnName2)

## Example -
```dax
DEFINE
    MEASURE Sales[Color_Wise] =
        CALCULATE (
            SUMX ( Sales, [Sales Amount] ),
            ALLEXCEPT ( 'Product', 'Product'[Color] )
        )
    MEASURE Sales[PC_Wise] =
        CALCULATE (
            SUMX ( Sales, [Sales Amount] ),
            ALLEXCEPT ( 'Product', 'Product'[Category] )
        )
EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Category],
    'Product'[Color],
    "Sales Amount", [Sales Amount],
    "Color_Wise", [Color_Wise],
    "PC_Wise", [PC_Wise]
)

```

### 3. ALLSELECTED
- Returns all the rows in a table, or all the values in a column, ignoring any filters that might have been applied inside the query, but keeping filters that come from outside.
- Syntax - ALLSELECTED(Table_or_ColumnsName, ColumnName)

## Example -
```dax
EVALUATE
CALCULATETABLE (
    ADDCOLUMNS (
        ALL ( 'Product'[Category] ),
        "Sales Amount", [Sales Amount],
        "Sales Sel",
            CALCULATE (
                [Sales Amount],
                ALLSELECTED ( Product[Category] )
            )
    ),
    Product[Category] IN { "Audio", "Computer" }
)
```

### 4. CALCULATE
- Evaluates an expression in a context modified by filters.
- Syntax - CALCULATE(Expression, Filters)

- ## Example -
```dax
DEFINE
    MEASURE Sales[Red Blue Sales Keepfilters] =
        CALCULATE (
            [Sales Amount],
            KEEPFILTERS ( 'Product'[Color] IN { "Red", "Blue" } )
        )
    MEASURE Sales[Red Blue Sales] =
        CALCULATE (
            [Sales Amount],
            'Product'[Color] IN { "Red", "Blue" }
        )
EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Color],
    "Sales Amount", [Sales Amount],
    "Red Blue Sales", [Red Blue Sales],
    "Red Blue Sales Keepfilters", [Red Blue Sales Keepfilters]
)
```
