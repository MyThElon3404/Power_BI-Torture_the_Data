# Logical Functions
Logical functions act upon an expression, to return information about the values or sets in the expression.

### 1. AND (&&)
- Checks whether all arguments are TRUE, and returns TRUE if all arguments are TRUE.
- Syntax - AND( expression1, expression2)

### 2. OR (||)
- Returns TRUE if any of the arguments are TRUE, and returns FALSE if all arguments are FALSE.
- Syntax - OR(expression1, expression2)

- ## Example -
```dax
EVALUATE
VAR A = TRUE
VAR B = FALSE
VAR C = TRUE
RETURN
    {
        ( "Using AND", AND ( A, AND ( B, C ) ) ),
        ( "Using &&", A && B && C ),
        ( "Using OR", OR ( A, OR ( B, C ) ) ),
        ( "Using ||", A || B || C )
    }
```

### 3. COALESCE
- Returns the first argument that does not evaluate to a blank value. If all arguments evaluate to blank values, BLANK is returned.
- Syntax - COALESCE ( Value1, Value2 )

- ## Example -
```dax
EVALUATE
SELECTCOLUMNS (
    TOPN ( 10, Store ),
    "Store Name", Store[Store Name],
    "Manager Name", COALESCE ( Store[Area Manager], "*** NOT ASSIGNED ***" ),
    "Years Open",
        DATEDIFF ( Store[Open Date], COALESCE ( Store[Close Date], TODAY () ), YEAR ) 
)
```

### 4. IF
- Checks whether a condition is met, and returns one value if TRUE, and another value if FALSE.
- Syntax - IF ( LogicalTest, ResultIfTrue )

- ## Example -
```dax
EVALUATE
ADDCOLUMNS (
    VALUES ( 'Product'[Brand] ),
    "Sales 1", [Sales Amount],
    "Sales 2",
        VAR SalesAmount = [Sales Amount]
        RETURN
            IF ( SalesAmount > 3000000, 3000000, SalesAmount ),
    "Sales 3", MIN ( [Sales Amount], 3000000 )
)
ORDER BY 'Product'[Brand]
```

### 5. SWITCH
- Returns different results depending on the value of an expression.
- Syntax - SWITCH(
    expression,
    value1, result1,
    value2, result2,
)

- ## Example -
```dax
EVALUATE
ADDCOLUMNS (
    VALUES ( 'Product'[Brand] ),
    "Sales 1", [Sales Amount],
    "Sales 2",
        VAR SalesAmount = [Sales Amount]
        RETURN
            IF ( SalesAmount > 3000000, 3000000, SalesAmount ),
    "Sales 3", MIN ( [Sales Amount], 3000000 )
)
ORDER BY 'Product'[Brand]
```
