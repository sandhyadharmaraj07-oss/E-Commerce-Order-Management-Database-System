USE ecommerce_db;

CREATE TABLE Payment (
    Payment_ID INT PRIMARY KEY,
    Order_ID INT NOT NULL,
    Payment_Mode VARCHAR(30),
    Payment_Date DATE,
    Payment_Status VARCHAR(20),
    Amount DECIMAL(10,2),
    FOREIGN KEY (Order_ID) REFERENCES Orders(Order_ID)
);

USE ecommerce_db;

DESCRIBE Payment;

INSERT INTO Payment
(Payment_ID, Order_ID, Payment_Mode, Payment_Date, Payment_Status, Amount)
VALUES
(1, 1001, 'UPI', '2026-09-02', 'Successful', 55800.00),
(2, 1002, 'Credit Card', '2026-09-03', 'Successful', 5700.00),
(3, 1003, 'Debit Card', '2026-09-04', 'Successful', 4500.00),
(4, 1004, 'UPI', '2026-09-05', 'Failed', 2100.00),
(5, 1005, 'Cash', '2026-09-06', 'Successful', 900.00);

SELECT * FROM Payment;

SELECT *
FROM Payment
WHERE Payment_Status = 'Successful';

SELECT *
FROM Payment
WHERE Payment_Status = 'Failed';

UPDATE Payment
SET Payment_Status = 'Successful'
WHERE Payment_ID = 4;

SELECT * FROM Payment
WHERE Payment_ID = 4;

SELECT Payment_Mode, COUNT(*) AS Transactions

SELECT
    c.Customer_ID,
    CONCAT(c.First_Name, ' ', c.Last_Name) AS Customer_Name,
    p.Payment_ID,
    p.Order_ID,
    p.Payment_Mode,
    p.Payment_Date,
    p.Payment_Status,
    p.Amount
FROM Customer c
JOIN Orders o ON c.Customer_ID = o.Customer_ID
JOIN Payment p ON o.Order_ID = p.Order_ID
ORDER BY p.Payment_Date DESC;

SELECT Payment_Status, COUNT(*) AS Transactions,
       SUM(Amount) AS Total_Amount

