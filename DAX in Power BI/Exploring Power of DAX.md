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

## **_Calculated columns:_**
- A calculated column is a column that you add to an existing table (in the model designer) and then create a DAX formula that defines the column's values. When a calculated column contains a valid DAX formula, values are calculated for each row as soon as the formula is entered. Values are then stored in the in-memory data model.

![Calculated Columns](https://spreadsheeto.com/wp-content/uploads/2019/12/new-calculated-column.png)












