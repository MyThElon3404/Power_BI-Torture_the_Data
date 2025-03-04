# Table manipulation Functions
These functions manipulate and return tables.

### 1. ADDCOLUMNS
- Returns a table with new columns specified by the DAX expressions.
- Syntax - ADDCOLUMNS(Table, Name, Expression)

## Example -
```dax
EVALUATE
FILTER (
    ADDCOLUMNS (
        VALUES ( 'Date'[Calendar Year Number] ),
        "Sales Amount", [Sales Amount],
        "Total Quantity wrong", SUMX ( Sales, Sales[Quantity] ),
        "TQ using calculate", CALCULATE ( SUM ( Sales[Quantity] ) )
    ),
    [Sales Amount] > 0
)
```

### 2. DISTINCT
- Returns a one column table that contains the distinct (unique) values in a column, for a column argument. Or multiple columns with distinct (unique) combination of values, for a table expression argument.
- Syntax - DISTINCT(ColumnExpression OR TableExpression)

## Example -
```dax
EVALUATE
SUMMARIZECOLUMNS (
    Store[Continent],
    "Store with no blank value", COUNTROWS ( DISTINCT ( Store[Store Name] ) ),
    "Store with blank value", COUNTROWS ( VALUES ( Store[Store Name] ) ),
    "#Stores", COUNTROWS ( Store ),
    "#Stores (no blank row)", COUNTROWS ( DISTINCT ( Store ) ),
    "#Stores (blank row)", COUNTROWS ( VALUES ( Store ) )
)
```

### 3. EXCEPT
- Returns the rows of left-side table which do not appear in right-side table.
- Syntax - EXCEPT(LeftTable, RightTable)

## Example -
```dax
EVALUATE
VAR Days = VALUES ( 'Date'[Day of Week] )
VAR WeekEndDays = { "Saturday", "Sunday" }
VAR WorkingDays = EXCEPT ( Days, WeekEndDays )
RETURN
    ADDCOLUMNS ( 
        WorkingDays, 
        "Store Sales", [Sales Amount] 
    )
```

### 4. FILTERS
- Returns a table of the filter values applied directly to the specified column.
- Syntax - FILTERS(ColumnName)

- ## Example -
```dax
EVALUATE
CALCULATETABLE (
    FILTERS ('Product'[Category]),
    'Product'[Color] = "Red"
)
```

### 5. GROUPBY
- Creates a summary the input table grouped by the specified columns.
- Syntax - GROUPBY(Table, GroupBY_ColumnName, Name, Expression)

## Example -
```dax
DEFINE
    VAR AverageCustomerSales = AVERAGEX ( Customer, [Sales Amount] )
    VAR TaggedCustomers =
        SUMMARIZECOLUMNS (
            Customer[CustomerKey],
            "Customer Category", 
                IF ( [Sales Amount] > AverageCustomerSales, "Above Average", "Below Average" )
        )
    VAR Result =
        GROUPBY (
            TaggedCustomers,
            [Customer Category],
            "Customer Count", COUNTX ( CURRENTGROUP (), 1 )
        )

EVALUATE
Result
```

### 6. INTERSECT
- Returns the rows of left-side table which appear in right-side table.
- Syntax - INTERSECT(LeftTable, RightTable)

## Example -
```dax
DEFINE
    VAR Days = VALUES ( 'Date'[Day of Week] )
    VAR WeekendDays = { "Saturday", "Sunday" }
    VAR DaysWeekends = INTERSECT ( Days, WeekendDays )
    VAR WeekendsDays = INTERSECT ( WeekendDays, Days )

EVALUATE
ADDCOLUMNS ( DaysWeekends, "Sales Amount", [Sales Amount] )

EVALUATE
ADDCOLUMNS ( WeekendsDays, "Sales Amount", [Sales Amount] )
```

### 7. SELECTEDCOLUMNS
- Returns a table with selected columns from the table and new columns specified by the DAX expressions.
- Syntax - SELECTEDCOLUMNS(Table, Name, Expression)
  
## Example -
```dax
EVALUATE
CALCULATETABLE (
    SELECTCOLUMNS (
        Sales,
        RELATED ( 'Date'[Date] ),
        Sales[Order Number],
        Sales[Order Line Number],
        "Customer", RELATED ( Customer[Name] ),
        RELATED ( 'Product'[Product Name] ),
        Sales[Quantity],
        "Line Amount", Sales[Quantity] * Sales[Unit Price]
    ),
    'Date'[Date] = DATE ( 2007, 9, 19 ),
    Customer[Customer Type] = "Person"
)
```

### 1. SUMMARIZE
- Creates a summary of the input table grouped by the specified columns.
- Syntax - SUMMARIZE(Table, GroupBY_ColumnName, Name, Expression)

## Example -
```dax
EVALUATE
CALCULATETABLE (
    SUMMARIZE (
        Sales,
        ROLLUP ( 'Product'[Brand], 'Date'[Calendar Year Number] ),
        "Amount", [Sales Amount]
    ),
    'Product'[Brand] IN { "Contoso", "Litware" },
    'Date'[Calendar Year Number] IN { 2008, 2009 }
)
```

### 2. SUMMARIZECOLUMNS
- Create a summary table for the requested totals over set of groups.
- Syntax - SUMMARIZECOLUMNS(GroupBY_ColumnName, FilterTable, Name, Expression)

## Example -
```dax
EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Brand],
    'Date'[Calendar Year],
    TREATAS ( { "CY 2008", "CY 2009" }, 'Date'[Calendar Year] ),
    TREATAS ( { "Blue", "Red" }, 'Product'[Color] ),
    "Amount", [Sales Amount],
    "Quantity", CALCULATE ( SUMX ( Sales, Sales[Quantity] ) )
)
```

### 3. TOPN
- Returns a given number of top rows according to a specified expression.
- Syntax - TOPN(N_Value, Table, OrderBY_Expression, Order(ASC, DESC))

## Example -
```dax
EVALUATE
TOPN (
    3,
    ADDCOLUMNS (
        VALUES ( 'Product'[Product Name] ),
        "@Sales Amount", MROUND ( [Sales Amount], 500000 )
    ),
    [@Sales Amount], DESC
)
ORDER BY [@Sales Amount] DESC
```

### 4. TREATS
- Treats the columns of the input table as columns from other tables. For each column, filters out any values that are not present in its respective output column.
- Syntax - TREATS(Expression, ColumnName)

- ## Example -
```dax
DEFINE
    MEASURE Sales[Sales Trendy Colors] =
        CALCULATE ( [Sales Amount], 'Product'[Color] IN { "Red", "White", "Blue" } )
    MEASURE Sales[Sales Trendy Colors 2] =
        CALCULATE (
            [Sales Amount],
            TREATAS ( { "Red", "White", "Blue" }, 'Product'[Color] )
        )

EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Brand],
    "Sales Trendy Colors", [Sales Trendy Colors],
    "Sales Trendy Colors 2", [Sales Trendy Colors 2]
)
```

### 5. UNION
- Returns the union of the tables whose columns match.
- Syntax - UNION(Table, Table1, Table2)

## Example -
```dax
EVALUATE
VAR Days = VALUES ( 'Date'[Day of Week] )
VAR WeekendDays = { "Saturday", "Sunday" }
VAR UnionDays = UNION ( Days, WeekendDays )
RETURN
    UnionDays
```

### 6. VALUES
- When a column name is given, returns a single-column table of unique values. When a table name is given, returns a table with the same columns and all the rows of the table (including duplicates) with the additional blank row caused by an invalid relationship if present.
- NOTE - VALUES is similar to DISTINCT, but it can have an additional blank row 
- Syntax - VALUES(TableName OR ColumnName)

## Example -
```dax
EVALUATE
SUMMARIZECOLUMNS (
    Store[Continent],
    "Store with no blank value", COUNTROWS ( DISTINCT ( Store[Store Name] ) ),
    "Store with blank value", COUNTROWS ( VALUES ( Store[Store Name] ) ),
    "#Stores", COUNTROWS ( Store ),
    "#Stores (no blank row)", COUNTROWS ( DISTINCT ( Store ) ),
    "#Stores (blank row)", COUNTROWS ( VALUES ( Store ) )
)
```

### 7. SELECTEDCOLUMNS
- Returns a table with selected columns from the table and new columns specified by the DAX expressions.
- Syntax - SELECTEDCOLUMNS(Table, Name, Expression)
  
## Example -
```dax
EVALUATE
CALCULATETABLE (
    SELECTCOLUMNS (
        Sales,
        RELATED ( 'Date'[Date] ),
        Sales[Order Number],
        Sales[Order Line Number],
        "Customer", RELATED ( Customer[Name] ),
        RELATED ( 'Product'[Product Name] ),
        Sales[Quantity],
        "Line Amount", Sales[Quantity] * Sales[Unit Price]
    ),
    'Date'[Date] = DATE ( 2007, 9, 19 ),
    Customer[Customer Type] = "Person"
)
```

