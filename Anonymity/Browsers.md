# TOR (The Onion Router)

TOR is a free, open-source software for enabling anonymous communication over the Internet. It protects users' identities and online activity by routing traffic through a network of volunteer-operated servers (nodes), obscuring the user's IP address.

- Installation:
```bash
sudo apt install torbrowser-launcher
```
- Start the TOR service:
```bash
sudo service tor start
```
- Launch the TOR Browser:
```bash
torbrowser-launcher
```

# Nipe 
Nipe is a tool that enables users to route their internet traffic through the Tor network, effectively masking their IP address and enhancing anonymity.

```bash
# Download* 
git clone https://github.com/htrgouvea/nipe && cd nipe  
      
# Install libs and dependencies
sudo cpan install Try::Tiny Config::Simple JSON  
  
# Nipe must be run as root
sudo perl nipe.pl install
```

**Commands**:
- install -> Install dependencies  
- start -> Start routing  
- stop -> Stop routing  
- restart ->Restart the Nipe circuit  
- status -> See status  
```bash
sudo perl nipe.pl <command>  
```

To test, before starting Nipe, do a test and after starting, repeat the test and see that your ip will change.

```bash
# Show IP
curl ifconfig.me/ip 

# Show all information  
curl ifconfig.me/all
```

#  Proxychains

You can install and configure proxy chains by using the following commands.
```
git clone https://github.com/rofl0r/proxychains-ng
cd proxychains-ng
sudo make install
sudo make install-config (installs proxychains.conf)
```

It's recommended using proxychains-ng because it is configured to use TOR.

Use multiple proxies to create a proxy chain and use proxychains.conf to manage the settings.

You can use the following command:

```
leafpad /etc/proxychains.conf
```


### Running proxy chains with Mozilla

```
proxychains Mozilla
``` 

