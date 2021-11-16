# Basic Mysql Queries

### _`1. Select Queries Examples`_
```
> SELECT * FROM table_name;

> SELECT CustomerName, City FROM Customers;

> SELECT DISTINCT Country FROM Customers;

> SELECT COUNT(DISTINCT Country) FROM Customers;
```

### _`2. Where Queries Examples`_
```
> SELECT * FROM Customers WHERE Country='Mexico';
```

### _`3. AND, OR, NOT Queries Examples`_
```
> SELECT * FROM Customers WHERE Country='Germany' AND City='Berlin';

> SELECT * FROM Customers WHERE Country='Germany' OR Country='Spain';

> SELECT * FROM Customers WHERE NOT Country='Germany';

> SELECT * FROM Customers WHERE Country='Germany' AND (City='Berlin' OR City='München');

> SELECT * FROM Customers WHERE NOT Country='Germany' AND NOT Country='USA';
```

### _`4. OREDER BY Queries Examples`_
```	
> SELECT * FROM Customers ORDER BY Country DESC;

> SELECT * FROM Customers ORDER BY Country, CustomerName;

> SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC;
```

### _`5. INSERT INTO Queries Examples`_
```
> INSERT INTO Customers (CustomerName, ContactName, Address) VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21');

> INSERT INTO Customers (CustomerName, City, Country) VALUES ('Cardinal', 'Stavanger', 'Norway');
```

### _`6. NULL Values Queries Examples`_
```
> SELECT CustomerName, ContactName, Address FROM Customers WHERE Address IS NULL;

> SELECT CustomerName, ContactName, Address FROM Customers WHERE Address IS NOT NULL;
```

### _`7. UPDATE Queries Examples`_
```
> UPDATE Customers SET ContactName = 'Alfred Schmidt', City= 'Frankfurt' WHERE CustomerID = 1;

> UPDATE Customers SET ContactName='Juan' WHERE Country='Mexico';

> UPDATE Customers SET ContactName='Juan';
```

### _`8. DELETE Queries Examples`_
```	
> DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';

> DELETE FROM table_name;

> DELETE FROM Customers;
```

### _`9. MIN & MAX Queries Examples`_
```	
> SELECT MIN(Price) AS SmallestPrice FROM Products;

> SELECT MAX(Price) AS LargestPrice FROM Products;
```

### _`10. COUNT, AVG, SUM Queries Examples`_
```
> SELECT COUNT(ProductID) FROM Products;

> SELECT AVG(Price) FROM Products; [Note: NULL values are ignored.]

> SELECT SUM(Quantity) FROM OrderDetails;
```

### _`11. LIKE Queries Examples`_
```	
> SELECT * FROM Customers WHERE CustomerName LIKE 'a%';

> SELECT * FROM Customers WHERE CustomerName LIKE '%a';

> SELECT * FROM Customers WHERE CustomerName LIKE '%or%';

> SELECT * FROM Customers WHERE CustomerName LIKE '_r%';

> SELECT * FROM Customers WHERE CustomerName LIKE 'a__%';

> SELECT * FROM Customers WHERE ContactName LIKE 'a%o';
```

### _`12. IN Queries Examples`_
```
> SELECT * FROM Customers WHERE Country IN ('Germany', 'France', 'UK');

> SELECT * FROM Customers WHERE Country NOT IN ('Germany', 'France', 'UK');

> SELECT * FROM Customers WHERE Country IN (SELECT Country FROM Suppliers);
```

### _`13. BETWEEN Queries Examples`_
```	
> SELECT * FROM Products WHERE Price BETWEEN 10 AND 20;

> SELECT * FROM Products WHERE Price NOT BETWEEN 10 AND 20;

> SELECT * FROM Products WHERE Price BETWEEN 10 AND 20 AND CategoryID NOT IN (1,2,3);

> SELECT * FROM Products WHERE ProductName BETWEEN 'Tigers' AND 'Mozzarella di Giovanni' ORDER BY ProductName;

> SELECT * FROM Products WHERE ProductName BETWEEN "Tigers" AND "Chef Anton's Cajun Seasoning" ORDER BY ProductName;

> SELECT * FROM Products WHERE ProductName NOT BETWEEN 'Carnarvon' AND 'di Giovanni' ORDER BY ProductName;

> SELECT * FROM Orders WHERE OrderDate BETWEEN #07/01/1996# AND #07/31/1996#;

> SELECT * FROM Orders WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';
```

### _`14. ALIAS Queries Examples`_
```
> SELECT CustomerID AS ID, CustomerName AS Customer FROM Customers;

> SELECT CustomerName AS Customer, ContactName AS [Contact Person] FROM Customers;

> SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address FROM Customers;

> SELECT CustomerName, CONCAT(Address,', ',PostalCode,', ',City,', ',Country) AS Address FROM Customers;

> SELECT o.OrderID, o.OrderDate, c.CustomerName FROM Customers AS c, Orders AS o WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;
```

### _`15. INNER JOIN Queries Examples`_
```
> SELECT Orders.OrderID, Customers.CustomerName FROM Orders INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;

> SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName FROM ((Orders INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID) INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);
```

### _`16. LEFT JOIN Queries Examples`_
```
> SELECT Customers.CustomerName, Orders.OrderID FROM Customers LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID ORDER BY Customers.CustomerName;
```

### _`17. RIGHT JOIN Queries Examples`_
```
> SELECT Orders.OrderID, Employees.LastName, Employees.FirstName FROM Orders RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID ORDER BY Orders.OrderID;
```

### _`18. FULL OUTER JOIN Queries Examples`_
```	
> SELECT Customers.CustomerName, Orders.OrderID FROM Customers FULL OUTER JOIN Orders ON Customers.CustomerID=Orders.CustomerID ORDER BY Customers.CustomerName;
```

### _`19. SELF JOIN Queries Examples`_
```	
> SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City FROM Customers A, Customers B WHERE A.CustomerID <> B.CustomerID AND A.City = B.City ORDER BY A.City;
```

### _`20. UNION Operator Queries Examples`_
```	
> SELECT City FROM Customers UNION SELECT City FROM Suppliers ORDER BY City;

> SELECT City FROM Customers UNION ALL SELECT City FROM Suppliers ORDER BY City;

> SELECT City, Country FROM Customers WHERE Country='Germany' UNION SELECT City, Country FROM Suppliers WHERE Country='Germany' ORDER BY City;

> SELECT City, Country FROM Customers WHERE Country='Germany' UNION ALL SELECT City, Country FROM Suppliers WHERE Country='Germany' ORDER BY City;

> SELECT 'Customer' AS Type, ContactName, City, Country FROM Customers UNION SELECT 'Supplier', ContactName, City, Country FROM Suppliers;
```

### _`21. GROUP BY Queries Examples`_
```
> SELECT COUNT(CustomerID), Country FROM Customers GROUP BY Country;

> SELECT COUNT(CustomerID), Country FROM Customers GROUP BY Country ORDER BY COUNT(CustomerID) DESC;

> SELECT Shippers.ShipperName, COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID GROUP BY ShipperName;
```

### _`22. HAVING Clause Queries Examples`_
```	
> SELECT COUNT(CustomerID), Country FROM Customers GROUP BY Country HAVING COUNT(CustomerID) > 5;

> SELECT COUNT(CustomerID), Country FROM Customers GROUP BY Country HAVING COUNT(CustomerID) > 5 ORDER BY COUNT(CustomerID) DESC;

> SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders FROM (Orders INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID) GROUP BY LastName HAVING COUNT(Orders.OrderID) > 10;

> SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID WHERE LastName = 'Davolio' OR LastName = 'Fuller' GROUP BY LastName HAVING COUNT(Orders.OrderID) > 25;
```

### _`23. EXISTS Queries Examples`_
```
> SELECT SupplierName FROM Suppliers WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);

> SELECT SupplierName FROM Suppliers WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price = 22);
```

### _`24. CREATE DATABASE Queries Examples`_
```
> CREATE DATABASE databasename;
```

### _`25. DROP DATABASE Queries Examples`_
```
> DROP DATABASE databasename;
```

### _`26. DROP TABLE Queries Examples`_
```	
> DROP TABLE table_name;
