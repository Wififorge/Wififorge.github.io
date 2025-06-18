---
title: WifiForge Documentation
---
**Safe and Legal Wi-Fi Security Training Through Virtual Network Simulation**

WifiForge is a Wi-Fi security training tool developed by **Black Hills InfoSec** that provides a safe and legal environment for learning Wi-Fi hacking techniques. Based on the open source mininet-wifi framework, WifiForge automatically sets up virtual networks needed to run Wi-Fi exploitation labs without physical hardware.

> **IMPORTANT**: WifiForge is in active development and **is recommended for use in virtual environments only**

---

## Quick Navigation

**[Overview](Overview.md)** - Comprehensive framework overview, available labs, and tools you'll use

**[Installation & Setup](Installation.md)** - Complete installation guide with Docker and source installation methods

**[Troubleshooting](Troubleshooting.md)** - Common issues, diagnostic commands, and performance optimization

**[Development](Development.md)** - Contributing guidelines, project structure, and development standards

---

## Lab Quick Access

| Lab                                                                                                                   | Topic                                                      | Duration |
| --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- | -------- |
| [Lab 00](Lab%20Walkthroughs/Lab%2000%20-%20Getting%20Started.md)                                                      | Getting Started                                            | ~10 min  |
| [Lab 01](Lab%20Walkthroughs/Lab%2001%20-%20Bettercap%20Recon.md)                                                      | Bettercap Recon                                            | ~20 min  |
| [Lab 02](Lab%20Walkthroughs/Lab%2002%20-%20Bettercap%20Wi-Fi%20Authentication%20Capture.md)                           | Bettercap Wi-Fi Authentication Capture                     | ~25 min  |
| [Lab 03](Lab%20Walkthroughs/Lab%2003%20-%20Packet%20Capture%20to%20HCCAPX%20Conversion%20and%20Hashcat%20Cracking.md) | Packet Capture to HCCAPX Conversion and Hashcat Cracking   | ~20 min  |
| [Lab 04](Lab%20Walkthroughs/Lab%2004%20-%20Airsuite%20Tools%20-%20Recon%20and%20Pre-Shared%20Key%20Recovery.md)       | Airsuite Tools - Recon and Pre-Shared Key Recovery         | ~35 min  |
| [Lab 05](Lab%20Walkthroughs/Lab%2005%20-%20Cracking%20WPA%20Handshakes%20with%20Aircrack-ng.md)                       | Cracking WPA Handshakes with Aircrack-ng                   | ~15 min  |
| [Lab 06](Lab%20Walkthroughs/Lab%2006%20-%20Airgeddon%20Denial%20of%20Service%20Beacon%20Attacks.md)                   | Airgeddon Denial of Service Beacon Attacks                 | ~25 min  |
| [Lab 07](Lab%20Walkthroughs/Lab%2007%20-%20Capture%20Active%20Directory%20Credentials%20with%20Evil-Twin%20Attack.md) | Capture Active Directory Credentials with Evil-Twin Attack | ~20 min  |
| [Lab 08](Lab%20Walkthroughs/Lab%2008%20-%20Cracking%20NETNTLM%20Credentials%20with%20John%20the%20Ripper.md)          | Cracking NETNTLM Credentials with John the Ripper          | ~20 min  |
| [Lab 09](Lab%20Walkthroughs/Lab%2009%20-%20Rogue%20AP%20with%20Wifiphisher.md)                                        | Rogue AP with Wifiphisher                                  | ~35 min  |
| [Lab 10](Lab%20Walkthroughs/Lab%2010%20-%20WPS%20Exploitation.md)                                                     | WPS Exploitation                                           | ~30 min  |
| [Lab 11](Lab%20Walkthroughs/Lab%2011%20-%20WEP%20Key%20Cracking.md)                                                   | WEP Key Cracking                                           | ~30 min  |
| [Lab 12](Lab%20Walkthroughs/Lab%2012%20-%20Drone%20Hacking.md)                                                        | Drone Hacking                                              | ~45 min  |

---

## About

WifiForge is a Wi-Fi security training framework that eliminates the traditional barriers to wireless security education. Built on mininet-wifi technology, it provides:

- **13 Hands-On Labs**: From basic reconnaissance to advanced exploitation techniques
- **Real Security Tools**: Aircrack-ng, Bettercap, Hashcat, Wifiphisher, and more
- **Zero Hardware Required**: Complete virtual wireless network simulation
- **Safe Learning Environment**: No interaction with real networks
- **Professional Skills**: Practical penetration testing techniques

**Perfect for**: Security professionals, students, penetration testers, and anyone wanting to learn wireless security without expensive equipment or complex setup.

## Mission

Our goal at Black Hills Information Security is to remove any barriers preventing you the end user from learning about new topics. With the wireless world being a backbone of security it's important to understand attacks without the pay wall. This tool removes the need for any hardware or setup. In other words, it just werks.

Be on the look out for more Forge tools down the road.

---

## Project Info & Roadmap

- **Version**: v3.3.0 | **Stars**: 303+ | **Forks**: 37+
- **Language**: Python (77.8%) | **License**: Apache-2.0
- **Repository**: [GitHub](https://github.com/blackhillsinfosec/WifiForge)

### Development Roadmap

#### v3.x.x (Current Focus)
- **WPS Lab Enhancement**: Currently the WPS Pixie Dust Attack lab does not work, this is under investigation and development
- **Stability Improvements**: Framework refinements and bug fixes
- **Documentation Expansion**: Comprehensive guides and educational materials

#### v4.0.0 (Under Development)
The next major version is currently under development with planned features:

- **WifiProbe**: A snapshot tool that takes a snapshot of the wireless landscape around the host, making a 1:1 copy of the Access Points
- **WifiHound**: An output file type for WifiProbe that formats an output file that can be fed into BloodHound to check different analytics and Access Point information

---

## Ready to Learn?

**New to Wireless Security?** → Start with [Overview](Overview.md)  
**Ready to Install?** → Jump to [Installation](Installation.md)  
**Want to Contribute?** → Check [Development](Development.md) 