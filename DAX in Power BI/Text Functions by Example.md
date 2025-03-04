# Text Functions
Text functions manipulate strings.

### 1. COMBINEVALUES
- Combines the given set of operands using a specified delimiter.
- Syntax - COMBINEVALUES(Delimiter, Expression1, Expression2)

## Example -
```dax
EVALUATE
ADDCOLUMNS (
    SUMMARIZE (
        TOPN ( 5, Customer ),
        Customer[Customer Code],
        Customer[Customer Name],
        Customer[CountryRegion]
    ),
    "Name, Code, and Country combined",
        COMBINEVALUES (
            " | ",
            Customer[Customer Name],
            Customer[Customer Code],
            Customer[CountryRegion]
        )
)
```

### 2. CONCATENATE
- Joins two text strings into one text string.
- Syntax - CONCATENATE(Table, Expression, Delimiter, OrderBY_Expression, order(ASC, DESC))

## Example -
```dax
EVALUATE
ADDCOLUMNS (
    SUMMARIZE (
        TOPN ( 5, Customer ),
        Customer[Customer Code],
        Customer[Customer Name]
    ),
    "Name and Code 1", CONCATENATE ( Customer[Customer Name], Customer[Customer Code] ),
    "Name and Code 2", Customer[Customer Name] & Customer[Customer Code]
)
```

### 3. CONCATENATEX
- Evaluates expression for each row on the table, then return the concatenation of those values in a single string result, seperated by the specified delimiter.
- Syntax - CONCATENATEX(Table_or_ColumnsName, ColumnName)

## Example -
```dax
EVALUATE
ADDCOLUMNS (
    VALUES ( 'Product'[Category] ),
    "Category colors",
        CONCATENATEX (
            CALCULATETABLE ( VALUES ( 'Product'[Color] ) ),
            Product[Color],
            ", ",             -- Separator (optional)
            Product[Color],   -- Sorting expression (optional)
            ASC               -- Sorting direction (optional)
        )
)
```

### 4. FIND
- Returns the starting position of one text string within another text string. FIND is case-sensitive and accent-sensitive.
- Syntax - FIND(FindText, WithinText, StartPosition, NotFindValue)

- ## Example -
```dax
EVALUATE
CALCULATETABLE (
    ADDCOLUMNS (
        TOPN ( 5, VALUES ( 'Product'[Product Name] ) ),
        "Position of Red", FIND ( "Red", 'Product'[Product Name], 1, BLANK () )
    ),
    'Product'[Color] IN { "Red", "Blue" }
)
```

### 5. FORMAT
- Converts a value to text in the specified number format.
- Syntax - FORMAT(Value, Format)

## Example -
```dax
EVALUATE
{
    ( "Percent",      FORMAT (                0.742, "Percent" )        ),
    ( "Currency (1)", FORMAT (             1234.567, "$#,0.00" )        ),
    ( "Currency (2)", FORMAT (             1234.567, """US$"" #,0.00" ) ),
    ( "Date (1)",     FORMAT ( DATE ( 2019, 3, 28 ), "yyyy-mm-dd" )     ),
    ( "Date (2)",     FORMAT ( DATE ( 2019, 3, 28 ), "m/d/yy" )         ),
    ( "Date (Q)",     FORMAT ( DATE ( 2019, 3, 28 ), "\QQ yyyy" )       )
}
```

### 6. LEFT
- Returns the specified number of characters from the start of a text string.
- Syntax - LEFT(Text, NumberOfCharactors)

### 7. RIGHT
- Returns the specified number of characters from the end of a text string.
- Syntax - LEFT(Text, NumberOfCharactors)

### 8. MID
- Returns a string of characters from the middle of a text string, given a starting position and length.
- Syntax - MID(Text, StartPosition, NumberOfCharactors)

### 9. LEN
- Returns the number of characters in a text string.
- Syntax - LEN(Text)

## Example -
```dax
DEFINE
    VAR Val = "DAX is so cool!"
EVALUATE
{
    ( "LEFT ( Val, 3 ) ",   LEFT  ( Val, 3     ) ),
    ( "RIGHT ( Val, 5 )",   RIGHT ( Val, 5     ) ),
    ( "MID ( Val, 11, 4 )", MID   ( Val, 11, 4 ) ),
    ( "LEN ( Val )",        LEN   ( Val        ) )
}
```

### 10. LOWER
- Converts all letters in a text string to lowercase.
- Syntax - LOWER ( TEXT )

### 11. UPPER
- Converts all letters in a text string to uppercase.
- Syntax - UPPER ( TEXT )
  
## Example -
```dax
DEFINE
    VAR Val = "DAX is so cool!"

EVALUATE
{
    ( "Original = " & Val ),
    ( "UPPER = " & UPPER ( Val ) ),
    ( "LOWER = " & LOWER ( Val ) )
}=
```

### 12. REPLACE
- Replaces part of a text string with a different text string.
- Syntax - REPLACE(OldText, StartPosition, NumberOfchar, NewText)

## Example -
```dax
DEFINE
    VAR Val = "DAX is so cool !"
    VAR Replacement = "fantastic"

EVALUATE
{ ( "Original", Val ), ( "Replaced", REPLACE ( Val, 11, 4, Replacement ) ) }

```

### 13. SEARCH
- Returns the starting position of one text string within another text string. SEARCH is not case-sensitive, but it is accent-sensitive.
- Syntax - SEARCH(FindText, WithinText, StartPosition, NotFoundValue)
- NOTE - SEARCH supports wildcards, whereas FIND does not.

## Example -
```dax
EVALUATE
CALCULATETABLE (
    ADDCOLUMNS (
        TOPN ( 5, VALUES ( 'Product'[Product Name] ) ),
        "player*blue", SEARCH ( "player*blue", 'Product'[Product Name], 1, BLANK () )
    ),
    'Product'[Color] IN { "Red", "Blue" }
)
```

### 3. TRIM
- Removes all spaces from a text string except for single spaces between words.
- Syntax - TRIM( Text )

## Example -
```dax
DEFINE
    VAR Test = "  DAX is          awesome !!!    "

EVALUATE
{ ( "Original", Test ), ( "Trimmed", TRIM ( Test ) ) }
```

### 4. VALUE
- Converts a text string that represents a number to a number.
- Syntax - VALUE( Text )

- ## Example -
```dax
EVALUATE
{
    ( "INT",            123,                     VALUE ( "123"        ) ),
    ( "FLOAT",          123.45678,               VALUE ( "123.45678"  ) ),
    ( "Scientific (1)", 123e3,                   VALUE ( "123e3"      ) ),
    ( "Scientific (2)", 123e-3,                  VALUE ( "123e-3"     ) ),
    ( "Date (1)",       DATE ( 2020, 10, 23 ),   VALUE ( "2020-10-23" ) ),
    ( "Date (2)",       DATE ( 2020, 10, 23 ),   VALUE ( "10/23/2020" ) ),
    ( "Date (3)",       DATE ( 2020, 10, 23 ),   VALUE ( "23/10/2020" ) ),
    ( "Time (1)",       TIME ( 10, 23, 45 ),     VALUE ( "10:23:45"   ) ),
    ( "Time (2)",       TIME ( 18, 05, 00 ),     VALUE ( "18:05:00"   ) ),
    ( "Time (3)",       TIME ( 18, 05, 00 ),     VALUE ( "6:05:00 pm" ) ),
    ( "Time (4)",       TIME ( 18, 05, 00 ),     VALUE ( "6:05pm"     ) )
}
```
