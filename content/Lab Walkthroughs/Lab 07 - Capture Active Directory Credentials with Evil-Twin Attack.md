Select "Evil Twin" from the menu. Allow up to 30 seconds to initialize the network. 

![[07-main-menu.png]]

A single attacker pane will appear in your terminal. 

Note: The software and methods used to create these labs are strictly limited to Linux environments. This lab uses a simulated connection to provide the NetNTLM hashes. Nonetheless, the process shown here exactly mirrors a real application of Eaphammer. 

Run the following command to start Eaphammer. 

```
/WifiForge/framework/lab_materials/eaphammer -e CORP_NET --creds --interface a-wlan0
```

Running this command will result in the following output. The hashes should appear as seen below after being captured from an authenticating host. Allow up to a minute for this to occur. 

![[07-eaphammer.png]]
The following will appear when the connection occurs. 

![[07-hashes.png]]

Hashes are saved to /Wifi-Forge/Framework/loot/ under the filename wpa_handshake_capture\[date]\[random_string].

Use the `main_menu` command to return to the main menu and onto the next lab.

NEXT LAB: [[Lab 07 - Capture Active Directory Credentials with Evil-Twin Attack]]