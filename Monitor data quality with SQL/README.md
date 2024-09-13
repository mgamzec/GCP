# Monitor data quality with SQL
By monitoring your data, you become aware of any problems that may occur within the ETL pipeline and data warehouse design. This can help you address problems as early as possible and avoid future problems.

In this reading, you’ll follow a fictional scenario where a BI engineer performs quality testing on their pipeline and suggests SQL queries that one could use for each step of testing.

## The scenario
At Francisco’s Electronics, an electronics manufacturing company, a BI engineer named Sage designed a data warehouse for analytics and reporting. After the ETL process design, Sage created a diagram of the schema.
![image](https://github.com/user-attachments/assets/e61f9bdb-db7f-4351-84d7-b2e6a19aadce)


The sales_warehouse database schema. The Sales table connects to the Products, Users, Locations, and Orders tables.
The diagram of the schema of the sales_warehouse database contains different symbols and connectors that represent two important pieces of information: the major tables within the system and the relationships among these tables.

The sales_warehouse database schema contains five tables:
- Sales 
- Products
- Users
- Locations
- Orders

These tables are connected via keys. The tables contain five to eight columns (or attributes) ranging in data type. The data types include varchar or char (or character), integer, decimal, date, text (or string), timestamp, and bit.

The foreign keys in the Sales table link to each of the other tables:
- The “product_id” foreign key links to the Products table
- The “user_id” foreign key links to the Users table
- The “order_id” foreign key links to the Orders table 
- The “shipping_address_id” and “billing_address_id” foreign keys link to the Locations table

After Sage made the sales_warehouse database, the development team made changes to the sales site. As a result, the original OLTP database changed. Now, Sage needs to ensure the ETL pipeline works properly and that the warehouse data matches the original OLTP database. 

Sage used the original OLTP schema from the store database to design the warehouse.
![image](https://github.com/user-attachments/assets/bc21256f-73cd-43d3-bd9a-5d70f0abf868)

The store database schema also contains five tables—Sales, Products, Users, Locations, and Orders—which are connected via keys. The tables contain four to eight columns ranging in data type. The data types include varchar or char, integer, decimal, date, text, timestamp, bit, tinyint, and datetime.

Every table in the store database has an id field as a primary key. The database contains the following tables:
The Sales table has price, quantity, and date columns. It references a user who made a sale (UserId), purchased a product (ProductId), and a related order (OrderId). Also, it references the Locations table for shipping and billing addresses (ShippingAddressId and BillingAddressId, respectively).

- The Users table has FirstName, LastName, Email, Password, and other user-related columns.
- The Locations table contains address information (Address1, Address2, City, State, and Postcode).
- The Products table has Name, Price, InventoryNumber, and Category of products.
- The Orders table has OrderNumber and purchase information (Subtotal, ShippingFee, Tax, Total, and Status).

## Using SQL to find problems
Sage compared the sales_warehouse database to the original store database to check for completeness, consistency, conformity, accuracy, redundancy, integrity, and timeliness. Sage ran SQL queries to examine the data and identify quality problems. Then Sage prepared the following table of lists, which include the types of quality issues found, the quality strategies that were violated, the SQL codes used to find the issues, and specific descriptions of the issues.

Quality testing sales_warehouse
Using SQL to find problems
Sage compared the sales_warehouse database to the original store database to check for completeness, consistency, conformity, accuracy, redundancy, integrity, and timeliness. Sage ran SQL queries to examine the data and identify quality problems. Then Sage prepared the following table of lists, which include the types of quality issues found, the quality strategies that were violated, the SQL codes used to find the issues, and specific descriptions of the issues.


