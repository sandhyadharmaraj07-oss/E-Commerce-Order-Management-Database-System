# Week 4: Order Management System & Database Normalization

USE ecommerce_db;

ALTER TABLE Order_Details
ADD Total_Price DECIMAL(10,2);
DESCRIBE Order_Details;

USE ecommerce_db;

SELECT * FROM Customer;

SELECT * FROM Product;

SELECT * FROM Orders;

SELECT * FROM Order_Details;

SELECT * FROM Category;
SELECT * FROM Supplier;

INSERT INTO Category
(Category_ID, Category_Name, Description)
VALUES
(1, 'Electronics', 'Electronic devices and accessories'),
(2, 'Home Appliances', 'Appliances for household use'),
(3, 'Fashion', 'Clothing and fashion products'),
(4, 'Books', 'Educational and general books');

SELECT * FROM Category;

INSERT INTO Supplier
(Supplier_ID, Supplier_Name, Contact_Name, Phone, Email, Address)
VALUES
(1, 'Tech World Suppliers', 'Arun Kumar', '9876543210', 'techworld@gmail.com', 'Chennai'),
(2, 'Home Needs Pvt Ltd', 'Priya Sharma', '9876543211', 'homeneeds@gmail.com', 'Bangalore'),
(3, 'Fashion Hub Suppliers', 'Rahul Singh', '9876543212', 'fashionhub@gmail.com', 'Mumbai');

SELECT * FROM Supplier;

INSERT INTO Product
(Product_ID, Product_Name, Description, Price, Stock_Quantity, Category_ID, Supplier_ID)
VALUES
(1, 'Laptop', 'HP Core i5 Laptop', 55000.00, 20, 1, 1),
(2, 'Wireless Mouse', 'Bluetooth Wireless Mouse', 800.00, 50, 1, 1),
(3, 'Mixer Grinder', '750W Mixer Grinder', 3500.00, 15, 2, 2),
(4, 'Smart Watch', 'Fitness Smart Watch', 4500.00, 25, 1, 1),
(5, 'Cotton Shirt', 'Men Cotton Casual Shirt', 1200.00, 40, 3, 3),
(6, 'Data Science Book', 'Introduction to Data Science', 900.00, 30, 4, 3);

SELECT * FROM Product;

USE ecommerce_db;

SHOW TABLES;
DESCRIBE Product;

INSERT INTO Customer
(Customer_ID, First_Name, Last_Name, Email, Phone, Address, City, State, Postal_Code)
VALUES
(1, 'Arun', 'Kumar', 'arun@gmail.com', '9876500001', '12 Anna Nagar', 'Chennai', 'Tamil Nadu', '600040'),
(2, 'Priya', 'Sharma', 'priya@gmail.com', '9876500002', '25 MG Road', 'Bangalore', 'Karnataka', '560001'),
(3, 'Rahul', 'Singh', 'rahul@gmail.com', '9876500003', '18 Andheri Road', 'Mumbai', 'Maharashtra', '400001'),
(4, 'Divya', 'Raj', 'divya@gmail.com', '9876500004', '10 Beach Road', 'Chennai', 'Tamil Nadu', '600001');

SELECT * FROM Customer;

INSERT INTO Orders
(Order_ID, Customer_ID, Order_Date, Order_Status, Total_Amount)
VALUES
(1001, 1, '2026-09-02', 'Pending', 55800.00),
(1002, 2, '2026-09-03', 'Confirmed', 5700.00),
(1003, 3, '2026-09-04', 'Delivered', 4500.00),
(1004, 1, '2026-09-05', 'Shipped', 2100.00),
(1005, 4, '2026-09-06', 'Pending', 900.00);

SELECT * FROM Orders;

INSERT INTO Order_Details
(Order_ID, Product_ID, Quantity, Unit_Price, Total_Price)
VALUES
(1001, 1, 1, 55000.00, 55000.00),
(1001, 2, 1, 800.00, 800.00),
(1002, 3, 1, 3500.00, 3500.00),
(1002, 2, 2, 800.00, 1600.00),
(1003, 4, 1, 4500.00, 4500.00),
(1004, 5, 1, 1200.00, 1200.00),
(1004, 2, 1, 800.00, 800.00),
(1005, 6, 1, 900.00, 900.00);

SELECT * FROM Order_Details;

SELECT * FROM Category;
SELECT * FROM Supplier;
SELECT * FROM Customer;
SELECT * FROM Product;
SELECT * FROM Orders;
SELECT * FROM Order_Details;

UPDATE Orders
SET Order_Status = 'Confirmed'
WHERE Order_ID = 1001;

SELECT * FROM Orders
WHERE Order_ID = 1001;

UPDATE Orders
SET Total_Amount = 1800.00
WHERE Order_ID = 1005;

SELECT * FROM Orders
WHERE Order_ID = 1005;

SELECT
    c.Customer_ID,
    CONCAT(c.First_Name, ' ', c.Last_Name) AS Customer_Name,
    o.Order_ID,
    o.Order_Date,
    o.Order_Status,
    p.Product_Name,
    od.Quantity,
    od.Unit_Price,
    od.Total_Price
FROM Customer c
JOIN Orders o
    ON c.Customer_ID = o.Customer_ID
JOIN Order_Details od
    ON o.Order_ID = od.Order_ID
JOIN Product p
    ON od.Product_ID = p.Product_ID
ORDER BY o.Order_Date DESC;

UPDATE Orders
SET Order_Status = 'Confirmed'
WHERE Order_ID = 1001;

SELECT * FROM Orders
WHERE Order_ID = 1001;

SELECT
    c.Customer_ID,
    CONCAT(c.First_Name, ' ', c.Last_Name) AS Customer_Name,
    o.Order_ID,
    o.Order_Date,
    o.Order_Status,
    p.Product_Name,
    od.Quantity,
    od.Unit_Price,
    od.Total_Price
FROM Customer c
JOIN Orders o
    ON c.Customer_ID = o.Customer_ID
JOIN Order_Details od
    ON o.Order_ID = od.Order_ID
JOIN Product p
    ON od.Product_ID = p.Product_ID
ORDER BY o.Order_Date DESC;

SELECT
    c.Customer_ID,
    CONCAT(c.First_Name, ' ', c.Last_Name) AS Customer_Name,
    COUNT(o.Order_ID) AS Total_Orders,
    SUM(o.Total_Amount) AS Total_Purchase
FROM Customer c
JOIN Orders o
    ON c.Customer_ID = o.Customer_ID
GROUP BY
    c.Customer_ID,
    c.First_Name,
    c.Last_Name
ORDER BY Total_Purchase DESC;

SELECT
    COUNT(Order_ID) AS Total_Orders,
    SUM(Total_Amount) AS Total_Sales
FROM Orders;

SELECT
    p.Product_Name,
    SUM(od.Quantity) AS Quantity_Sold,
    SUM(od.Total_Price) AS Revenue
FROM Product p
JOIN Order_Details od
    ON p.Product_ID = od.Product_ID
GROUP BY
    p.Product_ID,
    p.Product_Name
ORDER BY Revenue DESC;

SELECT
    Order_Status,
    COUNT(*) AS Number_of_Orders
FROM Orders
GROUP BY Order_Status;

SELECT
    Order_ID,
    Customer_ID,
    Order_Date,
    Order_Status,
    Total_Amount
FROM Orders
WHERE Total_Amount = (
    SELECT MAX(Total_Amount)
    FROM Orders
);

SELECT 
    c.Customer_ID,
    o.Order_ID,
    o.Order_Date,
    o.Order_Status,
    p.Product_Name,
    od.Quantity,
    od.Unit_Price,
    od.Total_Price
FROM Customer c
JOIN Orders o 
    ON c.Customer_ID = o.Customer_ID
JOIN Order_Details od 
    ON o.Order_ID = od.Order_ID
JOIN Product p 
    ON od.Product_ID = p.Product_ID
ORDER BY o.Order_Date DESC;

https://github.com/santhosh-v07/IMAGE-RES/blob/main/THUMBNAILS%20(1).jpg?raw=true
