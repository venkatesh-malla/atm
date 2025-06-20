# ATM Project

This is a Java-based ATM system that provides basic banking functionalities such as balance inquiry, deposit, withdrawal, fund transfer, and mini-statement. It also includes account creation and session management features.

## Features

- View account balance
- Deposit and withdraw cash
- Transfer funds to another account
- View transaction history (mini-statement)
- Create a new account
- Session timeout for security
- Secure PIN storage using SHA-256 hashing

## Project Structure

-ATM-Project/
│
├── src/                         # Source code directory
│   └── atm/                     # Package for all Java classes
│       ├── Main.java                # Entry point of the application
│       ├── atm.java                 # Interface for ATM operations
│       ├── atmoperation.java        # Implements ATM functionality (withdraw, deposit, etc.)
│       ├── userinterface.java       # Manages user interactions and session flow
│       ├── databaseconnection.java  # Handles database connection management
│       ├── accountmanagement.java   # Provides functionality for account creation
│       ├── sessionmanager.java      # Manages user session timeout logic
│       ├── securityutils.java       # Provides utilities for secure PIN hashing
│       └── testconnection.java      # Verifies database connectivity
│
├── scripts/                     # Database setup scripts
│   └── setup.sql                # SQL script to create tables and insert sample data
│
├── .gitignore                   # Specifies files and directories to be ignored by Git
├── README.md                    # Documentation file for the project
├── pom.xml                      # Maven configuration file (optional, for dependency management)
└── LICENSE                      # License file (optional, include if needed)


## Prerequisites

- Java Development Kit (JDK) 11 or higher
- MySQL Server
- JDBC Driver for MySQL

## Database Setup

1. Create a database named `atm_db`.
2. Create the following tables:
   ```sql
   CREATE DATABASE IF NOT EXISTS atm_db;
   USE atm_db;

   CREATE TABLE users (
       account_number INT PRIMARY KEY,
       pin VARCHAR(64) NOT NULL,
       balance DOUBLE DEFAULT 0.0,
       failed_attempts INT DEFAULT 0
   );

   CREATE TABLE transactions (
       transaction_id INT AUTO_INCREMENT PRIMARY KEY,
       account_number INT,
       type VARCHAR(20),
       amount DOUBLE,
       date_time DATETIME,
       ip_address VARCHAR(15),
       FOREIGN KEY (account_number) REFERENCES users(account_number)
   );
