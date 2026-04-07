# Chapter 5: Relational Data Concepts

In addition to changing how we store data, the shift to cloud computing has enhanced how we interact with relational databases, one of computing's most enduring and vital technolgies.
Whether you're working with a traditional on-premises database or a fully managed cloud service like Azure SQL Database, understanding relational fundamentals is crucial.
For the DP-900 exam and for anyone working with data platforms, these concepts form the foundation of data management.
While this chapter introduces core database concepts, we'll focus primarly on practical understanding rather than technical implementation details.

**Coverage of Curriculum Objectives**

This chapter addresses the following DP-900 exam objectives:

- Understand core relational data features and relationships.
- Implement normalization principles effectively.
- Work with fundamental SQL statements.
- Understand essential database objects and their roles.

**EOCCO**

## Core Relational Concepts

In today's data landscape, we encounter both structured and unstructured data.
Structured data follows a predefined schema with consistent fields and data types--perfect for transactional systems and reporting.
Unstructured data, like images, videos, and documents, requires different storage approaches, often using Blob Storage or data lakes.
In AI applications, structured data feeds machine learning models with clean training data, while unstructured data undergoes processing through computer vision or natural language processing before analysis.
Understanding these differences helps determine the appropriate storage solution: relational databases for structured data, and object storage or NoSQL systems for unstructured content.

Despite the buzz around AI and NoSQL databases remain important. Why?
The answer lies in their unique ability to organize and manage structured data in a way that maintains consistency, reduces redundancy, and enables complex queries.
Traditional spreadsheets might work for simple data storage, but when organizations need to manage thousands or millions of records with complex relationships, relational databases become essential.

**Exam Tip**

The DP-900 exam emphasizes practical understanding of relational concepts rather than theoretical database design.
Focus on how these concepts apply in real-world scenarios.

**EOET**

Think about how a retail company manages its operations.
It needs to track products, customers, orders, and inventory--all interconnected pieces of information.
A relational database organizes this data efficiently:

- Prodcuts have prices, descriptions, and inventory levels.
- Customers have names, addresses, and order histories.
- Orders contain multiple products and belong to specific customers.
- Inventory tracks stock levels across different locations.

**Note**

Modern cloud platforms like Azure have streamlined how we work with relational databases, but the fundamental concepts remain unchanged.

**EON**

These fundamental relationships form the backbone of how relational databases operate.
To implement these relationships effectively, we need to understand the basic building blocks of relationships effectively, we need to understand the basic building blocks to relational databases, starting with their primary data structure: tables.

### Understanding Tables

At their core, relational databases store information in tables--structured collections of related data.
Unlike spreadsheets, which offer flexibility at the cost of consistency, database tables enforce strict rules about what kind of data can be stored and how it's organized.
Think of a table as a contract with your data: every piece of information must follow specific rules to maintain order and relability.

#### Columns and fields

Columns define the type of information that can be stored in a table.
Each column specifies both the kind of data (like numbers, text, or dates) and rules about what values are acceptable.
For instance, a `ProductID` column might require unique numbers, while a `ProductName` column stores text and cannot be left empty.
`Price` columns typically use decimal numbers and must contain positive values.
These specifications ensure that every piece of data fits the table's intended purpose.

#### Records and rows

While columns define the structure, rows contain the actual data.
Each row represents one complete record in the table.
For example, in a `products` table, a row might contain all the information about a single product: its ID number, name, price, and other details.
Every row must follow the rules defined by the column specifications.
A typical `products` table might contain rows like:

- Product #1001, "Cloud Database Basics", $29.99
- Product #1002, "Azure Fundamentals", $39.99

#### Primary keys

When a table needs a way to uniquely identify each row, you can use primary keys.
Often implemented as automatically generated number, through modern approaches (especially v7 and newer) increasingly use UUIDs, which offer additional possible values, sortability, and near-zero collision risk, primary keys ensure taht every record can be distinguished from all others.
Primary keys are constrained by both `UNIQUE` and `NOT NULL` properties, effectively making them uniqur identifers for any row.
Many databases support `AUTO_INCREMENT` functionality, which automatically generates sequential values for numeric primary keys.
Sometimes multiple columns work together to form a composite key.
Primary keys are essential for creating relationships between tables, allowing data to be connected across the database.

**Exam Tip**

The DP-900 exam frequently tests understanding of table structure and how different elements work together.
Focus on practical application rather than theoretical concepts.

To see these concepts in action, let's examine a basic example of an order management system in the figure below.
Before we do, however, it's important to undertand foreign keys. A *foreign key* is a column in one table that refrences the primary key of another table, creating a link between them.
For instance, an `Orders` table might have a `CustomerID` column that reference the primary key in the `Customers` table, establishing which customer placed each order

![Basic order manamgemt tables](image-6.png)

The system demostrtes how tables work together to create a complete business solution.
The `Customers` table stores customer information, with each row representing one customer's complete profile.
The `Orders` table tracks when customers place orders, linking to customer records through their unique identifers.
The `Products` table maintains product details independently, while the `OrderItems` table serves as a bridge, connecting orders with their products.

While table provide the structure for our data, we need two more elements to ensure data integrity: appropriate data types and constraints.
These rules act as guardians, ensuring that only valid information enters our database.

### Data Types and Constraints

When designing database tables, we need to specify what kind of information each column can hold and what rules it must follow.
These specifications form the foundation of data integrity in our database.

#### Basic data types

Every column in a database must have a specific data type that defines what kind of information it can store.
Think of these as specialized containers, each designed to hold particular kinds of data efficiently and safely.

*Numeric types* handle all forms of numbers.
Integer columns (INT) store whole numbers, perfect for IDs and counts, for example, `CustomerID INT` or `QuantityInStock INT`.
Decimal types like `DECIMAL (10,2)` manage precise financial calculations, ensuring accuracy in prices and totals.
Float types handle scientific calculations where precision requirements differ from financial calculations.

*Text types* manage character data with different size requirements. `CHAR` columns store fixed-length text, useful for codes and abbreviations that never vary in length, such as `CHAR(2)` for state codes.
`VARCHAR` columns effeciently handle variable-length text like names or descriptions, such as `VARCHAR(255)` for product names.
Text columns manage longer content such as product descriptions or comments.

*Date and time types* handle temporal data.
`DATE` columns store calandar dates like birthdates, and `DATETIME` columns combine both, perfect for tracking when orders are placed or when inventory changes occur.

**Exam Tip**

While Azure databases support many advanced data types, the DP-900 exam focuses on understanding basic types and their common uses.
Familiarity with `INT`, `VARCHAR`, `DATE`, and `DECIMAL` is sufficent for the exam--your don't need to know advanced or nuanced types.

**EOET**

#### Data rules with constraints

While data types specify what kind of information a column can hold, constraints define the rules that data must follow.
Think of constraints as guards that protect your data's integrity.

The `NOT NULL` constraint ensures that essential information is always present.
For example, every product needs a name, so the `ProductName` column would use this constraint to prevent empty values.

`UNIQUE` constraints prevent duplicate values where they don't make sense.
Customer email addresses must be unique to avoid confusion, while product codes need to be distinct to prevent inventory mix-ups.

`DEFAULT` contraints provide fallback values when none are specified.
When a customer places an order, the `OrderDate` can automatically default to the current date if not explicitly set.

**Beyond Types and Rules: Building Connections**

While data types and constraints help us managed individual pieces of information, real-world data rarely exists in isolation.
A customer's order connects to both the customer who placed it and the products they purchased. To represent these real-world connections, we need to understand how tables relate to each other through relationships and keys.

## Understanding Relationships and Keys

In a real-world database, information rarely exists in isolation.
Consider how a retail business operates: customer place orders, orders contain products, and products belong in categories.
These natural connections need to be represented in our database structure.
Understanding how to establish and maintain these relationships is fundamental to working with databases effectively.

** Exam Tip**

For the DP-900 exam, focus on indentifying and understanding basic relationship types rather than complex database design principles.

**EOET**

### Types of Table Relationships

Relational databases support three primary types of relationships, each serving a specific purpose in connecting related data.

#### One-to-one relationships

The simplest but least common relationship type occurs when each record in one table corresponds to exactly one record in another table.
Think of an employee and their passport information.
While you could store passport details in the `employee` table, separating them might make sense for security or organizational reasons.
In this case, each employee has exactly one passport record, and each passport record belongs to exactly one employee.

#### One-to-many relationships

The most common relationship type occurs when a record in one table can relate to multiple records in another table.
The classic example is customers and their orders.
A single customer can plave many orders over time, but each order belongs to exactly one customer.
This relationship naturally models many real-world scenarios, from departments having multiple employees to categories containing multiple products.

#### Many-to-many relationships

Sometimes records in both tables need to relate to multiple records in the other table.
Consider products and orders: one order typically contains multiple products, and each product can appear in many different orders.
This relationship requires a special junction table (sometimes called a *bridge* or *linking table*) to connect the two tables.
In our example, an `OrderItems` table would connect Products and Orders, tracking which products appear in which orders and in what quantities.

### Use of Foreign Keys to Establish Table Relationships

To implement these relationships in practice, databases use foreign keys to connect related records.
A foreign key in one table refrences the primary key of another table, creating a link between them.
For example:

- In the `Orders` table, a `CustomerID` foreign key references the `Customers` table's primary key, connecting each order to its customer.
- In the `OrderItems` table, both `OrderID` and `ProductID` foreign keys reference their respective tables, enabling the many-to-many relationship between orders and products.

**Exam Tip**

While you can use various column types as keys, the DP-900 exam focuses on simple numeric IDs for primary keys.

**EOET**

### A Practical Example

To understand how these relationships work in practice, let's explore a basic scenario: an online bookstore.
Consider how a bookstore needs to track customers, customer's orders, books, and book categories in the figure below

![Bookstore database relationships](image-7.png)

Our bookstore database demostrates several key relationship types working together:

When customers place orders, we create a one-to-many relationship between the `Customers` and `Orders` tables.
Each customer might order multiple times throughout the year, but every order belongs to exactly one customer.
The `CustomerID` foreign key in the `Orders` table makes the connection possible.

Books and categories share a more complex relationship.
A book like *Cloud Computing Basics* might belong in both the "Technology" and "Professional Development" categories, and these categories naturally contain many different books.
This many-to-many relationship comes to life through a junction table that tracks which books belong in which categories.

The practical example shows how relational databases mirror real-world business relationships.
But how do we actually work with this connected data? That's where SQL comes in.
SQL gives us the tools to extract meaningful information from our database, whether we need to find a customer's order history or generate a list of books in a specific category.

## Basic SQL Queries

While the cloud has transformed how we manage databases, SQL remains the primary way to interact with relational databases.
Think of SQL as a specialized language designed specifically for talking to databases--it allows you to ask questions about your data and make changes when needed.
In this section, we'll explore the fundamental SQL operations you need to understand for the DP-900 exam.

**SQL Language Categories**

SQL statements fall into three main categories:
    
    Data Manipulation Language (DML)
        Commands that work with data (`SELECT`,`INSERT`, `UPDATE`, `DELETE`)
    
    Data Definition Language (DDL)
        Commands that define database structure (`CREATE`, `ALTER`, `DROP`)

    Data Control Language (DCL)
        Commands that manage permissions (`GRANT`, `REVOKE`)

**EOSLC**

For the DP-900 exam, focus primarly on DML commands, which handle day-to-day data operations.

**Exam Tip**

The DP-900 exam tests basic SQL concepts rather than complex query writing.
Focus on understanding what each type of query does and when to use it.

### Retrieving Data with SELECT

Imagine you're managing a bookstore's database.
Every day, you need to answer questions like "What books do we have by Jane Smith?" or "Which books cost more than $50?"
The SELECT statement is how you ask these questions of your database.
It's the most fundamental and frequently used SQL operation, allowing you to retrieve and view your data in meaningful ways.

The basic structue of a `SELECT` statement has three main parts: the columns you want to see (`SELECT`), the table you want to look in (`FROM`), and any conditions that must be met (`WHERE`).
Here's the basic Syntax

```SQL

SELECT column1, column2
FROM TableName
WHERE condition;

```

Let's put this into practice with a real example.
Say a customer asks about Jane Smith's books.
You would write:

```SQL

SELECT Title, Price
FROM Books
WHERE Author = 'Jane Smith';

```

This query tells the database to look in the `Books` table, find all books where the author is Jane Smith, and show you the title and price of each one.
It's like asking a librarian to check the shelves for all books by a specific author and tell you their titles and prices.

#### Filtering with WHERE

The `WHERE` clause is your tool for filtering data, much like how you might filter your email inbox to see only messages from a specific sender.
It helps you narrow down large sets of data to just the information you need.
You can use various comparison operators to create these filters:

- Equal sign (`=`) for exact matches
- Greater than sign (`>`) or less than sign (`<`) for numerical comparisons
- Greater than or equal to sign (`>=`) or less than or equal to sign (`<=`) for range checks

For example, if you're planning a promotion for premium books, you might want to see all books priced over $50:

```SQL

SELECT Title, Price
FROM Books
WHERE Price > 50.00;

```

This query acts like a filter, showing you only the high-end books in your inventory.
Similarly, if you need to review recent orders for your monthly report, you could find all orders placed since the start of 2024:

```SQL

SELECT OrderID, OrderDate
FROM Orders
WHERE OrderDate >= `2024-01-01`;

```

This helps you focus on just the recent orders than sifting through your entire order history.

#### Sorting with ORDER BY

Data organization is crucial for analysis and reporting.
The `ORDER BY` clause helps you arrange your results in a meaningful sequence, must like how you might sort a spreadsheet by different columns.
You can sort in ascending order (A to Z, lowest to highest) or desending order (Z to A, highest to lowest).

For instance, you could use the following query if you're preparing a display of your most expensive books:

```SQL

SELECT Title, Price
FROM Books
ORDER BY Price DESC;

```

The query arranges books from highes to lowest price, perfect for identifying your premium inventory.
Sometimes you need to sort by multiple criteria, like when reviewing orders by date and amount:

```SQL

SELECT OrderID, OrderDate, TotalAmount
FROM Orders
ORDER BY OrderDate DESC, TotalAmount DESC;

```

This organization is particularly useful for financial reports, showing your most recent and highest value orders first, then organizing lower value orders within each date and amount:

**Exam Tip**

Pay attention to how different SQL clauses work together to filter and sort data.
Understanding their interaction is key to writing effective queries.

**EOET**

### Modifying Data

While retrieving data is important, databases need to be kept up-to-date as your business operates.
SQL provides three main ways to modify your data: adding new records (`INSERT`), changing existing records (`UPDATE`), and removing old records (`DELETE`).

#### Adding records with INSERT

When new books arrive at your store, you need to add them to your database.
The `INSERT` statement handles this task.
Think of it as filling out a form for each new book.
You specify which information (columns) you're providing and then give the actual values:

```SQL

INSERT INTO Books (Title, Author, Price)
VALUES ('Azure Data Fundamentals', 'Michael John Pena', 59.99);

```

This is like creating a new catalog entry for a single book.
But what if you recieve a shipment of multiple books?
SQL allows you to add several records at once, saving time and effort:

```SQL

INSERT INTO Books (Title, Author, Price)
VALUES
    ('Azure Data Fundamentals', 'Michael John Pena', 59.99);
    ('Azure Cosmos DB Designs and Practices', 'Mike Johnson', 49.99);

```

This bulk insert is particularly useful during inventory updates or when importing data from another system.

#### Modifying records with UPDATE

Prices change, errors need to be corrected, and information needs to be updated.
These are all situations where the `UPDATE` statement comes into play.
Think of `UPDATE` as editing an existing record in your database.
It's crucial to be precise about which records you want to change, which is why the `WHERE` clause is so important here.

For example, to update the price of a specific book

```SQL

UPDATE Books
SET Price = 34.99
WHERE BookID = 1001

```

The `WHERE` clause ensures that you only change the intended book's price.
You can also make broader changes, like applying a storewide discount to all premium books:

```SQL

UPDATE Books
SET Price = Price * 0.9
WHERE Price > 50.00;

```

This automatically calcualated and applies a 10% discount to all books currently priced over $50, saving you from having to update each price manually.

#### Removing records with DELETE

Over time, databases can accumulate outdated or unnecessary records.
The `DELETE` statement helps you clean up your database by removing records you no longer need. 
However, because deletion is permanent, it's crucial to be extremely careful with your `WHERE` clause to ensure that you only remove the intended records.

The following code removes a specific order that was canceled:

```SQL

DELETE FROM Orders
WHERE OrderID = 5001;

```

You might also need to perform routine cleanup, like removing old orders to maintain system performance:

```SQL

DELETE FROM Orders
WHERE OrderDate < '2023-01-01';

```

This removes all order from 2022 and earlier but keeps your recent order history intact.
Always double-check your `WHERE` clause before executing a `DELETE` statement, as recovering deleted data can be difficult or impossible.

#### Visualizing your SQL operations

The SQL operations we've covered--`SELECT`, `INSERT`, `UPDATE` and `DELETE`-- form the basic building blocks for interacting with your database.
Each operation follows a specific pattern, making them systematic and predictable once you understand their structure.

Figure below illustrates the decision flow for each SQL operation.
Starting from the top, you first choose which operation you need based on your goal:

- If you need to view data, the `SELECT` path guides you through choosing columns, selecting your table, adding any filtering conditions, and finally sorting your results.
- To add new data, the `INSERT` path shows that you'll need to specify your target table, list the columns, and provide the values.
- When changing existing data, the `UPDATE` path leads you throug specifying the table, setting new values, and adding conditions to identify which records to update.
- For removing data, the `DELETE` path demonstrates the importance of specifying both the table and the `WHERE` clause to identify which records to remove.

![Common SQL operations](image-8.png)

So far, we've worked with single tables in our examples.
However, most real databases store related information across multiple tables.
To get a complete picture of your data, you'll often need to combine information from different tables, and that's where `JOIN` operations comes in.

### Joining Tables

Most production-running databases store related information across multiple tables.
This separation of data is intentional: it helps maintain data integrity and reduces redundancy.
For example, instead of storing a customer's complete information with every order they make, we store customer details once in a `Customers` table and link it to multiple orders in an `Orders` table.

To get a complete picture of your data spread across these tables, you need `JOIN` operations.
The most common types include:

`INNER JOIN`
    Returns only matching records from both tables.

`LEFT JOIN`
    Returns all records from the left table, plus matches from the right.

`RIGHT JOIN`
    Returns all records from the right table, plus matches from the left.

`FULL OUTER JOIN`
    Returns all records from both tables.
    For example, an `INNER JOIN` between Orders and Customers shows only orders with valid customers, while a `LEFT JOIN` would show all orders even if customer data is missing.

Think of `JOIN` as a way to temporarily combine tables based on their relationships.
For instance, when processing orders, you might want to see both order details and customer information in a single view.

Here's how you can combine order and customer information:

```SQL

SELECT Orders.OrderID, Customers.Name, Orders.OrderDate
FROM Orders
JOIN Customers ON Orders.CustomerID = Customers.CustomerID;

```

This query connects each order with its corresponding customer using the `CustomerID` that's common to both tables.
The result gives you a comprehensive view showing the order ID, the customer's name, and when they placed the order-- information that orginally lived in seperate tables.

