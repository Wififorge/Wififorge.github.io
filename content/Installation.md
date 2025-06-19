---
title: Installation & Setup Guide
---
**Complete Installation and Configuration Guide for WifiForge**

This comprehensive guide covers everything you need to install and configure WifiForge for safe Wi-Fi security training.

---

## Critical Safety Requirements

> **IMPORTANT**: WifiForge is in active development and **is recommended for use in virtual environments only**.

---

## Compatibility

> [!WARNING]
> Wifi-Forge will not run on Kali Kernel release 6.12.13. Check your kernel version using `uname -r` and update if necessary. Running `sudo apt upgrade` followed by a reboot often updates the kernel on its own. 


WifiForge works on the following Linux operating systems:
- **Kali Linux** 
- **Parrot OS**
- **Ubuntu**

---

## Docker Installation (Recommended)


### Why Docker is Recommended
This is the **easiest and quickest method** of installation. Docker provides:
- **Complete Environment**: All dependencies included
- **Consistent Setup**: Same environment regardless of host OS
- **Quick Deployment**: Minimal understanding required
- **Easy Management**: Simple container lifecycle

### Step 1: Install Docker
```bash
# Update system packages
sudo apt update -y

# Install Docker
sudo apt install docker.io -y
```

### Step 2: Install WifiForge Container
```bash
# Pull the latest WifiForge Docker image
sudo docker pull redblackbird/wififorge:latest
```

**Note**: Installing the Docker container can take up to an hour but averages 30 minutes.

### Step 3: Run WifiForge Container
```bash
# Run WifiForge with full privileges and X11 forwarding
sudo docker run --privileged=true -it \
  --env="DISPLAY" \
  --env="QT_X11_NO_MITSHM=1" \
  -v /tmp/.X11-unix:/tmp/.X11-unix:rw \
  -v /sys/:/sys \
  -v /lib/modules/:/lib/modules/ \
  --name mininet-wifi \
  --network=host \
  --hostname mininet-wifi \
  redblackbird/wififorge:latest /bin/bash
```

### Step 4: Start WifiForge Framework
Once inside the Docker container:
```bash
# Navigate to WifiForge directory
cd /WifiForge/

# Start OpenVSwitch service
service openvswitch-switch start

# Launch WifiForge
sudo python3 WifiForge.py
```

### Starting Existing Docker Container
After initial installation, you can start an existing Docker container:
```bash
# Start existing container
sudo docker exec -it mininet-wifi /bin/bash

# Then follow Step 4 above
```

---

## Source Installation (Advanced)

### When to Use Source Installation
- **More Control**: Full control over your experience
- **Development**: Contributing to the project
- **Customization**: Need to modify framework components

**Warning**: This method is less simple and may have more issues.

### Installation Steps
```bash
# Clone the repository
git clone https://github.com/blackhillsinfosec/WifiForge.git
cd WifiForge/framework/setup

# Run setup script
sudo ./setup.sh

# Navigate back to main directory
cd ../..

# Launch WifiForge
sudo python3 WifiForge.py
```

**Note**: Installation may take a while, this tool is massive.

---

## Bring Your Own Tools (BYOT)

### Required Tools
If you install from source, you'll need to install the following tools manually:

**Core Wireless Security Tools:**
- **Wifiphisher**: Phishing attacks against WiFi networks
- **Wifite**: Automated wireless auditing tool
- **Aircrack-ng**: Complete wireless security suite
- **Bettercap**: Modern network attack framework
- **Hashcat**: Advanced password recovery
- **John**: John the Ripper password cracker
- **Airgeddon**: Multi-use wireless security auditing tool
- **iperf**: Network performance measurement

### BYOT Installation Instructions

#### For Kali Linux (Recommended OS)
```bash
# 1. APT Packages
sudo apt install wifiphisher
sudo apt install wifite
sudo apt install aircrack-ng
sudo apt install iperf
sudo apt install bettercap
sudo apt install john

# 2. Git Tools
git clone --depth 1 https://github.com/v1s1t0r1sh3r3/airgeddon.git
cd airgeddon
sudo bash airgeddon.sh
```

#### For Ubuntu
```bash
# 1. Import Kali APT Repositories
sudo sh -c "echo 'deb https://http.kali.org/kali kali-rolling main non-free contrib' > /etc/apt/sources.list.d/kali.list"
sudo apt install gnupg -y
wget 'https://archive.kali.org/archive-key.asc'
sudo apt-key add archive-key.asc
sudo sh -c "echo 'Package: *'>/etc/apt/preferences.d/kali.pref; echo 'Pin: release a=kali-rolling'>>/etc/apt/preferences.d/kali.pref; echo 'Pin-Priority: 50'>>/etc/apt/preferences.d/kali.pref"
sudo apt update -y

# 2. APT Packages
sudo apt install -t kali-rolling wifiphisher -y
sudo apt install -t kali-rolling wifite -y
sudo apt install -t kali-rolling aircrack-ng -y
sudo apt install -t kali-rolling iperf -y 
sudo apt install -t kali-rolling bettercap -y
sudo apt install -t kali-rolling john -y

# 3. Git Tools
git clone --depth 1 https://github.com/v1s1t0r1sh3r3/airgeddon.git
cd airgeddon
sudo bash airgeddon.sh
```

#### For Parrot OS
```bash
# 1. APT Packages
sudo apt install wifiphisher
sudo apt install wifite
sudo apt install aircrack-ng
sudo apt install iperf
sudo apt install bettercap
sudo apt install john

# 2. Git Tools
git clone --depth 1 https://github.com/v1s1t0r1sh3r3/airgeddon.git
cd airgeddon
sudo bash airgeddon.sh
```

---

## Post-Installation

### Having Issues?
If you encounter any problems during installation, check our dedicated [Troubleshooting Guide](Troubleshooting.md) for comprehensive solutions.

---

## Next Steps

### Ready to Learn!
Your WifiForge environment is now installed and ready for safe, legal wireless security education. The framework provides a comprehensive platform for learning wireless security techniques in a controlled virtual environment.

**Next Steps:**
- **Explore the framework**: Check [Overview.md](Overview.md) for available labs and tools
- **Start learning**: Begin with Lab 00 to learn framework basics
- **Need help?**: Use [Troubleshooting.md](Troubleshooting.md) if you encounter issues
- **Want to contribute?**: See our [Development Guide](Development.md)

### Framework Updates
```bash
# For Docker installations
sudo docker pull redblackbird/wififorge:latest

# For source installations
cd ~/WifiForge
git pull origin main
```

---

**Installation Complete!**

Always:
- Use virtual environments only
- Follow the framework's safety guidelines
- Keep the framework updated
- Follow ethical and legal guidelines
- Take regular snapshots for backup

**Ready to start learning? Head to [Overview.md](Overview.md) to see what's available, then jump into Lab 00!** 
