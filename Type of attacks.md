## IDOR
This vulnerability is known as Insecure Direct Object Reference (IDOR), wherein a user can directly access data owned by another user. 
- Example:
	- There exists a domain http://domain.htb/data/ where is stored different data. When we access with our user the URL that appears is http://domain.htb/data/2, that could mean that exists a sub-directory in data for each user. If we search http://domain.htb/data/0 and the information that we obtain is different we a re in front of an IDOR.