# Shopify-Fall-2022-Data-Science-Intern-Challenge-
Fall 2022 Data Science Intern Challenge 

DataSet: https://docs.google.com/spreadsheets/d/16i38oonuX1y1g7C_UAmiK9GkY7cS-64DfiDMNiR41LM/edit#gid=0

<Part 1>

A) Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 

The AOV of $3145.13 was calculated by calculating the mean of order_amount column. This is however not the best way as mean is sensitive to outliers such as order ID #17 where the order_amount is 704000 while the majority of the order_amount in the data set is nowhere near that.

B) What metric would you report for this dataset?

I would use the median over the mean because it isn't influenced by extremely large values.

C) What is its value?

$284.0

<Part 2>

Test out SQL statement: https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL

A) How many orders were shipped by Speedy Express in total?

SELECT Shippers.ShipperName, COUNT(Orders.ShipperID)
FROM Orders
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
WHERE Orders.ShipperID=1;

Speedy Express	54

B) What is the last name of the employee with the most orders?

SELECT Employees.LastName, COUNT(Orders.EmployeeID)
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY Orders.EmployeeID
ORDER BY COUNT(Orders.EmployeeID) DESC LIMIT 1;

Peacock	40

C) What product was ordered the most by customers in Germany?

SELECT Products.ProductName, COUNT(Products.ProductName)
FROM ((Customers
INNER JOIN Orders ON Customers.CustomerID= Orders.CustomerID)
INNER JOIN OrderDetails ON OrderDetails.OrderID = Orders.OrderID
INNER JOIN Products ON Products.ProductID = OrderDetails.ProductID)
WHERE Customers.Country = "Germany"
GROUP BY Products.ProductName
ORDER BY COUNT(Products.ProductName) DESC LIMIT 1;

Gorgonzola Telino	5
