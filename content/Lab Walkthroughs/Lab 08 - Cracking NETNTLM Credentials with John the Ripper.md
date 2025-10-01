---
title: Lab 08 - Cracking NETNTLM Credentials with John the Ripper
---

**Estimated Time:** ~15-20 minutes  

## Summary
Crack captured NetNTLM hashes using John the Ripper with mask-based attacks for efficient password recovery.

Select "Ntlm John Crack" from the menu. Allow up to 30 seconds to initialize the network. 

![[08-main-menu.png]]

A single attacker pane will appear in your terminal. 

Run the following command to crack the NetNTLM hash found in the last lab. Note that this uses a wildcard for the capture filename, you may need to specify your filename directly if the file cannot be found. 

```
john --format=netntlm /WifiForge/framework/lab_materials/loot/wpa_handshake_capture* --mask='Badpass?d' --min-length=7 --max-length=13 --pot=/WifiForge/framework/lab_materials/loot/output.pot
```

The above command is an example of using a *mask*. Masks point John in a direction to crack a password from a partially known one. In this case, John brute forces the password by appending a set of characters onto the phrase Badpass. Masks are usually useful if a pattern can be found among groups of passwords. 

Eventually, John will crack the password as seen in the screenshot below. 

![[08-john.png]]

Use the `main_menu` command to return to the main menu and onto the next lab. 

## Lab Complete
Congratulations! You have successfully completed Lab 08. You now understand:
- Cracking NetNTLM hashes with John the Ripper
- Using mask-based attacks for targeted password cracking
- Working with enterprise credential hashes
- Pattern-based password attack strategies

---
**PREVIOUS LAB:** [Lab 07 - Capture Active Directory Credentials with Evil-Twin Attack](Lab%2007%20-%20Capture%20Active%20Directory%20Credentials%20with%20Evil-Twin%20Attack.md)  
**NEXT LAB:** [Lab 09 - Rogue AP with Wifiphisher](Lab%2009%20-%20Rogue%20AP%20with%20Wifiphisher.md)

