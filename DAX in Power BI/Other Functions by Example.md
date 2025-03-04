# Other Functions
These are special functions that cannot be classified in other categories.

### 1. BLANK()
- Returns a blank.
- Syntax - BLANK()

## Example -
```dax
DEFINE
    MEASURE Customer[EmptyNames] =
        CALCULATE (
            COUNTROWS ( Customer ),
            Customer[Customer Name] == BLANK ()
        )
EVALUATE
SUMMARIZECOLUMNS (
    Customer[Continent],
    "Customers", COUNTROWS ( Customer ),
    "Customers with blank name", [EmptyNames]
)
```

### 2. EARLIER
- Returns the value in the column prior to the specified number of table scans (default is 1).
- Syntax - EARLIER( ColumnName )

## Example -
```dax
EVALUATE
ADDCOLUMNS (
    VALUES ( Customer[Yearly Income] ),
    "Customers", CALCULATE ( COUNTROWS ( Customer ) ),
    "RT Customers",
        COUNTROWS (
            FILTER (
                Customer,
                Customer[Yearly Income] <= EARLIER ( Customer[Yearly Income] )
            )
        )
)
ORDER BY [Yearly Income]

```

### 3. RANK
- Returns the rank for the current context within the specified partition sorted by the specified order or on the axis specified.
- Syntax - RANK ( [<ties>][, <relation> or <axis>][, <orderBy>][, <blanks>][, <partitionBy>][, <matchBy>][, <reset>] )

## Example -
```dax
DEFINE
    MEASURE Sales[Rounded Sales] =
        MROUND ( [Sales Amount], 400000 )
    MEASURE Sales[Rank] =
        VAR SourceTable =
            ADDCOLUMNS ( ALLSELECTED ( Product[Brand] ), "@Amt", [Rounded Sales] )
        VAR Result =
            RANK ( DENSE, SourceTable, ORDERBY ( [@Amt], DESC, Product[Brand], ASC ) )
        RETURN
            Result
 
EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Category],
    'Product'[Brand],
    TREATAS ( { "Audio", "Computers" }, 'Product'[Category] ),
    "Sales Amount", [Sales Amount],
    "Rank", [Rank]
)
ORDER BY
    'Product'[Category],
    [Rank] ASC
```

### 4. ROWNUMBER
- Returns the unique rank for the current context within the specified partition sorted by the specified order or on the axis specified.
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

### 5. CALCULATETABLE
- Evaluates a table expression in a context modified by filters.
- Syntax -
CALCULATETABLE (
    <table_expression>,
    FILTER (
        ALL ( table[column] ),
        table[column] = 10
    )
)

## Example -
```dax
EVALUATE
CALCULATETABLE (
    VALUES ( 'Product'[Color] ),
    'Product'[Brand] = "Proseware"
)
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
