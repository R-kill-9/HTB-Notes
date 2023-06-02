## revshells.com
It's a very useful online tool that allows you to create a reverse shell in a lot of programming languages specifying the ip and the port.

## Cookies
- It can be very useful checking the cookies of a web-site. For example if we are on a web and we have this parameters on a table:
	- role: guest
	- user: 24322
- And we know that there exists the admin role and it's userId is 34322, we can change them to gain access as admin.
	- role: admin
	- user: 34322
- After using this, if we have gained admin's account, we have a lot of opportunities to exploit the machine. For example, if as admin we can upload files we can try to do a reverse shell.
## /usr/share/webshells/
If we are using Parrot or Kali we can find in this directory a lot of reverse shells and backdoors.
For example, if we want to do a reverse shell in php we can use:
- /usr/share/webshells/php/php-reverse-shell.php