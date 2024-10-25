# OpenVPN

A recommended VPN tool is **OpenVPN**, that can be installed with this command:
```
sudo apt-get install openvpn
```

For using it we will need root permissions.
```
sudo openvpn <client.ovpn>
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


# 15 steps to remain anonymous
https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet
## Table of contents

-  **Step 1**  [Make some fake mobile numbers and emails to Stay Anonymous](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-nbsp-step-1-make-some-fake-mobile-numbers-and-emails-to-stay-anonymous)
- **Step 2**  [Untraceable Internet source to Become Anonymous](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-2-untraceable-internet-source-to-become-anonymous)
- **Step 3**  [An Anonymous-OS system to Stay Anonymous](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-3-an-anonymous-os-system-to-stay-anonymous)
- **Step 4**  [Change your mac address](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-4-nbsp-change-your-mac-address)
- **Step 5**  [Use a Vpn or a proxy to Stay Anonymous](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-5-use-a-vpn-or-a-proxy-to-stay-anonymous)
    - [Install OpenVPN](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-install-openvpn)
    - [Running the OpenVPN client with the downloaded client config setup file](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-running-the-openvpn-client-with-the-downloaded-client-config-setup-file)
    - [Use Proxychains](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-use-proxychains)
        - [Running proxy chains with Mozilla](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-running-proxy-chains-with-mozilla)
- **Step 6**  [Disable all telemetry services for your browser and disable tracking services](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-6-disable-all-telemetry-services-for-your-browser-and-disable-tracking-services)
- **Step 7**  [Block cookies.](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-7-block-cookies)
- **Step 8**  [Block Plugins to Get Anonymous](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-8-block-plugins-to-get-anonymous)
- **Step 9**  [Do not use google](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-9-do-not-use-google)
- **Step 10**  [Turn off your location](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-10-turn-off-your-location)
- **Step 11**  [Disable access to camera and other media and disable hardware acceleration](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-11-disable-access-to-camera-and-other-media-and-disable-hardware-acceleration)
- **Step 12**  [Disable WebRTC (Leaks IP Addresses)](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-12-disable-webrtc-leaks-ip-addresses)
- **Step 13**  [Disable Javascript to Stay Anonymous](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-13-disable-javascript-to-stay-anonymous)
- **Step 14**  [Disable Health Reporting](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-14-disable-health-reporting)
- **Step 15**  [Disable flash](https://hackeracademy.org/how-to-stay-anonymous-and-untraceable-on-the-internet/#h-step-15-disable-flash)


# Using TOR for pentesting
https://www.sans.org/blog/tor-nonymous-using-tor-for-pen-testing/