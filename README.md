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
    WHERE user_id IN (SELECT user_id FROM security_logs WHERE event_type     = 'Failed Login');

### Pattern Matching with LIKE
Use `LIKE` for pattern matching in SQL to identify specific patterns in your data.

    -- Find usernames starting with 'admin'
    SELECT * FROM user_information
    WHERE username LIKE 'admin%';

### Time-based Analysis
Analyze security events based on specific time frames.

    -- Count security events per hour
    SELECT DATE_TRUNC('hour', timestamp) AS hour, COUNT(*) AS event_count
    FROM security_logs
    GROUP BY hour
    ORDER BY hour;


## Sample Scenarios and Queries

### Scenario One: Investigating Suspicious Activity
Query to find users with multiple failed login attempts:

    SELECT user_id, COUNT(*) AS failed_login_attempts
    FROM security_logs
    WHERE event_type = 'Failed Login'
    GROUP BY user_id
    HAVING failed_login_attempts > 3;

### Scenario Two: Identifying Traffic Anomalies
Query to identify anomalies in network traffic:

    SELECT source_ip, destination_ip, COUNT(*) AS traffic_count
    FROM network_logs
    GROUP BY source_ip, destination_ip
    HAVING traffic_count > 100;

### Scenario Three: User Account Lockouts
Query to identify user accounts with multiple lockouts, which may indicate a potential security threat.

    -- Find user accounts with multiple lockouts
    SELECT user_id, COUNT(*) AS lockout_count
    FROM security_logs
    WHERE event_type = 'Account Lockout'
    GROUP BY user_id
    HAVING lockout_count > 3;

### Scenario Four: Unusual Access Times
Query to identify user logins during unusual hours, helping to detect potentially unauthorized access.

    -- Find user logins during unusual hours
    SELECT user_id, timestamp
    FROM security_logs
    WHERE event_type = 'Successful Login'
    AND EXTRACT(HOUR FROM timestamp) NOT BETWEEN 9 AND 17; -- Assuming 9 AM to 5 PM are regular working hours

## Resources for Further Learning

- [SQL Tutorial by W3Schools](https://www.w3schools.com/sql/)
- [SQL for Web Developers - MDN](https://developer.mozilla.org/en-US/docs/Learn/Server-side/SQL)
- [Coursera: SQL for Data Science](https://www.coursera.org/learn/sql-for-data-science)
- [MySQL Tutorial for Beginners](https://www.youtube.com/watch?v=7S_tz1z_5bA)


Feel free to explore these examples and scenarios to enhance your SQL skills for security analysis. <br>
Happy querying!
