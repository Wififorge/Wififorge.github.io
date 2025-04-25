Select "Packet Capture To Hccapx Hashcat Cracking" from the menu. Allow up to 30 seconds to initialize the network. 

![[03-main-menu.png]]

Two panes will appear in the resulting screen. One represents the attacking machine "**Attacker**". The other panel represents the host machine from which you will launch a browser session. 

![[03-terminals.png]]

Click the area within the "**host_machine**" panel to ensure that the host machine terminal is selected. Type the following command to open a browser window. 

```bash
/WifiForge/framework/lab_materials/browser linux
```

Ignore any errors that appear on the command line. Wait for a chrome browser to appear as seen below.

![[03-browser.png]]

Insert the following filepath into your browser.

```bash
file:///WifiForge/framework/lab_materials/hashcat.net/cap2hashcat/index.html
```

The following site will appear in the browser window. 

![[03-browser-hashcat.png]]

Select browse, navigate to the /Wifi-Forge/Framework/loot/4whs file, and click convert.

![[03-browser-upload.png]]

After clicking the convert button, click "Download." Close the Chrome window. 

Select your attacker machine by clicking in the top half of the terminal window. 

Within the attacker terminal, run the following command. Replace \<YOUR-HCCAPX-HERE\> with the HCCPAX file in your Downloads file. it will likely consist of a series of numbers with with the file type hc22000. 

```
hashcat -m22000 -a0 ~/Downloads/<YOUR-HCCAPX-HERE> /WifiForge/framework/lab_materials/rockyou.txt --potfile-path /Wifi-Forge/Framework/loot/4whs.pot
```

The following will appear on your screen. Hashcat will attempt to crack the password using the hash we recovered in the last lab. Allow for a few minutes for it to iterate through all the possible passwords.

![[03-hashcat-running.png]]

When it succeeds, the most likely passwords will be revealed (in this case, the password is december2022)

![[03-hashcat-results.png]]

In either of the terminal panes, type `main_menu` to return to the main menu and onto the next lab. 

NEXT LAB: [[Lab 04 - Airsuite Tools - Recon and Pre-Shared Key Recovery]]