# Database Normalization Assignment

## Overview
This project demonstrates the process of database normalization from an initial unnormalized form to First Normal Form (1NF) and Second Normal Form (2NF). The assignment involves creating and transforming a product order database to eliminate data redundancy and ensure proper dependencies.

## Files
- `database_normalization.sql`: SQL script containing table creation, data insertion, and normalization steps

## Database Schema

### Initial State (Unnormalized)
The initial data had a table where each order could contain multiple products in a single row, violating first normal form.

### First Normal Form (1NF)
Created the `ProductDetail_1NF` table where:
- Each cell contains atomic values
- No repeating groups of data
- Each record is unique

**Table Structure:**
```sql
CREATE TABLE ProductDetail_1NF (
    OrderID INT,
    CustomerName VARCHAR(100),
    Product VARCHAR(50)
);
```

### Second Normal Form (2NF)
Created two tables to achieve second normal form:

1. **Orders Table** (removes partial dependencies):
```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(100)
);
```

2. **OrderItems Table** (stores product details with composite key):
```sql
CREATE TABLE OrderItems (
    OrderID INT,
    Product VARCHAR(50),
    Quantity INT,
    PRIMARY KEY (OrderID, Product),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

## Normalization Process

### 1NF Achievement
- Separated composite product entries into individual rows
- Ensured each row contains atomic values
- Eliminated repeating groups

### 2NF Achievement
- Removed partial dependencies by separating order information from product information
- Created a relationship between Orders and OrderItems tables using foreign key
- Established proper composite primary key for OrderItems table

## Data Sample

### ProductDetail_1NF Table Contents:
| OrderID | CustomerName | Product   |
|---------|--------------|-----------|
| 101     | John Doe     | Laptop    |
| 101     | John Doe     | Mouse     |
| 102     | Jane Smith   | Tablet    |
| 102     | Jane Smith   | Keyboard  |
| 102     | Jane Smith   | Mouse     |
| 103     | Emily Clark  | Phone     |

### Orders Table Contents:
| OrderID | CustomerName |
|---------|--------------|
| 101     | John Doe     |
| 102     | Jane Smith   |
| 103     | Emily Clark  |

### OrderItems Table Contents:
| OrderID | Product   | Quantity |
|---------|-----------|----------|
| 101     | Laptop    | 2        |
| 101     | Mouse     | 1        |
| 102     | Tablet    | 3        |
| 102     | Keyboard  | 1        |
| 102     | Mouse     | 2        |
| 103     | Phone     | 1        |

## How to Use
1. Execute the SQL script in your preferred database management system
2. Verify the table structures and data integrity
3. Examine how the normalization process has eliminated redundancy
4. Note the foreign key relationship between Orders and OrderItems tables

## Benefits of This Normalization
- Reduced data redundancy
- Improved data integrity
- Elimination of update anomalies
- Better database structure for future expansion
- Proper relationship enforcement through foreign keys

## Further Improvements
This database could be further normalized to Third Normal Form (3NF) by:
- Creating a separate Customers table to remove transitive dependency
- Creating a Products table to store product information separately

## Author
Database normalization assignment demonstrating 1NF and 2NF principles.
