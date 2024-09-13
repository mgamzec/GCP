- The SELECT clause selects the address of each tree. By using the COUNT function, you count the number of trees at each address and return a single row of data per address, instead of per tree. This data is saved as a new column.

- The FROM clause is straightforward as it specifies the street_trees table within the San Francisco Street Trees dataset. 

- The WHERE clause is necessary to ensure that your target table only includes rows that have a value in the address column. 

- The GROUP BY clause specifies that you’re grouping data by the address, and the ORDER BY clause sorts the data in descending order by number_of_trees column.

- The LIMIT clause limits the query to return only the top ten rows of data. When working with large datasets, including a limit will decrease the processing time required to return the data. 
