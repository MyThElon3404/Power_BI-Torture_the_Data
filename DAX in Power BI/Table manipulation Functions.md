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

### 6. FILTER
- Returns a table that has been filtered.
- Syntax - 
FILTER (
    Table,
    Filter Expression
)

## Example -
```dax
DEFINE
    MEASURE Sales[Red Sales] =
        SUMX (
            FILTER ( Sales, RELATED ( Product[Color] ) = "Red" ),
            Sales[Quantity] * Sales[Net Price]
        )
    MEASURE Sales[Red Sales CALCULATE] =
        CALCULATE ( [Sales Amount], KEEPFILTERS ( Product[Color] = "Red" ) )

EVALUATE
SUMMARIZECOLUMNS (
    Product[Brand],
    "Sales", [Sales Amount],
    "Red Sales", [Red Sales],
    "Red Sales CALCULATE", [Red Sales CALCULATE]
)
```

### 7. KEEPFILTERS
- Changes the CALCULATE and CALCULATETABLE function filtering semantics.
- Syntax - KEEPFILTERS ( Filter Expression )
  
## Example -
```dax
DEFINE
    MEASURE Sales[White Sales] =
        CALCULATE ( [Sales Amount], Product[Color] = "White" )
    MEASURE Sales[White Sales Keep] =
        CALCULATE ( [Sales Amount], KEEPFILTERS ( Product[Color] = "White" ) )

EVALUATE
ADDCOLUMNS (
    VALUES ( 'Product'[Color] ),
    "Sales Amount", [Sales Amount],
    "White Sales", [White Sales],
    "White Sales Keep", [White Sales Keep]
)
ORDER BY [Sales Amount] DESC
```
