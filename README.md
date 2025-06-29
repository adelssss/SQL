# README: Working with PostgreSQL using DataGrip and pgAdmin

This guide explains how to set up PostgreSQL, connect to it via DataGrip, create tables, insert data, run queries, and explore the database structure using an ER diagram.

# 1. Install Required Tools
Make sure you have the following software installed:

PostgreSQL-the database system
pgAdmin-graphical interface to manage PostgreSQL
DataGrip-advanced SQL IDE by JetBrains

 # 2. Connect to PostgreSQL via DataGrip
Open DataGrip.
Go to File-New-Data Source-PostgreSQL.
Enter the connection details:
Host: localhost (or your database server IP)
Port: 5432 (default)
User: your PostgreSQL username (e.g., postgres)
Password: your database password
Database: (existing database name or leave empty to create one later)
Click Test Connection to verify.

If successful, click OK to save the data source.

# 3. Create Tables
Once connected, you can start writing SQL queries to create your database schema.
CREATE TABLE clients (
  client_id INT PRIMARY KEY,
  client_name TEXT,
  connect_date DATE,
  revenue NUMERIC
);

After executing the query, the table will be created.
You can also verify it in pgAdmin under the "Tables" section.

# 4.Insert data(Using INSERT INTO)
You can insert  data using SQL:
INSERT INTO clients (client_id, connected_branch_id, connect_date) VALUES (1, 10, '2023-10-07');

You can insert as many rows as needed, either individually or in bulk using comma-separated value groups.

# 5. Run SQL Queries
Now you're ready to run SQL queries for analysis — filtering, grouping, aggregation, etc.
Example:
SELECT
  b.city,
  SUM(so.revenue) AS суммарная_выручка
FROM service_orders so
JOIN clients c ON so.client_id = c.client_id
JOIN branches b ON c.connected_branch_id = b.branch_id
WHERE so.status = 'завершён'
GROUP BY b.city
HAVING SUM(so.revenue) > 50000
ORDER BY суммарная_выручка DESC;

You can write and execute all queries in DataGrip’s editor.

# 6. View ER Diagram(Table Relationships)
To visualize the structure of your database:
In DataGrip:
Right-click on your database-Diagrams-Show Visualization

In pgAdmin:
Use the ERD Tool to generate entity-relationship diagrams.

This is useful for understanding how tables relate to each other-especially when writing JOIN queries.
