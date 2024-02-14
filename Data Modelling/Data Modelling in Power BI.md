# **_Database normalization:_**
A set of guidelines and procedures for data modeling is called database normalization. You may compare it to creating or organizing a database.
- **Removing redundant data:** When the same data is kept in different locations, that is. File sizes can be reduced and inconsistent data can be avoided by reducing redundancy
- **Table relationships:** Table relationships are established using _primary and foreign keys_. Primary keys are the column(s) that uniquely identify each row of data that is not empty. The primary key is a shorthand term for the distinctive value that is given to each row. This process becomes important when you are referencing rows in a different table, which is what foreign keys do.

## **_Types of data modeling process:_**  
The process will start with a conceptual model, progress to a logical model, and conclude with a physical model

![Types of data models](https://www.altamira.ai/wp-content/uploads/2022/09/Factors-influencing-development-speed-1024x789.jpg)

**1.**  **_Conceptual data models:_** They are also referred to as domain models and offer a big-picture view of what the system will contain, how it will be organized, and which business rules are involved. Conceptual models are usually created as part of the process of gathering initial project requirements

![Conceptual data models](https://www.ibm.com/content/dam/connectedassets-adobe-cms/worldwide-content/creative-assets/s-migr/ul/g/ae/c5/conceptual-data-modeling.png)

**2.**  **_Logical data models:_** They are less abstract and provide greater detail about the concepts and relationships in the domain under consideration. One of several formal data modeling notation systems is followed. These indicate data attributes, such as data types and their corresponding lengths, and show the relationships among entities. Logical data models don’t specify any technical system requirements

![Conceptual data models](https://www.ibm.com/content/dam/connectedassets-adobe-cms/worldwide-content/creative-assets/s-migr/ul/g/73/fd/logical-data-modeling.png)

**3.**  **_Physical data models:_** They provide a schema for how the data will be physically stored within a database. As such, they’re the least abstract of all. They offer a finalized design that can be implemented as a relational database, including associative tables that illustrate the relationships among entities as well as the primary keys and foreign keys that will be used to maintain those relationships. Physical data models can include database management system (DBMS)-specific properties.

![Conceptual data models](https://www.ibm.com/content/dam/connectedassets-adobe-cms/worldwide-content/creative-assets/s-migr/ul/g/82/20/physical-data-modeling.png)

##### ==========================================
#### **_To know more about data modeling refer to this links:_** 
IBM -> https://www.ibm.com/topics/data-modeling

Vertabelo -> https://vertabelo.com/blog/data-modeling-techniques/

Hevo -> https://hevodata.com/learn/power-bi-data-model/
##### ==========================================

## **_The Kimball Model:_** 
There are two key concepts in the Kimball model: facts and dimensions. Facts are the metrics from your business process. Dimensions provide the context surrounding a business process. These combine to form a star schema.

- **_Fact Table:_** The measurements or metrics from your business process are facts. Fact tables include values for observational or event data, such as sales orders, product counts, prices, transactional dates, and quantity. Keys are how we establish relationships between fact tables and dimension tables. The number of columns should be reduced and their size because they contain a lot of rows. 

- **_Dimension Table:_** Dimension tables contain the details about the data in fact tables: products, locations, employees, and order types. Dimensions provide the rest of the story while a fact may only provide the quantity or frequency. These tables are connected to the fact table through key columns. Dimension tables are used to filter and group the data tables. Dimension tables are typically short and wide. They don’t contain that many rows, but do contain a large amount of context for the facts.

## **_Data Modeling Techniques:_**

- **_Star Schema:_** Star schema is the type of multidimensional model that is used for data warehouse. In a star schema, The fact tables and the dimension tables are contained. In this schema, fewer foreign-key join is used. This schema forms a star with a fact table and dimension tables.

![Star Schema](https://th.bing.com/th/id/R.038b56503c695986ced4ca75093d6e87?rik=Iyv1qxPjD9UhYw&riu=http%3a%2f%2fatsc.com.sg%2fwp-content%2fuploads%2f2018%2f05%2f3.4.png&ehk=9x1BwCNkkw0lkt0aUC6lhs9dhA04MolVAA6P6Mvp%2fnM%3d&risl=&pid=ImgRaw&r=0)

- **_Snowflake Schema:_** Snowflake Schema is also the type of multidimensional model that is used for the data warehouse. In the snowflake schema, The fact tables, dimension tables as well as sub-dimension tables are contained. This schema forms a snowflake with fact tables, dimension tables as well as sub-dimension tables. 

![Star Schema](https://i1.wp.com/static.javatpoint.com/tutorial/datawarehouse/images/star-schema-vs-snowflake-schema2.png?resize=618%2C481&ssl=1)


