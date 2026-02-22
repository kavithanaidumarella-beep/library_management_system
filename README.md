
    # Library Management System (SQL)

A SQL project to manage library books, students, and issued books.

## Tables

*Books*: book_id, book_name, author_name,  total_copies, available_copies  
*Students*: student_id,mail_id, student_name,   join_date  
*information*: issued_id, student_id (FK), book_id (FK), issued_date, due_date, return_date, status

## Queries

- Currently issued books.  
- Overdue books with fines.  
- Most issued book.

## Stored Procedures
- stored procedure to issue a book:
- issued_books_procedure(issued_id,student_id, book_id,issued_date,due_date,return_date,status)  
