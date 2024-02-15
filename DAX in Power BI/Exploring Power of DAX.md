# **_Let's Start with DAX_**

- Data Analysis Expressions (DAX) is a formula expression language used in Analysis Services, Power BI, and Power Pivot in Excel. DAX formulas include functions, operators, and values to perform advanced calculations and queries on data in related tables and columns in tabular data models.

## **_Types of DAX:_** Calculated Measures and Calculated Columns
DAX formulas are used in measures, calculated columns, calculated tables, and row-level security.

## **_Automatic Measures and Measures:_**

## **_Measure:_**
- Measures are dynamic calculation formulas where the results change depending on context. Measures are used in reporting that support combining and filtering model data by using multiple attributes such as a Power BI report or Excel PivotTable or PivotChart. Measures are created by using the DAX formula bar in the model designer.

- Measures in Power BI are dynamic calculations used in reports and visualizations. Unlike regular columns, measures are not stored in the dataset but are calculated on the fly, providing real-time insights. Commonly utilized in summarizing data, measures aggregate information based on defined calculations.
- 
**_1. Automatic Measures:_** In most cases, Power BI Desktop automatically generates a measure for you.

![automatic measure](https://editor.analyticsvidhya.com/uploads/420502022-09-14%20(6).png)

**_2. DAX Calculated Measures:_** Here we calculate measures by the DAX formula.

![measure](https://cdn.educba.com/academy/wp-content/uploads/2020/01/Measures-in-Power-BI.jpg)

### **_Steps to Create Calculated Measure:_**
- Step 1 - Power BI Desktop’s Modeling section.
- Step 2 - Next, choose the “New Measure” menu item.

![measure](https://editor.analyticsvidhya.com/uploads/173612022-09-14%20(7).png)

- right-click on the table where you want to create a measure you can see the pop-up. From there select the new measure option.

![measure](https://www.wallstreetmojo.com/wp-content/uploads/2019/09/measures-in-power-bi.png)

- Step 3 - The words “Measure =” will appear in a Formulas window.

![measure](https://editor.analyticsvidhya.com/uploads/297242022-09-14%20(8).png)

- Step 4 -  You can change “Measure” to any other name for a unit of measurement.

![measure](https://editor.analyticsvidhya.com/uploads/259822022-09-14%20(9).png)

- Step 5 - Next, type the expression for the resultant size to the right of the equals sign.
- 
![measure](https://editor.analyticsvidhya.com/uploads/727542022-09-14%20(10).png)

-  Once you’ve made a measurement, you may give it a new name by clicking on the calculator icon that appears next to the measure’s name in the table where it was made

## **_Calculated columns:_**
- A calculated column is a column that you add to an existing table (in the model designer) and then create a DAX formula that defines the column's values. When a calculated column contains a valid DAX formula, values are calculated for each row as soon as the formula is entered. Values are then stored in the in-memory data model.

![Calculated Columns](https://spreadsheeto.com/wp-content/uploads/2019/12/new-calculated-column.png)

### **_Steps to Create Calculated Columns:_**
- Step 1 - Turn on the Power BI Desktop
- Step 2 - In the Power BI Desktop left pane, select the Data tab / Table View / Data View.

![measure](https://editor.analyticsvidhya.com/uploads/437442022-09-21%20(1).png)

- Step 3 - Next, click the New Column button

![measure](https://editor.analyticsvidhya.com/uploads/812342022-09-21%20(2).png)

- Step 4 - In the Formula bar, enter “Column =” and hit enter.

![measure](https://editor.analyticsvidhya.com/uploads/523892022-09-21%20(3).png)

- Step 5 - The column can be changed to the desired column name.

# **_Context in DAX_**
- Knowing the DAX context is crucial for mastering the DAX syntax with Power BI. In DAX, you can work with either a Row context or a Filter context.

## **_Row Context:_**
- Using a filtering row as a reference in a DAX expression means “row context.” The formula’s action on the current row is the primary concern in the row context. The rows of measures typically receive this kind of context.

## **_Filter Context:_**
- The filter context goes beyond a simple emphasis on values. Row context allowed us to select which rows to process and eliminate others. However, the phrase narrows in on particular values inside a row when used as a filter. Therefore, the filter context is used with the row context to restrict the range of values to which a calculation is applied. We apply filter context when we use CALCULATE, FILTER, RELATED, ALL, etc.

## **_Different Types of DAX in Power BI_**

![DAX](https://editor.analyticsvidhya.com/uploads/63088types%20of%20DAX.PNG)

- DAX is a powerful formula language that can be used to handle data modeling, add value to data, and visualize measures in Power BI. This tutorial has provided an overview of the basics of DAX, the components of a DAX expression, and the types of DAX measures. We have also discussed the detailed steps to create calculated columns and measures in Power BI.

## **_CALCULATE TABLE_**
- CALCULATETABLE is a DAX Function that evaluates a table expression in a context that has been modified by the given filters. It returns a value table. It is used to create Power BI calculated tables. The table expression to be evaluated is expression>. It is not possible to use a measure as an expression.
- Power BI Calculated tables come at a price: they expand the model’s storage space and can slow down data refresh. The reason for this is that when calculated tables have formula dependencies on refreshed tables, they recalculate. External data cannot be connected to a Power BI calculated table; instead, you must use Power Query.

![Calculated columns](https://i0.wp.com/sqlskull.com/wp-content/uploads/2020/06/Dax_Calculate.png?w=1001&ssl=1)

![Calculated columns](https://learn.microsoft.com/en-us/power-bi/transform-model/media/desktop-calculated-tables/calctables_westregionempl.png)

**_To know more about Calculated columns_** -> https://dax.guide/calculatetable/

**_To learn more about DAX_** -> https://dax.guide/
Here you get all DAX functions, formulae, and many more.


