#### Talking to a Database

###### SQL Statements
 * SQL keywords are written in CAPS
 * Basic Structure of a SQL statement:
	`SELECT ______   
	FROM ______
	JOIN ______ ON ______
	WHERE ______`

* Example:  `SELECT * FROM employees WHERE name LIKE ‘b%’`
   * LIKE means “matches a pattern” and % means “starts with” (wildcard).

* Example 2: `SELECT products.id, products.name FROM order_details JOIN products ON  order_details.product_id = products.id WHERE order_details.order_id = 10250`

###### Joins
* http://blog.codinghorror.com/a-visual-explanation-of-sql-joins/
* With a join, you must specify how the table is joined using ON. Otherwise, you will get all the combinations possible of one table row matched with another table row.
  * **Inner Join** matches one table with another table row for row. If one row doesn’t have its pair on another table, it will be excluded. It will only show matching row pairs.
  * **Outer Join** matches two tables row for row but includes rows that are not paired up, aka rows that have a pair with a null in the other table.




## Requirements
Use the [Chinook Database](https://chinookdatabase.codeplex.com/) and the [DB Browser for SQLite](http://sqlitebrowser.org/) we downloaded in the ERD exercise.

For each of the following exercises, provide the appropriate query.

Answers:

1. Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.
  ```sql
  SELECT FirstName || " " || LastName AS Name,
         CustomerId,
         Country
  FROM   Customer
  WHERE  Country != "USA"
  ```
2. Provide a query only showing the Customers from Brazil.
  ```sql
  SELECT FirstName || " " || LastName AS Name, CustomerId, Country
  FROM Customer
  WHERE Country = "Brazil"
  ```
3. Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.
  ```sql
    SELECT FirstName || ' ' || LastName AS Name,
           InvoiceId,
           InvoiceDate,
           BillingCountry
    FROM   Invoice
    JOIN   Customer
    ON     Invoice.CustomerId = Customer.CustomerId
    WHERE  Country = 'Brazil'
  ```
4. Provide a query showing only the Employees who are Sales Agents.
  ```sql
  SELECT FirstName || " " || LastName AS Name, Title
  FROM Employee
  WHERE Title = "Sales Support Agent"
  ```
5. Provide a query showing a unique list of billing countries from the Invoice table.
  ```sql
  SELECT DISTINCT BillingCountry
  FROM      Invoice
  ORDER BY  BillingCountry
  ```
6. Provide a query showing the invoices of customers who are from Brazil.
   ```sql
   SELECT FirstName || ' ' || LastName AS Name,
          InvoiceId,
          InvoiceDate,
          BillingCountry
   FROM   Invoice
   JOIN   Customer
   ON     Invoice.CustomerId = Customer.CustomerId
   WHERE  Country = 'Brazil'

   ```
7. Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.
  ```sql
  SELECT Employee.FirstName || " " || Employee.LastName AS "Full Name", Invoice.* FROM Invoice
  JOIN Customer ON Invoice.CustomerId == Customer.CustomerId
  JOIN Employee ON Customer.SupportRepId == Employee.EmployeeId
  WHERE Employee.Title == "Sales Support Agent";
  ```
8. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.
  ```sql
  SELECT Customer.FirstName || " " || Customer.LastName, Invoice.Total, Customer.Country, Employee.FirstName || " " || Employee.LastName AS "Sales Agent" FROM Invoice
  JOIN Customer ON Invoice.CustomerId == Customer.CustomerId
  JOIN Employee ON Customer.SupportRepId == Employee.EmployeeId;
  ```
9. How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?
  ```sql
  SELECT COUNT(*) FROM Invoice
  WHERE strftime('%Y', InvoiceDate) = "2009" OR strftime('%Y', InvoiceDate) = "2011";
  ```
  ```sql
  SELECT SUM(Total) FROM Invoice
  WHERE strftime('%Y', InvoiceDate) = "2009";

  SELECT SUM(Total) FROM Invoice
  WHERE strftime('%Y', InvoiceDate) = "2011";
  ```
10. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.
  ```sql
  SELECT COUNT(*) FROM InvoiceLine
  WHERE InvoiceId = 37
  ```
11. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: [GROUP BY](http://www.sqlite.org/lang_select.html#resultset)
12. Provide a query that includes the track name with each invoice line item.
13. Provide a query that includes the purchased track name AND artist name with each invoice line item.
14. Provide a query that shows the # of invoices per country. HINT: [GROUP BY](http://www.sqlite.org/lang_select.html#resultset)
15. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be include on the resultant table.
16. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.
17. Provide a query that shows all Invoices but includes the # of invoice line items.
18. Provide a query that shows total sales made by each sales agent.
19. Which sales agent made the most in sales in 2009?
20. Which sales agent made the most in sales in 2010?
21. Which sales agent made the most in sales over all?
22. Provide a query that shows the # of customers assigned to each sales agent.
23. Provide a query that shows the total sales per country. Which country's customers spent the most?
24. Provide a query that shows the most purchased track of 2013.
25. Provide a query that shows the top 5 most purchased tracks over all.
26. Provide a query that shows the top 3 best selling artists.
27. Provide a query that shows the most purchased Media Type.

#### Other Resources
* http://www.sqlcourse.com/
* https://github.com/treehouse/cheatsheets/blob/master/sql_basics/cheatsheet.md
* [SQL Cheatsheet](https://zeroturnaround.com/wp-content/uploads/2016/06/RebelLabs-SQL-cheat-sheet.png)
* http://www.sqlite.org/lang_select.html
* https://www.sololearn.com/Course/SQL/
