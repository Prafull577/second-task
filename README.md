-- 1. Create tables for LibraryDB
CREATE TABLE Books (
    BookID INTEGER PRIMARY KEY AUTOINCREMENT,
    Title TEXT NOT NULL,
    Author TEXT,
    Genre TEXT,
    YearPublished INTEGER,
    CopiesAvailable INTEGER
);

CREATE TABLE Members (
    MemberID INTEGER PRIMARY KEY AUTOINCREMENT,
    Name TEXT NOT NULL,
    JoinDate DATE,
    MembershipType TEXT
);

CREATE TABLE Loans (
    LoanID INTEGER PRIMARY KEY AUTOINCREMENT,
    BookID INTEGER,
    MemberID INTEGER,
    LoanDate DATE,
    ReturnDate DATE,
    FOREIGN KEY (BookID) REFERENCES Books(BookID),
    FOREIGN KEY (MemberID) REFERENCES Members(MemberID)
);

-- 2. Insert sample data into Books
INSERT INTO Books (Title, Author, Genre, YearPublished, CopiesAvailable) VALUES
('To Kill a Mockingbird', 'Harper Lee', 'Fiction', 1960, 4),
('1984', 'George Orwell', 'Dystopian', 1949, 2),
('The Great Gatsby', 'F. Scott Fitzgerald', 'Classic', 1925, 5),
('Harry Potter and the Sorcerer''s Stone', 'J.K. Rowling', 'Fantasy', 1997, 3),
('The Hobbit', 'J.R.R. Tolkien', 'Fantasy', 1937, 6);

-- 3. Insert sample data into Members
INSERT INTO Members (Name, JoinDate, MembershipType) VALUES
('Alice Johnson', '2024-01-15', 'Standard'),
('Bob Smith', '2023-11-20', 'Premium'),
('Charlie Brown', '2024-03-10', 'Standard');

-- 4. Insert sample data into Loans
INSERT INTO Loans (BookID, MemberID, LoanDate, ReturnDate) VALUES
(1, 1, '2024-07-01', '2024-07-15'),
(2, 2, '2024-07-05', NULL),
(4, 3, '2024-07-10', '2024-07-20');

-- 5. SELECT Queries

-- a) Select all books
SELECT * FROM Books;

-- b) Select specific columns
SELECT Title, Author FROM Books;

-- c) Books with fewer than 4 copies available
SELECT * FROM Books
WHERE CopiesAvailable < 4;

-- d) Fantasy books published after 1950
SELECT * FROM Books
WHERE Genre = 'Fantasy' AND YearPublished > 1950;

-- e) Books with title containing 'The'
SELECT * FROM Books
WHERE Title LIKE '%The%';

-- f) Sort members by join date (newest first)
SELECT * FROM Members
ORDER BY JoinDate DESC;

-- g) Get top 2 oldest books in the library
SELECT * FROM Books
ORDER BY YearPublished ASC
LIMIT 2;

-- h) Members who borrowed books and haven't returned yet
SELECT m.Name, b.Title, l.LoanDate
FROM Loans l
JOIN Members m ON l.MemberID = m.MemberID
JOIN Books b ON l.BookID = b.BookID
WHERE l.ReturnDate IS NULL;

