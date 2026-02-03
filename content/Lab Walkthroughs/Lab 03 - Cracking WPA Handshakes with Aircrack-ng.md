---
title: Lab 03 - Cracking WPA Handshakes with Aircrack-ng
---

**Estimated Time:** ~10-15 minutes  

## Summary
Use aircrack-ng to crack WPA handshakes captured in previous labs using dictionary-based password attacks.

Select "Cracking WPA with Aircrack" from the main menu. Allow up to 30 seconds to initialize the network. 

![[05-main-menu.png]]

A single attacker window will appear in your terminal. 

Run the following command in this terminal to crack the key associated with the WPA handshake collected from the bettercap lab. 

```
aircrack-ng -w /WifiForge/framework/lab_materials/rockyou.txt /WifiForge/framework/lab_materials/loot/4whs-01.cap
```

If your capture file contains multiple networks, aircrack will find all the networks in the capture and ask which network the hash is associated with. Input the number associated with the WPA2_Network and hit enter if you are prompted.

![[05-networks.png]]

Allow for up to 30 seconds for the password to be revealed.

![[05-key-found.png]]

You now are familiar with two different methods to collect and crack WPA2 keys. Use the `main_menu` command to return to the main menu and onto the next lab. 

## Lab Complete
Congratulations! You have successfully completed Lab 05. You now understand:
- Using aircrack-ng for WPA handshake analysis
- Dictionary-based password cracking techniques
- Working with previously captured handshake files
- Multiple network selection in capture files

---

