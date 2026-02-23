
# 📚 Library Management System (SQL)

This project manages books, students, and issued books in a library. It includes tables, sample data, queries, indexes, views, and stored procedures.

---

## 🏷 Tables

```sql
-- Books table
CREATE TABLE Books (
    book_id INT PRIMARY KEY,
    book_name VARCHAR(100),
    author_name VARCHAR(100),
    total_copies INT,
    available_copies INT
);

-- Students table
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100),
    email_id VARCHAR(100),
    join_date DATE
);

-- Issued Books table
CREATE TABLE Issued_Books (
    issued_id INT PRIMARY KEY,
    student_id INT,
    book_id INT,
    issued_date DATE,
    due_date DATE,
    return_date DATE,
    status VARCHAR(20),
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (book_id) REFERENCES Books(book_id)
);
-- Sample data in Books
INSERT INTO Books (book_id, book_name, author_name, total_copies, available_copies) VALUES
(101, 'The Alchemist', 'Paulo Coelho', 5, 5),
(102, 'Harry Potter', 'J.K. Rowling', 10, 10),
(103, 'Think and Grow Rich', 'Napoleon Hill', 7, 7),
(104, 'Rich Dad Poor Dad', 'Robert Kiyosaki', 6, 6),
(105, 'Atomic Habits', 'James Clear', 8, 8);

-- Sample data in Students
INSERT INTO Students (student_id, student_name, email_id, join_date) VALUES
(201, 'Alice Johnson', 'alice@gmail.com', '2026-01-10'),
(202, 'Bob Smith', 'bob@gmail.com', '2026-01-12'),
(203, 'Charlie Brown', 'charlie@gmail.com', '2026-01-15');

-- Sample data in Issued Books
INSERT INTO Issued_Books (issued_id, student_id, book_id, issued_date, due_date, return_date, status) VALUES
(301, 201, 101, '2026-02-01', '2026-02-10', NULL, 'issued'),
(302, 202, 102, '2026-02-02', '2026-02-11', '2026-02-10', 'returned'),
(303, 203, 103, '2026-02-03', '2026-02-12', '2026-02-15', 'fine');

-- 1. Show issued books
SELECT book_name AS issued_books
FROM books
WHERE book_id IN (SELECT book_id FROM issued_books);

-- 2. Calculate fines (2 rupees per day)
SELECT b.book_name AS overdue_books,
       DATEDIFF(i.return_date, i.due_date) * 2 AS fine
FROM books b
JOIN issued_books i ON b.book_id = i.book_id
WHERE i.return_date > i.due_date;

-- 3. Most issued book
SELECT b.book_name, COUNT(i.book_id) AS count
FROM issued_books i
JOIN books b ON b.book_id = i.book_id
GROUP BY i.book_id
ORDER BY COUNT(i.book_id) DESC
LIMIT 1;

-- Create index on book_name
CREATE INDEX index_book_name ON books(book_name);
-- Books in the library
SELECT book_name FROM books;

-- View on current issued books
CREATE  VIEW current_issued_books AS
SELECT s.student_name, i.book_id, i.issued_id
FROM issued_books i
JOIN students s ON i.student_id = s.student_id
WHERE i.status='issued';

-- Test the view
SELECT * FROM current_issued_books;
-- Stored procedure to insert an issued book
DELIMITER //
CREATE PROCEDURE issued_book_procedure(
    IN p_issued_id INT,
    IN p_student_id INT,
    IN p_book_id INT,
    IN p_issued_date DATE,
    IN p_due_date DATE,
    IN p_return_date DATE,
    IN p_status VARCHAR(50)
)
BEGIN
    INSERT INTO issued_books(issued_id, student_id, book_id, issued_date, due_date, return_date, status)
    VALUES(p_issued_id, p_student_id, p_book_id, p_issued_date, p_due_date, p_return_date, p_status);
END //
DELIMITER ;

-- Call stored procedure example
CALL issued_book_procedure(304, 203, 105, '2026-09-12', '2026-09-27', NULL, 'issued');

-- Check Issued_Books table after procedure
SELECT * FROM issued_books;
