# Logical Functions
Logical functions act upon an expression, to return information about the values or sets in the expression.

### 1. AND (&&)
- Checks whether all arguments are TRUE, and returns TRUE if all arguments are TRUE.
- Syntax - AND(<expression>, <expression>)

### 2. OR (||)
- Returns TRUE if any of the arguments are TRUE, and returns FALSE if all arguments are FALSE.
- Syntax - OR(<expression>, <expression>)

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
