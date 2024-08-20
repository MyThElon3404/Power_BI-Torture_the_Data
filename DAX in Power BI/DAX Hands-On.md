## DAX Functions with Example

- #### MATHs & STATs Functions ->
<details>
  <summary> Click Here for Functions </summary>

- ### SUM - Calculates the total sum of a column. 
		Total Sales = SUM(Table[Sales])
- ### AVERAGE - Calculates the AVG of column.
  		Average Sales = AVERAGE(Table[Sales])
- ### MAX/MIN - Finds the maximum or minimum value in a column.
		Max Sale = MAX(Table[Sales])
		Min Sale = MIN(Table[Sales])
- ### DIVIDE - Divides two numbers, with an option to specify an alternate result if the denominator is zero.
		AVG Price per Unit = DIVIDE([Total Sales], SUM(Maths_State_Funct[Quantity]))
- ### COUNT/COUNTA - Counts the number of rows or non-blank values in a column.
- ### CountRows - Counts the number of rows in a table or table expression.
- ### DistinctCount - Counts the number of unique, non-blank values in a column.
  		Count Measure = Count(Maths_State_Funct[ID])
  		CountA Measure = COUNTA(Maths_State_Funct[Quantity])
		CountRow Measure = COUNTROWS(Maths_State_Funct)
  		DistinctCount Measure = DISTINCTCOUNT(Maths_State_Funct[Price])
- ### Iterator Functions -
Iterator functions in DAX (Data Analysis Expressions) are a category of functions that evaluate an expression for each row of a table and then aggregate the results. Unlike simple aggregation functions like SUM or AVERAGE, which operate on entire columns, iterator functions work row by row, allowing for more complex calculations.

- ### SUMX - Sums up the results of an expression evaluated for each row in a table.
		SUMX Funct = SUMX(Maths_State_Funct, Maths_State_Funct[Price]*Maths_State_Funct[Quantity])
- ### AVERAGEX - Averages the results of an expression evaluated for each row in a table.
  		Average Sales Per Transaction = AVERAGEX(Table, Table[Sales])
- ### MAX/MIN - Finds the maximum or minimum value in a column.
		Max Profit = MAXX(Table, Table[Sales] - Table[Quantity])
		Min Profit = MINX(Table, Table[Sales] - Table[Quantity])
- ### DIVIDE - Divides two numbers, with an option to specify an alternate result if the denominator is zero.
		AVG Price per Unit = DIVIDE([Total Sales], SUM(Maths_State_Funct[Quantity]))
- ### COUNTX - Counts the rows that result from an expression evaluated for each row in a table.
  		CountX Funct = COUNTAX(Maths_State_Funct, if(Maths_State_Funct[Quantity] > 90, 1, BLANK()))
</details>

- #### Logical Functions ->
<details>
  <summary> Click Here for Functions </summary>

- #### IF - The IF function checks a condition and returns one value if the condition is true and another value if the condition is false.
		Simple If Funct = IF([Total Sales LF] > 9000, "Great", "Good")
		Nested If Funct = IF([Total Sales LF] >= 50000, "High", IF([Total Sales LF] < 50000 & [Total Sales LF] >= 10000, "Medium", "Low"))
  		Bonus = IF(Sales[Total Sales] > 50000, Sales[Total Sales] * 0.1, Sales[Total Sales] * 0.05)
- #### AND - The AND function returns TRUE if all arguments are true, and FALSE otherwise
  		High_Performer = IF(AND(Sales[Total Sales] > 50000, Sales[Attendance] > 95), "Yes", "No")
- #### OR - The OR function returns TRUE if at least one of the conditions is true.
		Qualified = IF(OR(Sales[Total Sales] > 50000, Sales[Experience] > 5), "Yes", "No")
- #### NOT - The NOT function reverses the result of a logical expression.
		Below_Average = IF(NOT(Sales[Total Sales] > 30000), "Yes", "No")
- #### SWITCH - The SWITCH function evaluates an expression against a list of values and returns one based on matching results.
  		CountX Funct = COUNTAX(Maths_State_Funct, if(Maths_State_Funct[Quantity] > 90, 1, BLANK()))
- #### IFERROR - The IFERROR function returns a specified value if an expression results in an error.
		DivisionResult = IFERROR(Sales[Total Sales] / Sales[No. of Products], "Error")
- #### TRUE and FALSE - TRUE and FALSE return the respective logical values.
		AlwaysTrue = TRUE()
		AlwaysFalse = FALSE()
</details>

- #### Text Functions ->
<details>
  <summary> Click Here for Functions </summary>

- #### CONCATENATE - Combines two text strings into one.
		FullName = CONCATENATE(Orders[FirstName], Orders[LastName])
- #### COMBINEVALUES - Joins multiple text strings with a specified delimiter.
  		FullNameWithSpace = COMBINEVALUES(" ", Orders[FirstName], Orders[LastName])
- #### FORMAT - Converts a value to text according to a specified format.
		FormattedDate = FORMAT(Orders[OrderDate], "DD/MM/YYYY")
- #### LEFT/MID/RIGHT -
  	- LEFT: Extracts a specified number of characters from the start.
  	- LeftPart = LEFT(Orders[ProductCode], 3)
	- MID: Extracts characters from the middle.
	- RIGHT: Extracts a specified number of characters from the end.
 		LeftPart = LEFT(Orders[ProductCode], 3)
		MidPart = MID(Orders[ProductCode], 2, 3)
		RightPart = RIGHT(Orders[ProductCode], 4)


- #### SWITCH - The SWITCH function evaluates an expression against a list of values and returns one based on matching results.
  		CountX Funct = COUNTAX(Maths_State_Funct, if(Maths_State_Funct[Quantity] > 90, 1, BLANK()))
- #### IFERROR - The IFERROR function returns a specified value if an expression results in an error.
		DivisionResult = IFERROR(Sales[Total Sales] / Sales[No. of Products], "Error")
- #### TRUE and FALSE - TRUE and FALSE return the respective logical values.
		AlwaysTrue = TRUE()
		AlwaysFalse = FALSE()
</details>
