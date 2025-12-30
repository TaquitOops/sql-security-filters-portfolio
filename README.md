# sql-security-filters-portfolio
# Apply Filters to SQL Queries  
## SQL Portfolio Project – Cybersecurity

---

##  Project Description

In this project, I use SQL queries to investigate potential security incidents within an organization. By applying filtering techniques such as **AND, OR, NOT, and LIKE**, I analyze login attempts and employee data to identify suspicious activity and support security-related decisions. This project reflects real-world tasks commonly performed by entry-level cybersecurity and SOC analysts.

---

##  Database Tables Overview

This project uses two tables from the organization’s database: **log_in_attempts** and **employees**.

### log_in_attempts

Stores employee login activity and helps detect suspicious behavior such as failed logins, after-hours access, and logins from unexpected locations.

**Columns:**
- `event_id` – Unique ID for each login event  
- `username` – Employee username  
- `login_date` – Date of the login attempt  
- `login_time` – Time of the login attempt  
- `country` – Country where the login originated  
- `ip_address` – IP address of the employee’s device  
- `success` – Login result (`FALSE` = failed attempt)

---

### employees

Contains employee and device information used to determine which users require security updates.

**Columns:**
- `employee_id` – Unique employee ID  
- `device_id` – Device assigned to the employee  
- `username` – Employee username  
- `department` – Employee department  
- `office` – Office location

---

##  SQL Queries and Analysis

###  Retrieve After-Hours Failed Login Attempts

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
AND success = 0;

Explanation:
This query identifies failed login attempts that occurred after business hours. Using the AND operator ensures that only login attempts that were both unsuccessful and after 6:00 PM are returned, helping detect potentially suspicious activity.

2️ Retrieve Login Attempts on Specific Dates
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
OR login_date = '2022-05-08';

Explanation:
This query retrieves login attempts from a specific incident date and the day before. The OR operator allows filtering records from either date, which is useful when investigating incidents spanning multiple days.

3️ Retrieve Login Attempts Outside of Mexico
SELECT *
FROM log_in_attempts
WHERE country NOT LIKE 'MEX%';

Explanation:
This query finds login attempts that did not originate in Mexico. The LIKE operator with % matches values such as MEX or MEXICO, and NOT excludes them to return only foreign login attempts.

4️ Retrieve Employees in Marketing (East Building)
SELECT *
FROM employees
WHERE department = 'Marketing'
AND office LIKE 'East%';

Explanation:
This query retrieves employees from the Marketing department located in the East building. The LIKE operator allows matching all East offices, and AND ensures both conditions are met.

5️ Retrieve Employees in Finance or Sales
SELECT *
FROM employees
WHERE department = 'Finance'
OR department = 'Sales';

Explanation:
This query identifies employees who belong to either the Finance or Sales departments. The OR operator enables filtering based on multiple possible values in the same column.

6️ Retrieve All Employees Not in IT
SELECT *
FROM employees
WHERE department != 'Information Technology';

Explanation:
This query retrieves all employees who are not part of the IT department. This helps identify users who still require a specific security update that IT employees have already received.

 Documentation Notes

SQL queries were executed in a MariaDB shell as part of the Filter with AND, OR, and NOT lab.

Screenshots (when included) show only the SQL terminal and output.

When screenshots are not included, queries are clearly written using a monospaced format for readability.

Queries demonstrate filtering with AND, OR, NOT, LIKE, as well as date and time conditions.

 Summary

This project demonstrates my ability to use SQL to analyze login activity and employee data during a security investigation. By applying logical operators and pattern matching, I retrieved targeted datasets relevant to cybersecurity analysis. These skills are directly applicable to real-world environments and entry-level security analyst roles.

 Skills Demonstrated

SQL querying and filtering

AND, OR, NOT logical operators

Pattern matching with LIKE

Date and time filtering

Cybersecurity incident analysis

Technical documentation for security portfolios
