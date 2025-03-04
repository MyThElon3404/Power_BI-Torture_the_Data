# Relationship management Functions
These functions manage and manipulate relationships between tables.

### 1. RELATED
- Returns a related value from another table.
- Syntax - RELATED( ColumnName )
- NOTE - The RELATED function requires that a regular relationship exists between the current table and the table with related information. The argument specifies a column reference, and the function follows a chain of one or more many-to-one relationships to fetch the value from the specified column in the related table. If a relationship does not exist, RELATED raises an error. 

## Example -
```dax
DEFINE
    MEASURE Sales[Sales Amount] =
        SUMX ( Sales, Sales[Quantity] * Sales[Net Price] )
    MEASURE Sales[Sales at List Price] =
        SUMX ( Sales, Sales[Quantity] * RELATED ( 'Product'[List Price] ) )

EVALUATE
SUMMARIZECOLUMNS (
    'Date'[Calendar Year],
    "Sales Amount", [Sales Amount],
    "Sales at List Price", [Sales at List Price]
)
```

### 2. RELATEDTABLE
- Returns the related tables filtered so that it only includes the related rows.
- Syntax - RELATEDTABLE( Table )
- NOTE - The RELATEDTABLE function performs a context transition from row context(s) to a filter context, and evaluates the expression in the resulting filter context.
This function is a shortcut for CALCULATETABLE function with no additional filters, accepting only a table reference and not a table expression.

## Example -
```dax
DEFINE
    MEASURE Sales[Sales Amount] =
        SUMX ( Sales, Sales[Quantity] * Sales[Net Price] )
    MEASURE Sales[TX/Customer w/rel] =
        AVERAGEX ( Customer, COUNTROWS ( RELATEDTABLE ( Sales ) ) )
    MEASURE Sales[TX/Customer w/calc] =
        AVERAGEX ( Customer, COUNTROWS ( CALCULATETABLE ( Sales ) ) )
 
EVALUATE
SUMMARIZECOLUMNS (
    'Date'[Calendar Year],
    "Sales Amount", [Sales Amount],
    "TX/Customer w/rel", [TX/Customer w/rel],
    "TX/Customer w/calc", [TX/Customer w/calc]
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
