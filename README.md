# SQL for SOC Analysts

## Introduction
SQL (Structured Query Language) is a fundamental skill for SOC (Security Operations Center) Analysts. This guide aims to provide an in-depth understanding of SQL and its application in security analysis.

## Overview of SQL
SQL is a domain-specific language used to manage and manipulate relational databases. It allows analysts to interact with databases, retrieve data, and perform various operations.

## Importance in SOC Roles
SOC Analysts often use SQL to query and analyze security data stored in databases. Understanding SQL is crucial for:
- Investigating security incidents.
- Analyzing log data.
- Correlating information for threat detection.
- Generating reports for management.

## Basic SQL Queries

### SELECT Statement
The `SELECT` statement is used to retrieve data from a database.

    -- Select all columns from a table
    SELECT * FROM security_logs;

    -- Select specific columns
    SELECT timestamp, source_ip, destination_ip FROM security_logs


### WHERE Clause
The`WHERE` clause filters data based on specified conditions.

    -- Filter data based on a condition
    SELECT * FROM security_logs WHERE event_type = 'Unauthorized Access';

### ORDER BY Clause
The `ORDER BY` clause sorts the result set.

    -- Order data by timestamp in descending order
    SELECT * FROM security_logs ORDER BY timestamp DESC;

## SQL for Security Analysis

### JOIN Operations
Use `JOIN` to combine rows from two or more tables.

    -- Inner Join
    SELECT * FROM security_logs
    INNER JOIN user_information ON security_logs.user_id = user_information.user_id;

### Subqueries
Subqueries allow nesting one query inside another.

    -- Find users with multiple failed login attempts
    SELECT * FROM user_information
    WHERE user_id IN (SELECT user_id FROM security_logs WHERE event_type = 'Failed Login');

### Aggregation Functions
Aggregate functions perform a calculation on a set of values.

    -- Calculate the number of security events per user
    SELECT user_id, COUNT(*) AS event_count
    FROM security_logs
    GROUP BY user_id;


