elif,else
for loop range and sequence types
x,*
group by
flow
can we use datatypes names as variables
// 
logical operators
why they are following in order
why we can't use top
if condition in queues
sep in tuples
printing 10,20,like that using slicing negative indexing
unpacking starred

why we dont use top except in displaying
taking characters from user in stack
string palindrome stack
#include <stdio.h>

#define MAX 100   // Maximum queue capacity

int queue[MAX];   // Array to store queue elements
int front = -1;   // Points to first element
int rear = -1;    // Points to last element
int size;         // Actual queue size entered by user

/* Function to insert element into queue */
void enqueue(int element)
{
    // Check for overflow condition
    if (rear == size - 1)
    {
        printf("Queue Overflow\n");
    }
    else
    {
        // If queue is empty, initialize front
        if (front == -1)
        {
            front = 0;
        }

        rear++;                    // Move rear forward
        queue[rear] = element;     // Insert element

        printf("Inserted element: %d\n", element);
    }
}

/* Function to delete element from queue */
void dequeue()
{
    // Check for underflow condition
    if (front == -1 || front > rear)
    {
        printf("Queue Underflow\n");
    }
    else
    {
        printf("Deleted element: %d\n", queue[front]);

        front++;   // Move front forward after deletion
    }
}

/* Function to display queue elements */
void display()
{
    int i;

    // Check if queue is empty
    if (front == -1 || front > rear)
    {
        printf("Queue Empty\n");
    }
    else
    {
        printf("Queue Elements: ");

        // Traverse from front to rear
        for (i = front; i <= rear; i++)
        {
            printf("%d ", queue[i]);
        }

        printf("\n");
    }
}

/* Function to search for an element */
void searchElement(int key)
{
    int i, found = 0;

    // Check if queue is empty
    if (front == -1 || front > rear)
    {
        printf("Queue Empty\n");
    }
    else
    {
        // Traverse queue to find key
        for (i = front; i <= rear; i++)
        {
            if (queue[i] == key)
            {
                printf("Element %d found at position %d\n", key, i + 1);
                found = 1;
                break;   // Stop after finding element
            }
        }

        // If element not found
        if (!found)
        {
            printf("Element Not Found\n");
        }
    }
}

int main()
{
    int choice, element, key;

    // Ask user for queue size
    printf("Enter Queue Size: ");
    scanf("%d", &size);

    do
    {
        // Display menu
        printf("\n--- Queue Menu ---\n");
        printf("1. Enqueue\n");
        printf("2. Dequeue\n");
        printf("3. Display\n");
        printf("4. Search\n");
        printf("5. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
        case 1:
            // Insert operation
            printf("Enter element to insert: ");
            scanf("%d", &element);
            enqueue(element);
            break;

        case 2:
            // Delete operation
            dequeue();
            break;

        case 3:
            // Display operation
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
