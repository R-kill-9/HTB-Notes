This is a tool created by [s4vitar](https://github.com/s4vitar) with the aim of deploying an automated Rogue AP. Using it, you can capture the credentials of the victims that connect to your fake Wifi. In my case, I could not capture **IOS** requests.

Tool link: https://github.com/s4vitar/evilTrust

# Configuration
First of all, if you are not using any network card you need to ensure that your laptop can use the `Monitor`mode on its own card.

- Stop Network Manager
```bash
sudo systemctl stop NetworkManager
```
- Setup the network card in monitor mode
```bash
sudo iwconfig wlan0 mode monitor
```
- Verify that the Monitor mode is enabled
```bash
iwconfig
```

Once you have finished the activity, you can reconnect your wifi settings.
```bash
sudo iwconfig wlan0 mode managed
sudo systemctl start NetworkManager
```

# Usage
Before using it you just need to ensure that you have installed the following tools:
- php
- dnsmasq
- hostapd

Next, you need to select the interface to use, the name for your new access point and the channel to use (the most recommended ones are 1, 6, 11).

Finally, you need to select the template that you want to use and wait for the victims to introduce their credentials.