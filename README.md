
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
  ## screenshots
  ![Books Table](screenshots/books_table.png)
  ![Students Table](screenshots/students_table.png)
  ![ Issued Books table](screenshots/issued_books_table.png)
  ![Issued Books](screenshots/issued_books.png)
  ![Fines](screenshots/overdue_and_fines.png)
  ![Most Issued Book](screenshots/most_issued_book.png)
  ![Index](screenshots/index_on_book_name.png)
  ![Views](screenshots/view.png)
  ![Stored Procedures](screenshots/stored_procedure.png)

