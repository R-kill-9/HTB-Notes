If you already have the database on your Kali machine, you can easily view and analyze it using the appropriate tools. The first step is to identify the type of database to choose the correct tool. Below is a general guide on how to proceed:

#  **Identify the type of database**

First, make sure you know the format of the database. To do so, use the `file` command:
```bash
file archivo.bd
```
This command will tell you what type of file it is (for example, SQLite, MySQL dump, PostgreSQL, etc.).

# sqlite3
- Open the database with `sqlite3`:
```sql
sqlite3 archivo.bd
```

- To list all tables:
```sql
.tables
```

- To see the schema of a table:
```sql
.schema table_name
```

- To query all the data from a table:
```sql
SELECT * FROM table_name;
```

- To exit:
```sql
.exit
```

# MySQL or MariaDB
- Create a new database:
```sql
mysql -u root -p
CREATE DATABASE db_name;
EXIT;
```
- Import the `.bd` file (if it’s an SQL dump):
```sql
mysql -u root -p db_name < archivo.bd
```
- Once imported, you can connect to the database:
```sql
mysql -u root -p db_name
```
### Commands <a name="mysql"></a>

- Prints out the databases we can access:
````bash
SHOW databases;
````  

- Set to use the database named {database_name}:
````bash
USE {database_name};
````  

- Prints out the available tables inside the current database:

````bash
SHOW tables;
````  
- Prints out all the data from the table {table_name}:
````bash
SELECT * FROM {table_name};
````  


# PostgreSQL
- Create a new database:
```sql
sudo -u postgres createdb db_name
```
- Import the `.bd` file (if it’s an SQL dump):
```sql
psql -U postgres -d db_name -f archivo.bd
```
- Once imported, you can connect to the database:
```sql
psql -U postgres -d db_name
```

# DBeaver
If you prefer a graphical interface to analyze the database, you can install tools like **DBeaver**:

```sql
sudo apt install dbeaver
```