
# 📚 Online Bookstore SQL Project

This project simulates the backend of an **Online Bookstore** using SQL. It includes creating a relational database, importing data from CSVs, and performing **basic to advanced SQL queries** to extract insights about books, customers, and orders.

---

## 🎯 Objective

- Design a relational database for an online bookstore.
- Import customer, book, and order data using SQL.
- Perform queries to analyze sales, customer behavior, and inventory.
- Build hands-on experience with real-world SQL use cases.

---

## 🧠 Motive

The aim is to:
- Understand how SQL manages structured data in commerce scenarios.
- Practice writing optimized queries using `JOIN`, `GROUP BY`, `HAVING`, and subqueries.
- Use SQL as a tool to uncover business insights from relational data.

---

## 🧱 Database Structure

### Tables Created:
1. **Books**
   - `Book_ID`, `Title`, `Author`, `Genre`, `Published_Year`, `Price`, `Stock`
2. **Customers**
   - `Customer_ID`, `Name`, `Email`, `Phone`, `City`, `Country`
3. **Orders**
   - `Order_ID`, `Customer_ID`, `Book_ID`, `Order_Date`, `Quantity`, `Total_Amount`

---

## 📦 Data Import

```sql
-- Import Data into Books Table
COPY Books(Book_ID, Title, Author, Genre, Published_Year, Price, Stock) 
FROM 'Books.csv' 
CSV HEADER;

-- Import Data into Customers Table
COPY Customers(Customer_ID, Name, Email, Phone, City, Country) 
FROM 'Customers.csv' 
CSV HEADER;

-- Import Data into Orders Table
COPY Orders(Order_ID, Customer_ID, Book_ID, Order_Date, Quantity, Total_Amount) 
FROM 'Orders.csv' 
CSV HEADER;
````

---

## 🔍 SQL Queries Used

### 🔹 Basic Queries

```sql
-- 1. Retrieve all books in the "Fiction" genre:
SELECT * FROM Books 
WHERE Genre = 'Fiction';

-- 2. Find books published after the year 1950:
SELECT * FROM Books 
WHERE Published_Year > 1950;

-- 3. List all customers from Canada:
SELECT * FROM Customers 
WHERE Country = 'Canada';

-- 4. Show orders placed in November 2023:
SELECT * FROM Orders 
WHERE Order_Date BETWEEN '2023-11-01' AND '2023-11-30';

-- 5. Retrieve the total stock of books available:
SELECT SUM(Stock) AS Total_Stock
FROM Books;

-- 6. Find the details of the most expensive book:
SELECT * FROM Books 
ORDER BY Price DESC 
LIMIT 1;

-- 7. Show all customers who ordered more than 1 quantity of a book:
SELECT * FROM Orders 
WHERE Quantity > 1;

-- 8. Retrieve all orders where the total amount exceeds $20:
SELECT * FROM Orders 
WHERE Total_Amount > 20;

-- 9. List all genres available in the Books table:
SELECT DISTINCT Genre FROM Books;

-- 10. Find the book with the lowest stock:
SELECT * FROM Books 
ORDER BY Stock 
LIMIT 1;

-- 11. Calculate the total revenue generated from all orders:
SELECT SUM(Total_Amount) AS Revenue 
FROM Orders;
```

---

### 🔹 Advanced Queries

```sql
-- 1. Retrieve the total number of books sold for each genre:
SELECT b.Genre, SUM(o.Quantity) AS Total_Books_Sold
FROM Orders o
JOIN Books b ON o.Book_ID = b.Book_ID
GROUP BY b.Genre;

-- 2. Find the average price of books in the "Fantasy" genre:
SELECT AVG(Price) AS Average_Price
FROM Books
WHERE Genre = 'Fantasy';

-- 3. List customers who have placed at least 2 orders:
SELECT o.Customer_ID, c.Name, COUNT(o.Order_ID) AS Order_Count
FROM Orders o
JOIN Customers c ON o.Customer_ID = c.Customer_ID
GROUP BY o.Customer_ID, c.Name
HAVING COUNT(o.Order_ID) >= 2;

-- 4. Find the most frequently ordered book:
SELECT o.Book_ID, b.Title, COUNT(o.Order_ID) AS Order_Count
FROM Orders o
JOIN Books b ON o.Book_ID = b.Book_ID
GROUP BY o.Book_ID, b.Title
ORDER BY Order_Count DESC
LIMIT 1;

-- 5. Show the top 3 most expensive books of 'Fantasy' genre:
SELECT * FROM Books
WHERE Genre = 'Fantasy'
ORDER BY Price DESC 
LIMIT 3;

-- 6. Retrieve the total quantity of books sold by each author:
SELECT b.Author, SUM(o.Quantity) AS Total_Books_Sold
FROM Orders o
JOIN Books b ON o.Book_ID = b.Book_ID
GROUP BY b.Author;

-- 7. List the cities where customers who spent over $30 are located:
SELECT DISTINCT c.City, o.Total_Amount
FROM Orders o
JOIN Customers c ON o.Customer_ID = c.Customer_ID
WHERE o.Total_Amount > 30;

-- 8. Find the customer who spent the most on orders:
SELECT c.Customer_ID, c.Name, SUM(o.Total_Amount) AS Total_Spent
FROM Orders o
JOIN Customers c ON o.Customer_ID = c.Customer_ID
GROUP BY c.Customer_ID, c.Name
ORDER BY Total_Spent DESC
LIMIT 1;

-- 9. Calculate the stock remaining after fulfilling all orders:
SELECT b.Book_ID, b.Title, b.Stock, COALESCE(SUM(o.Quantity), 0) AS Order_Quantity,  
       b.Stock - COALESCE(SUM(o.Quantity), 0) AS Remaining_Quantity
FROM Books b
LEFT JOIN Orders o ON b.Book_ID = o.Book_ID
GROUP BY b.Book_ID 
ORDER BY b.Book_ID;
```

---

## 📊 Features of the Project

* End-to-end SQL workflow:

  * Create database and tables
  * Load real-world data
  * Run insightful queries
* Practice of core SQL concepts
* In-depth business insights from data
* Clean query formatting and logic

---

## 🔮 Future Prospects

* Create dashboards in **Power BI/Tableau** to visualize:

  * Revenue by genre/author
  * Monthly order trends
  * Stock analysis
* Create **stored procedures** for managing new orders.
* Build a **web app frontend** (HTML + Flask) connected to this SQL backend.
* Host the project in PostgreSQL and connect via Python for automation.

---

## 👨‍💻 Author

**Ankit Kumar**
🎓 B.Tech – Artificial Intelligence & Data Science
🏫 Truba Institute of Engineering & Information Technology
📍 Bhopal, Madhya Pradesh
🌐 \[Your LinkedIn/GitHub Profile Link Here]

---

## 📜 License

This project is licensed under the **MIT License** – feel free to use, modify, and share it with attribution.

---

## ⭐ Support

If you find this project useful, feel free to ⭐ star the repo and share your thoughts!


