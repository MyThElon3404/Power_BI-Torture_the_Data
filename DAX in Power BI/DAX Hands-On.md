# DAX Functions with Example

- ### MATHs & STATs Functions ->
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

- #### SUMX - Sums up the results of an expression evaluated for each row in a table.
		SUMX Funct = SUMX(Maths_State_Funct, Maths_State_Funct[Price]*Maths_State_Funct[Quantity])
- #### AVERAGEX - Averages the results of an expression evaluated for each row in a table.
  		Average Sales Per Transaction = AVERAGEX(Table, Table[Sales])
- #### MAX/MIN - Finds the maximum or minimum value in a column.
		Max Profit = MAXX(Table, Table[Sales] - Table[Quantity])
		Min Profit = MINX(Table, Table[Sales] - Table[Quantity])
- #### DIVIDE - Divides two numbers, with an option to specify an alternate result if the denominator is zero.
		AVG Price per Unit = DIVIDE([Total Sales], SUM(Maths_State_Funct[Quantity]))
- #### COUNTX - Counts the rows that result from an expression evaluated for each row in a table.
  		CountX Funct = COUNTAX(Maths_State_Funct, if(Maths_State_Funct[Quantity] > 90, 1, BLANK()))
</details>

- ### Logical Functions ->
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

- ### Text Functions ->
<details>
  <summary> Click Here for Functions </summary>

- #### CONCATENATE - Combines two text strings into one.
		FullName = CONCATENATE(Orders[FirstName], Orders[LastName])
- #### COMBINEVALUES - Joins multiple text strings with a specified delimiter.
  		FullNameWithSpace = COMBINEVALUES(" ", Orders[FirstName], Orders[LastName])
- #### FORMAT - Converts a value to text according to a specified format.
		FormattedDate = FORMAT(Orders[OrderDate], "DD/MM/YYYY")
- #### LEFT/MID/RIGHT - Extracts a specified number of characters from the start / Extracts characters from the middle / Extracts a specified number of characters from the end.
 		LeftPart = LEFT(Orders[ProductCode], 3)
		MidPart = MID(Orders[ProductCode], 2, 3)
		RightPart = RIGHT(Orders[ProductCode], 4)
- #### UPPER/LOWER - Converts text to uppercase or lowercase.
  		UpperCase = UPPER(Orders[ProductName])
		LowerCase = LOWER(Orders[ProductName])
- #### LEN - Returns the number of characters in a text string.
		LengthOfName = LEN(Orders[ProductName])
- #### SEARCH/FIND - Finds the starting position of a substring within a string.
		Position = SEARCH("top", Orders[ProductName], 1, 0)
- #### REPLACE - Replaces part of a text string with another text string.
  		ReplacedText = REPLACE(Orders[ProductCode], 2, 3, "XYZ")
- #### SUBSTITUTE - Substitutes old text with new text in a string.
		SubstitutedText = SUBSTITUTE(Orders[ProductName], "top", "phone")
- #### TRIM - Removes all spaces from text except for single spaces between words.
		TrimmedText = TRIM(Orders[ProductName])
</details>

- ### Filter Functions ->
<details>
  <summary> Click Here for Functions </summary>

- #### CALCULATE - The CALCULATE function is one of the most powerful functions in DAX. It modifies the context in which data is filtered and then performs a calculation based on that modified context.
		Calculate = CALCULATE(SUM('Filter Functions'[Salary]), 'Filter Functions'[Department] = "IT")
- #### FILTER - The FILTER function returns a table that represents a subset of another table based on a condition.
  		Filter tb = FILTER('Filter Functions', 'Filter Functions'[Age] > 50)
- #### ALL - The ALL function removes all filters from a specified column or table. It is often used to create calculations that do not consider any existing filters.
		All Funct = CALCULATE(SUM('Filter Functions'[Salary]), ALL('Filter Functions'[Department]))
- #### ALLEXCEPT - The ALLEXCEPT function removes all filters from the specified table or column except for the ones mentioned.
 		AllExcept Funct = CALCULATE(SUM('Filter Functions'[Salary]), ALLEXCEPT('Filter Functions', 'Filter Functions'[Department]))
- #### ALLSELECTED - The ALLSELECTED function returns all rows in a table or all values in a column by ignoring any filters that might have been applied, except for those set by a visual or slicer.
		AllSelected Funct = CALCULATE(SUM('Filter Functions'[Salary]), ALLSELECTED('Filter Functions'))
- #### KEEPFILTERS - The KEEPFILTERS function applies a filter on top of an existing filter, ensuring that the new filter is respected.
  		UpperCase = UPPER(Orders[ProductName])
		LowerCase = LOWER(Orders[ProductName])
- #### REMOVEFILTERS - The REMOVEFILTERS function clears any filters that have been applied to the columns or tables specified.
		Position = SEARCH("top", Orders[ProductName], 1, 0)
- #### SELECTEDVALUE - The SELECTEDVALUE function returns the value of a column when only one value is selected, or it returns an alternative result when multiple values are selected.
  		SelectedValue = IF(HASONEVALUE('Filter Functions'[Department]), SUM('Filter Functions'[Salary]), BLANK())
  		SelectedValue Funct = SELECTEDVALUE('Filter Functions'[Department], "Select a Department")
- #### HASONEVALUE - The HASONEVALUE function in DAX is used to check whether there is exactly one distinct value in the current filter context for a specified column or expression. It returns a Boolean value: TRUE if there is exactly one distinct value and FALSE otherwise.
  		SalesInformation = SWITCH(TRUE(), HASONEVALUE(Product[Category]), SUM(Sales[SalesAmount]),
  			ISFILTERED(Product[Category]), "Multiple Categories Selected",
    			"No Category Selected")
- #### ISFILTERED - The ISFILTERED function in DAX checks whether a column or table has been filtered in the current context. It returns a Boolean value: TRUE if the column or table is filtered and FALSE otherwise.
  		Isfiltered = if(ISFILTERED('Filter Functions'[Department]), "Yes", "No")
</details>

- ### Table Functions ->
<details>
  <summary> Click Here for Functions </summary>

- #### SUMMARIZE - The SUMMARIZE function creates a summary table for the requested columns of a table. It groups the data by the specified columns and can calculate aggregations.
		Summarize tb = 
    			SUMMARIZE('Table Function', 
        			'Table Function'[Category], 
        			'Table Function'[SubCategory],
        			"Total Sales", SUM('Table Function'[SalesAmount]),
        			"Total Quantity", SUM('Table Function'[QuantitySold])
    			)
- #### ADDCOLUMNS - The ADDCOLUMNS function adds calculated columns to a table.
  		AddColumn tb = 
    			ADDCOLUMNS('Table Function',
        			"Profit", 'Table Function'[SalesAmount] - 100
    			)
- #### DISTINCT - The DISTINCT function returns a one-column table that contains the distinct values from the specified column.
		Distinct Funct = DISTINCT('Table Function'[Category])
- #### VALUES - The VALUES function returns a one-column table that contains the distinct values in a column or a one-row table that contains the distinct values in the columns.
 		Value Funct = VALUES('Table Function'[Category]) 
- #### UNION - The UNION function combines two or more tables by combining their rows.
		Union Funct = UNION('Table Function', 'Filter Functions')
- #### INTERSECT - The INTERSECT function returns a table that contains only the rows that are present in both tables.
  		Intersect tb = INTERSECT('Table Function', 'Logical Functions')
- #### TOPN - The TOPN function returns the top N rows of a table, based on a specified expression.
		Topn Funct = TOPN(10, 'Table Function', 'Table Function'[ID], ASC)
</details>

- ### Relationship Functions ->
<details>
  <summary> Click Here for Functions </summary>

- #### RELATED Function (Calculated Column) - The RELATED function in Power BI DAX is a powerful tool that allows you to fetch related data from another table based on an existing relationship between the tables. It is particularly useful in scenarios where you want to enrich your data model by pulling in additional details from a related table.
		Price = RELATED(Products_Relationship_F1[Price])
- #### RELATEDTABLE Function - The RELATEDTABLE function in Power BI DAX is used to retrieve a table containing all rows from a related table that are associated with the current row. It is particularly useful when you have a one-to-many relationship and you want to aggregate or analyze related rows from the "many" side of the relationship.
  		OrderCount = COUNTROWS(RELATEDTABLE(Orders_Relationship_F2))
</details>
