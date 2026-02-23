# Library Management System (SQL, MySQL)

A SQL project to manage library books, students, and issued books using MySQL.

---

## ✅ Project Description

This project simulates a library management system. It manages;

- Books  
- Students  
- Issued books and returns  



## 📄 Tables

--books table

CREATE TABLE Books (
    book_id INT PRIMARY KEY,
    book_name VARCHAR(100),
    author_name VARCHAR(100),
    total_copies INT,
    available_copies INT
);

--students table(students who registered)
 
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100),
    email_id VARCHAR(100),
    join_date DATE
);

-- issued books table

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

--sample data in books table

INSERT INTO Books (book_id, book_name, author_name, total_copies, available_copies) VALUES
(101, 'The Alchemist', 'Paulo Coelho', 5, 5),
(102, 'Harry Potter', 'J.K. Rowling', 10, 10),
(103, 'Think and Grow Rich', 'Napoleon Hill', 7, 7),
(104, 'Rich Dad Poor Dad', 'Robert Kiyosaki', 6, 6),
(105, 'Atomic Habits', 'James Clear', 8, 8);

-- sample data in students table(who are registerd)

INSERT INTO Students (student_id, student_name, email_id, join_date) VALUES
(201, 'Alice Johnson', 'alice@gmail.com',  '2026-01-10'),
(202, 'Bob Smith', 'bob@gmail.com',  '2026-01-12'),
(203, 'Charlie Brown', 'charlie@gmail.com',  '2026-01-15');

--sample data in issued books table

INSERT INTO Issued_Books (issued_id, student_id, book_id, issued_date, due_date, return_date, status) VALUES
(301, 201, 101, '2026-02-01', '2026-02-10', NULL, 'issued'),
(302, 202, 102, '2026-02-02', '2026-02-11', '2026-02-10', 'returned'),
(303, 203, 103, '2026-02-03', '2026-02-12', '2026-02-15', 'fine');

--sample queries

--1.show issued books
select book_name as issued_books from books
where book_id in (select book_id from issued_books);

--2.calculating fines
-- fine per day is 2rupees
select b.book_name as overdue_books,DATEDIFF(i.return_date,i.due_date)*2 as fine from books b
join issued_books i on b.book_id=i.book_id
where i.return_date>i.due_date;
--3.finding most issued book
select b.book_name,count(i.book_id) as count from issued_books i
join books b on b.book_id=i.book_id
group by i.book_id order by count(i.book_id) desc limit 1;

--index

-- create index on book_name
create index index_book_name on books(book_name);
-- books in the library
select book_name from books;

-- view

-- view on current issued books
create view current_issued_books as
select s.student_name,i.book_id,i.issued_id  from issued_books i
join students s on i.student_id=s.student_id
where i.status='issued';
select *from current_issued_books;

--stored procedure

-- stored procedure to store an issued book in issued books table

delimiter //
create procedure issued_book_procedure(
IN p_issued_id int,
IN p_student_id int,
IN p_book_id int,
IN p_issued_date date,
IN p_due_date date,
IN p_return_date date,
IN p_status varchar(50)
)
begin
insert into issued_books values(p_issued_id,p_student_id,p_book_id,p_issued_date,p_due_date,p_return_date,p_status);
end
//
call issued_books_procedure(30,,203,105,'2025-09-12','2025-09-27',NULL,'issued');
select *from isssued_books;



