# IDOR
This vulnerability is known as Insecure Direct Object Reference (IDOR), wherein a user can directly access data owned by another user. 
- Example:
	- There exists a domain http://domain.htb/data/ where is stored different data. When we access with our user the URL that appears is http://domain.htb/data/2, that could mean that exists a sub-directory in data for each user. If we search http://domain.htb/data/0 and the information that we obtain is different we a re in front of an IDOR.

# Path Hijacking
Path hijacking occurs when an attacker manipulates the $PATH variable to force the system to execute a malicious file instead of the intended command. For doing that, the attacker places a directory under his control at the beginning of $PATH.
- Example:
	- Look for a file that can be executed as root.
	```bash
	sudo -l
	```
	- Find where is this file located and if the location is included in the path.
	 ```bash 
	 whereis <file>
	 echo $PATH
	 ```
	 - Create a new file with the exploit code and locate it inside a known directory.
	 - Modify the $PATH to point to the chosen directory.
	 ```bash
	 export PATH=/<directory>:$PATH
	```
 


# Path Traversal <a name='dt'></a>

The attack typically takes advantage of insufficient input validation or sanitization mechanisms. By manipulating the input, an attacker can traverse directories and access sensitive files that should not be directly accessible. This could include system files, configuration files, or even user data.

For example, if a web application allows users to download files by specifying a file name in the URL, an attacker could provide a malicious input such as "../../../etc/passwd" to traverse up the directory tree and access the password file.

That can be useful if, for example, the web has a php file with a variable called `filename`.
In this case, we could make a request attempting to access other files, such as /etc/passwd.

```bash
http://example.com/?filename=../../../../../../etc/passwd
```
In some cases the php code can be blocking this attack switching "../" with "". In this case we could try to do:
```bash
http://example.com/?....//....//....//....//....//etc/passwd
```
Sometimes, if the previous method doesn't work, it can be useful to URL-encode the request or URL-encode it twice.
```bash
..%25df..%25df..%25df..%25df..%25df..%25df..%25df..%25dfetc/passwd
```