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


<img width="1917" height="1035" alt="Screenshot 2026-09-29 111357" src="https://github.com/user-attachments/assets/1ab84132-aa51-409f-a7c2-d5930f2432f0" />

<img width="1917" height="1040" alt="Screenshot 2026-09-29 111409" src="https://github.com/user-attachments/assets/837daef4-d296-4490-abae-2bf5f3f55c99" />

<img width="1917" height="1037" alt="Screenshot 2026-09-29 111518" src="https://github.com/user-attachments/assets/3afef71c-ca8c-44fa-af6d-195fdeff13de" />

<img width="1917" height="1030" alt="Screenshot 2026-09-29 111558" src="https://github.com/user-attachments/assets/c48e6d03-0378-4478-85bd-0f9393f93bcd" />

<img width="1917" height="1028" alt="Screenshot 2026-09-29 111631" src="https://github.com/user-attachments/assets/bd5df400-fa6f-4922-9be3-dbbd9babf570" />

<img width="1917" height="1027" alt="Screenshot 2026-09-29 111743" src="https://github.com/user-attachments/assets/93e636ae-2031-448a-b686-5dfec7ce55ba" />

<img width="1917" height="761" alt="Screenshot 2026-09-29 111812" src="https://github.com/user-attachments/assets/5d202a81-b324-44f0-91a2-78bd454c9fe0" />

<img width="1917" height="790" alt="Screenshot 2026-09-29 111823" src="https://github.com/user-attachments/assets/6ed038df-df95-453d-8d7b-1c8c6a939990" />

<img width="1917" height="1035" alt="Screenshot 2026-09-29 111927" src="https://github.com/user-attachments/assets/324ec424-9851-4b88-9644-1487760f98b1" />

<img width="1917" height="1035" alt="Screenshot 2026-09-29 112007" src="https://github.com/user-attachments/assets/bef2875b-1112-4b2c-8509-89fafefbb02a" />


