# Apply Filters to SQL Queries

## Project Description
My organization is working to make its systems more secure. As a security analyst, my role is to investigate potential security issues and ensure that employee systems are properly updated and protected. In this project, I use SQL queries with filters to analyze login activity and employee information in order to identify suspicious behavior and support security-related decisions.

## Database Tables Overview
This project uses two tables from the organization’s database: log_in_attempts and employees.

The log_in_attempts table stores employee login activity and is used to detect suspicious behavior such as failed login attempts, after-hours access, and logins from unexpected locations. Its columns include event_id, username, login_date, login_time, country, ip_address, and success, where FALSE or 0 indicates a failed login attempt.

The employees table contains information about employees and their assigned devices. Its columns include employee_id, device_id, username, department, and office. This data is used to determine which employees require security updates.

## Retrieve After-Hours Failed Login Attempts
There was a potential security incident that occurred after business hours (after 18:00). All login attempts that failed after business hours needed to be investigated.

SQL query used:
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
AND success = 0;

Explanation:
The query selects all records from the log_in_attempts table. A WHERE clause with the AND operator is used to filter the results. The condition login_time > '18:00' filters for login attempts that occurred after business hours. The condition success = 0 filters for failed login attempts. Together, these conditions return only unsuccessful login attempts that occurred after 18:00.

Screenshot (optional):
screenshots/after_hours_failed_logins.png

## Retrieve Login Attempts on Specific Dates
A suspicious event occurred on 2022-05-09. All login activity from that date and the day before (2022-05-08) needed to be reviewed.

SQL query used:
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
OR login_date = '2022-05-08';

Explanation:
This query retrieves all login attempts that occurred on either 2022-05-09 or 2022-05-08. The OR operator allows the query to return records that match either of the specified dates, which is useful when investigating incidents spanning multiple days.

Screenshot (optional):
screenshots/specific_dates_logins.png

## Retrieve Login Attempts Outside of Mexico
After reviewing login activity, I determined that login attempts originating outside of Mexico required further investigation.

SQL query used:
SELECT *
FROM log_in_attempts
WHERE country NOT LIKE 'MEX%';

Explanation:
This query filters login attempts using NOT and LIKE. The pattern MEX% matches values such as MEX and MEXICO. Using NOT excludes those values and returns only login attempts that occurred outside of Mexico.

Screenshot (optional):
screenshots/outside_mexico_logins.png

## Retrieve Employees in Marketing
The organization needed to update machines for employees in the Marketing department who are located in offices within the East building.

SQL query used:
SELECT *
FROM employees
WHERE department = 'Marketing'
AND office LIKE 'East%';

Explanation:
This query retrieves employee records using a WHERE clause with the AND operator. The condition department = 'Marketing' filters for employees in the Marketing department. The condition office LIKE 'East%' filters for offices located in the East building. Both conditions must be true for a record to be returned.

## Retrieve Employees in Finance or Sales
The organization also needed to perform updates on computers used by employees in the Finance or Sales departments.

SQL query used:
SELECT *
FROM employees
WHERE department = 'Finance'
OR department = 'Sales';

Explanation:
This query uses the OR operator to retrieve employees who belong to either the Finance department or the Sales department.

## Retrieve All Employees Not in IT
Employees in the Information Technology department had already received a security update. All other employees still needed the update.

SQL query used:
SELECT *
FROM employees
WHERE department != 'Information Technology';

Explanation:
This query excludes employees in the Information Technology department using NOT logic. It returns all employees who are not part of IT and still require the security update.

## Instructions for Including SQL Queries
SQL queries were executed in a MariaDB shell during the Filter with AND, OR, and NOT lab. Screenshots, when included, show only the SQL terminal and a portion of the output. When screenshots are not available, queries are written directly in the document using a monospaced format. All queries accurately reflect the database structure and demonstrate professional SQL documentation practices.

## Summary
In this project, I used SQL queries with filters to investigate potential security incidents and retrieve employee information. I applied AND, OR, NOT, and LIKE operators, as well as date and time filtering, to analyze login activity and employee data. These techniques demonstrate how SQL can be used to support real-world cybersecurity investigations and system security efforts.
