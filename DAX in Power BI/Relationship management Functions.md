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

### 3. USERELATIONSHIP
- Specifies an existing relationship to be used in the evaluation of a DAX expression. The relationship is defined by naming, as arguments, the two columns that serve as endpoints.
- Syntax - USERELATIONSHIP(ColumnName1, ColumnName2)

## Example -
```dax
DEFINE
    MEASURE Sales[Delivery Amount] =
        CALCULATE (
            [Sales Amount],
            USERELATIONSHIP ( Sales[Delivery Date], 'Date'[Date] )
        )
EVALUATE
SUMMARIZECOLUMNS (
    'Date'[Calendar Year],
    "Sales Amount", [Sales Amount],
    "Delivery Amount", [Delivery Amount]
)
```
