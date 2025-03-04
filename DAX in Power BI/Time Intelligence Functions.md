# Time Intelligence Functions
Time intelligence functions support calculations to compare and aggregate data over time periods, supporting days, months, quarters, and years.

### 1. DATEADD
- Moves the given set of dates by a specified interval.
- Syntax - DATEADD(Date, NumberOfInterval, Interval(Year, Quarter, Month, Day))

## Example -
```dax
DEFINE
    MEASURE Sales[Same Period Last Month] =
        CALCULATE ( [Sales Amount], DATEADD ( 'Date'[Date], -1, MONTH ) )
    MEASURE Sales[Same Period Last Quarter] =
        CALCULATE ( [Sales Amount], DATEADD ( 'Date'[Date], -1, QUARTER ) )
    MEASURE Sales[Same Period Last Year] =
        CALCULATE ( [Sales Amount], DATEADD ( 'Date'[Date], -1, YEAR ) )

EVALUATE
SUMMARIZECOLUMNS (
    'Date'[Calendar Year Month],
    "SPLM", [Same Period Last Month],
    "SPLQ", [Same Period Last Quarter],
    "SPLY", [Same Period Last Year]
)
```

### 2. DATESBETWEEN
- Returns the dates between two given dates.
- Syntax - DATESBETWEEN( Date, StartDate, EndDate )

## Example -
```dax
EVALUATE
DATESINPERIOD (
  'Date'[Date],           -- Return dates in Date[Date]
  DATE ( 2008, 08, 15 ),  -- Starting from 08/15/2008
  3,                      -- the set needs to contain 3
  DAY                     -- days
)
```

### 3. DATESINPERIOD
- Returns the dates from the given period.
- Syntax - DATESINPERIOD( Date, StartDate, NumberOfInterval, Interval(Day, Month, Quarter, Year))

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

### 4. DATESMTD
- Returns a set of dates in the month up to the last date visible in the filter context.
- Syntax - DATESMTD( Date )

- ## Example -
```dax
EVALUATE
CALCULATETABLE (
    DATESMTD ( 'Date'[Date] ),
    'Date'[Date] >= DATE ( 2007, 2, 5 )
        && 'Date'[Date] <= DATE ( 2007, 5, 6 )
)
ORDER BY [Date] ASC
```

### 5. DATESQTD
- Returns a set of dates in the quarter up to the last date visible in the filter context.
- Syntax - DATESQTD ( Date )

## Example -
```dax
EVALUATE
CALCULATETABLE (
    DATESQTD ( 'Date'[Date] ),
    'Date'[Date] >= DATE ( 2007, 2, 5 )
        && 'Date'[Date] <= DATE ( 2007, 5, 12 )
)
ORDER BY [Date] ASC
```

### 6. DATESYTD 
- Returns a set of dates in the year up to the last date visible in the filter context.
- Syntax - DATESYTD( Date )

## Example -
```dax
EVALUATE
CALCULATETABLE (
    DATESYTD ( 'Date'[Date] ),
    'Date'[Date] >= DATE ( 2007, 2, 5 )
        && 'Date'[Date] <= DATE ( 2007, 5, 12 )
)
ORDER BY [Date] ASC
```

### 7. ENDOFMONTH
- Returns the end of month.
- Syntax - ENDOFMONTH( Date )

### 8. STARTOFMONTH
- Returns the Start of month.
- Syntax - ENDOFMONTH( Date )

- Example -
```dax
EVALUATE
    CALCULATETABLE (
        STARTOFMONTH ( 'Date'[Date] ),
        'Date'[Date] >= DATE ( 2007, 2, 5 ) &&
        'Date'[Date] <= DATE ( 2007, 5, 12 )
    )
     
EVALUATE
    CALCULATETABLE (
        ENDOFMONTH ( 'Date'[Date] ),
        'Date'[Date] >= DATE ( 2007, 2, 5 ) &&
        'Date'[Date] <= DATE ( 2007, 5, 12 )
    )
```

### 9. ENDOFQUARTER
- Returns the end of month.
- Syntax - ENDOFMONTH( Date )

### 10. STARTOFQUARTER
- Returns the Start of month.
- Syntax - STARTOFMONTH( Date )

- Example -
```dax
EVALUATE
CALCULATETABLE (
    STARTOFQUARTER ( 'Date'[Date] ),
    'Date'[Date] = DATE ( 2007, 5, 12 )
)
 
EVALUATE
CALCULATETABLE (
    ENDOFQUARTER ( 'Date'[Date] ),
    'Date'[Date] = DATE ( 2007, 5, 12 )
)
```

### 11. ENDOFYEAR
- Returns the end of Year.
- Syntax - ENDOFYEAR( Date )

### 12. STARTOFYEAR
- Returns the Start of Year.
- Syntax - STARTOFYEAR( Date )

- Example -
```dax
EVALUATE
CALCULATETABLE (
    STARTOFYEAR ( 'Date'[Date] ),
    'Date'[Date] = DATE ( 2007, 5, 12 )
)
 
EVALUATE
CALCULATETABLE (
    ENDOFYEAR ( 'Date'[Date] ),
    'Date'[Date] = DATE ( 2007, 5, 12 )
)
```

### 11. FIRSTDATE
- Returns first non blank date.
- Syntax - FIRSTDATE( Date )

### 12. LASTDATE
- Returns last non blank date.
- Syntax - LASTDATE( Date )

- Example -
```dax
DEFINE
VAR StartDate = DATE ( 2008, 08, 15 )
VAR EndDate   = DATE ( 2008, 08, 31 )
 
EVALUATE
    CALCULATETABLE (
        FIRSTDATE ( 'Date'[Date] ),
        'Date'[Date] >= StartDate && 'Date'[Date] <= EndDate
    )
     
EVALUATE
    CALCULATETABLE (
        LASTDATE ( 'Date'[Date] ),
        'Date'[Date] >= StartDate && 'Date'[Date] <= EndDate
    )
```

### 13. NEXTDAY / NEXTMONTH / NEXTQUARTER / NEXTYEAR
- Returns a next day.
- Syntax - NEXTDAY( Date )

### 14. PREVIOUSDAY / PREVIOUSMONTH / PREVIOUSQUARTER / PREVIOUSYEAR
- Returns a previous day.
- Syntax - PREVIOUSDAY( Date )

- Example -
```dax
EVALUATE
CALCULATETABLE (
    PREVIOUSDAY ( 'Date'[Date] ),  
    'Date'[Date] >= DATE ( 2008, 08, 15 ) &&
    'Date'[Date] <= DATE ( 2008, 08, 20 )
)
ORDER BY [Date] ASC

EVALUATE
CALCULATETABLE (
    NEXTDAY ( 'Date'[Date] ),  
    'Date'[Date] >= DATE ( 2008, 08, 15 ) &&
    'Date'[Date] <= DATE ( 2008, 08, 20 )
)
ORDER BY [Date] ASC
```

### 15. SAMEPERIODLASTYEAR
- Returns a set of dates in the current selection from the previous year.
- Syntax - SAMEPERIODLASTYEAR ( Date )

- Example -
```dax
EVALUATE
VAR StartDate = DATE ( 2008, 07, 25 )
VAR EndDate =   DATE ( 2008, 07, 31 )
RETURN
    CALCULATETABLE (
        SAMEPERIODLASTYEAR ( 'Date'[Date] ),
        'Date'[Date] >= StartDate &&
        'Date'[Date] <= EndDate
    )
ORDER BY [Date]
```
