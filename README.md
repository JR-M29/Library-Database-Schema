# Library-Database-Schema


*Library Management Database Schema*

The following database schema captures key information for a library management system, including books, authors, publishers, borrowers, and loan transactions.

```
-- Create database
CREATE DATABASE LibraryManagement;

-- Use database
USE LibraryManagement;

-- Create tables
CREATE TABLE Authors (
    AuthorID INT AUTO_INCREMENT,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    BirthDate DATE,
    PRIMARY KEY (AuthorID)
);

CREATE TABLE Publishers (
    PublisherID INT AUTO_INCREMENT,
    PublisherName VARCHAR(100) NOT NULL,
    Address VARCHAR(200),
    PRIMARY KEY (PublisherID)
);

CREATE TABLE Books (
    BookID INT AUTO_INCREMENT,
    Title VARCHAR(200) NOT NULL,
    ISBN VARCHAR(20) UNIQUE NOT NULL,
    PublisherID INT,
    PublicationDate DATE,
    PRIMARY KEY (BookID),
    FOREIGN KEY (PublisherID) REFERENCES Publishers(PublisherID)
);

CREATE TABLE BookAuthors (
    BookID INT,
    AuthorID INT,
    PRIMARY KEY (BookID, AuthorID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID),
    FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID)
);

CREATE TABLE Borrowers (
    BorrowerID INT AUTO_INCREMENT,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    PRIMARY KEY (BorrowerID)
);

CREATE TABLE Loans (
    LoanID INT AUTO_INCREMENT,
    BookID INT,
    BorrowerID INT,
    LoanDate DATE NOT NULL,
    ReturnDate DATE,
    PRIMARY KEY (LoanID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID),
    FOREIGN KEY (BorrowerID) REFERENCES Borrowers(BorrowerID)
);

CREATE TABLE Fines (
    FineID INT AUTO_INCREMENT,
    LoanID INT,
    FineAmount DECIMAL(10, 2) NOT NULL,
    PaymentStatus VARCHAR(20) NOT NULL DEFAULT 'Unpaid',
    PRIMARY KEY (FineID),
    FOREIGN KEY (LoanID) REFERENCES Loans(LoanID)
);
```

This database schema includes the following entities and relationships:

1. *Authors*: stores information about book authors.
2. *Publishers*: stores information about book publishers.
3. *Books*: stores information about books, including the publisher.
4. *BookAuthors*: resolves the many-to-many relationship between books and authors.
5. *Borrowers*: stores information about library borrowers.
6. *Loans*: stores information about book loans, including the book and borrower.
7. *Fines*: stores information about fines associated with loans.

The relationships between these entities are established using foreign keys, ensuring data consistency and reducing redundancy.
