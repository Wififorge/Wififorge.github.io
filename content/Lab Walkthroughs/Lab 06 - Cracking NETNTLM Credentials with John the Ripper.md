---
title: Lab 06 - Cracking NETNTLM Credentials with John the Ripper
---

**Estimated Time:** ~15-20 minutes  

## Summary
Crack captured NetNTLM hashes using John the Ripper with mask-based attacks for efficient password recovery.

Select "Ntlm John Crack" from the menu. Allow up to 30 seconds to initialize the network. 

![[08-main-menu.png]]

A single attacker pane will appear in your terminal. 

Run the following command to crack the NetNTLM hash found in the last lab. Note that this uses a wildcard for the capture filename, you may need to specify your filename directly if the file cannot be found. 

```
john --format=netntlm /wififorge/src/wififorge/labs/materials/loot/wpa_handshake_capture* --mask='Badpass?d' --min-length=7 --max-length=13 --pot=/wififorge/src/wififorge/labs/materials/loot/output.pot
```

If John reports that the file does not exist (for example, you skipped Lab 05 or the container was restarted since), use the copy of the same hash that ships with WifiForge:

```
john --format=netntlm /wififorge/src/wififorge/labs/materials/loot/john_hash --mask='Badpass?d' --min-length=7 --max-length=13 --pot=/wififorge/src/wififorge/labs/materials/loot/output.pot
```

> [!WARNING]
> This lab needs the "jumbo" edition of John the Ripper. Kali ships it; Debian and Ubuntu ship a core edition that answers `Unknown ciphertext format name requested` or `Unknown option: "--mask=Badpass?d"`. Re-running `./install-system-deps.sh` from `/wififorge` builds jumbo John when it is missing. Alternatively, crack the same hash with hashcat:
> ```
> echo 'johnnie.doyle@lab.local::::5eb76975d83fee344ededca6fb86e8b04fde87c3cde150ff:65c09d9d0f121f7d' > /tmp/netntlm.hash
> hashcat -m 5500 -a 3 /tmp/netntlm.hash 'Badpass?d?d?d?d' --potfile-disable
> ```

The above command is an example of using a *mask*. Masks point John in a direction to crack a password from a partially known one. In this case, John brute forces the password by appending a set of characters onto the phrase Badpass. Masks are usually useful if a pattern can be found among groups of passwords. 

Eventually, John will crack the password as seen in the screenshot below. 

![[08-john.png]]

Use the `main_menu` command to return to the main menu and onto the next lab. 

## Lab Complete
Congratulations! You have successfully completed Lab 06. You now understand:
- Cracking NetNTLM hashes with John the Ripper
- Using mask-based attacks for targeted password cracking
- Working with enterprise credential hashes
- Pattern-based password attack strategies

---

