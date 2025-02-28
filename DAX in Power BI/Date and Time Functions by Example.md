# Date and Time Functions
Date and time functions help create calculations based on dates and time. Many of the functions in DAX are similar to the Excel date and time functions.

### 1. CALENDAR
- Returns a table with one column of all dates between StartDate and EndDate.
- Syntax - CALENDAR( StartDate, EndDate)

- ## Example -
```dax
EVALUATE
    CALENDAR (
        DATE ( 2022, 11, 26 ), -- Start Date
        DATE ( 2022, 12, 5 ) -- End Date
    )
ORDER BY [Date] DESC
```

### 2. DATE / TIME
- Returns the specified date in datetime format.
- Syntax - DATE (Year, Month, Day) / TIME(HH, MM, SS)

- ## Example -
```dax
EVALUATE
    {
        DATE ( 2020, 10, 15 ),
        TIME ( 22, 45, 30 ),
        DATE ( 2020, 10, 15 ) + TIME ( 22, 45, 30 )
    }
```

### 3. DATEDIFF
- Returns the number of units (unit specified in Interval) between the input two dates.
- Syntax - DATEDIFF ( StartDate, EndDate, Interval ) -- Interval (Year, Month, Day)

- ## Example -
```dax
EVALUATE
VAR StartDate =  DATE ( 2011, 01, 01 )
VAR EndDate =    DATE ( 2012, 12, 15 )
RETURN
    {
        ( "DATEDIFF Year",     DATEDIFF ( StartDate, EndDate, YEAR ) ),
        ( "DATEDIFF Quarter",  DATEDIFF ( StartDate, EndDate, QUARTER ) ),
        ( "DATEDIFF Month",    DATEDIFF ( StartDate, EndDate, MONTH ) ),
        ( "DATEDIFF Day",      DATEDIFF ( StartDate, EndDate, DAY ) ),
        ( "Subtraction-1",     INT ( EndDate - StartDate ) ),
        ( "Subtraction-2",     CONVERT ( EndDate - StartDate, INTEGER ) ),
        ( "YEARFRAC",          YEARFRAC ( StartDate, EndDate ) )
    }   
```

### 4. DATEVALUE / TIMEVALUE
- Converts a date in the form of text to a date in datetime format.
- Syntax - DATEVALUE ( TextDate ) / TIMEVALUE ( TextDate )

- ## Example -
```dax
EVALUATE
{
    DATEVALUE ( "28/02/2020" ),
    DATEVALUE ( "02/28/2020" ),
    DATEVALUE ( "08/10/2020" ),  -- 10th of August
    DATEVALUE ( "2020-02-06" )
}
```

### 5. DAY / MONTH / QUARETER / YEAR
- Returns a number from 1 to 31 representing the day of the month.
- Returns a number from 1 (January) to 12 (December) representing the month.
- Returns a number from 1 (January-March) to 4 (October-December) representing the quarter.
- Returns the year of a date as a four digit integer.
- Syntax - DAY(date) / MONTH(date) / QUARTER(date) / YEAR(date)

- ## Example -
```dax
EVALUATE
ADDCOLUMNS (
    TOPN ( 10, VALUES ( 'Date'[Date] ), 'Date'[Date], ASC ),
    "Year", YEAR ( 'Date'[Date] ),
    "Quarter", QUARTER ( 'Date'[Date] ),
    "Month", MONTH ( 'Date'[Date] ),
    "Day", DAY ( 'Date'[Date] )
)
ORDER BY 'Date'[Date]
```

### 6. WEEKDAY
- Returns a number identifying the day of the week of a date. The number is in a range 1-7 or 0-6 according to the choice of the ReturnType parameter.
- Syntax - WEEKDAY(date, returnType) -- returnType - A number that determines the return value

- ## Example -
```dax
EVALUATE
ADDCOLUMNS (
    TOPN ( 10, VALUES ( 'Date'[Date] ), 'Date'[Date], ASC ),
    "Day of week", FORMAT  ( 'Date'[Date], "dddd" ),
    "Weekday",     WEEKDAY ( 'Date'[Date]      ),   -- 1 is Sunday (Default)
    "Weekday 1",   WEEKDAY ( 'Date'[Date], 1   ),   -- 1 is Sunday
    "Weekday 2",   WEEKDAY ( 'Date'[Date], 2   ),   -- 1 is Monday
    "Weekday 3",   WEEKDAY ( 'Date'[Date], 3   ),   -- 0 is Monday
    "Weekday 11",  WEEKDAY ( 'Date'[Date], 11  ),   -- 1 is Monday
    "Weekday 12",  WEEKDAY ( 'Date'[Date], 12  ),   -- 1 is Tuesday
    "Weekday 13",  WEEKDAY ( 'Date'[Date], 13  ),   -- 1 is Wednesday
    "Weekday 14",  WEEKDAY ( 'Date'[Date], 14  )    -- ...
)
ORDER BY [Date]
```

### 7. WEEKNUM
- Returns the week number in the year.
- Syntax - WEEKNUM(date, returnType)

- ## Example -
```dax
EVALUATE
ADDCOLUMNS (
    TOPN ( 10, VALUES ( 'Date'[Date] ), 'Date'[Date], ASC ),
    "Day of week", FORMAT ( 'Date'[Date], "dddd" ),
    "WEEKNUM",    WEEKNUM ( 'Date'[Date] ) ,   -- Same as 1, week start on Sun
    "WEEKNUM  2", WEEKNUM ( 'Date'[Date],  2 ), -- Week start on Mon
    "WEEKNUM 11", WEEKNUM ( 'Date'[Date], 11 ), -- 11 to 17: 1st DOW Mon
    "WEEKNUM 12", WEEKNUM ( 'Date'[Date], 12 ), -- 11 to 17: 1st DOW Tue
    "WEEKNUM 13", WEEKNUM ( 'Date'[Date], 13 ), -- 11 to 17: 1st DOW Wed
    "WEEKNUM 21", WEEKNUM ( 'Date'[Date], 21 ) -- ISO 8601 Week
                                                -- (1st thursday of the year)
)
ORDER BY 'Date'[Date]
```

### 8. EMONTH 
- Returns the date that is the indicated number of months before or after the start date.
- Syntax - EMONTH(startdate, months) -- neither positive value or negative value (-1 or +1)

- ## Example -
```dax
EVALUATE
ADDCOLUMNS (
    TOPN ( 10, VALUES ( 'Date'[Date] ), 'Date'[Date], ASC ),
    "EDATE, +1", EDATE ( 'Date'[Date], +1 ),
    "EDATE, -1", EDATE ( 'Date'[Date], -1 ),
)
ORDER BY 'Date'[Date]
```

### 9. EOMONTH
- Returns the date in datetime format of the last day of the month before or after a specified number of months.
- Syntax - EOMONTH(startdate, months)

- ## Example -
```dax
EVALUATE
ADDCOLUMNS (
    TOPN ( 10, VALUES ( 'Date'[Date] ), 'Date'[Date], ASC ),
    "End current month", EOMONTH ( 'Date'[Date], 0 ),
    "End next month", EOMONTH ( 'Date'[Date], +1 ),
    "End prev. month", EOMONTH ( 'Date'[Date], -1 ),
    "Start current month", EOMONTH ( 'Date'[Date], -1 ) + 1,
    "Start next month", EOMONTH ( 'Date'[Date], 0 ) + 1,
    "Start prev. month", EOMONTH ( 'Date'[Date], -2 ) + 1
)
ORDER BY 'Date'[Date]
```
