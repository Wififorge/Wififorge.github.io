---
title: Troubleshooting Guide
---
**Solutions for Common WifiForge Issues and Problems**

> **⚠️ IMPORTANT SAFETY WARNING ⚠️**
> 
> **WifiForge and mininet-wifi should ONLY be used in virtual environments (VMs or Docker containers).** 
> 
> **DO NOT install or run on bare metal systems** - mininet-wifi can:
> - Interfere with your host system's network configuration
> - Modify kernel modules and network interfaces
> - Potentially disrupt your main system's connectivity
> - Require system-level changes that may affect stability
> 
> **Always use:**
> - **Docker** (recommended): Isolated container environment
> - **Virtual Machines**: VMware, VirtualBox, Hyper-V, etc.
> - **Never** install directly on your main operating system
> 
> If you see commands in this guide suggesting bare metal installation, they are intended for use **inside** virtual environments only.

This guide provides troubleshooting solutions for WifiForge framework issues, based on common problems with mininet-wifi and virtual wireless environments.

---

## Quick Diagnostic Steps

### Basic Framework Check
```bash
# Navigate to WifiForge directory
cd ~/WifiForge

# Verify main scripts exist and are executable
ls -la WifiForge.py

# Check Python environment
python3 --version  # Should be 3.7+
which python3

# Check if in correct directory
pwd
echo "Expected directory should contain WifiForge.py"
```

### Docker Container Check
```bash
# Check if Docker container is running
sudo docker ps | grep mininet-wifi

# Access running container
sudo docker exec -it mininet-wifi /bin/bash

# Start stopped container
sudo docker start mininet-wifi
sudo docker exec -it mininet-wifi /bin/bash
```

---

## Installation Issues

### Issue: Framework Scripts Won't Execute
**Symptoms**: Permission denied or command not found errors

**Solution Steps**:
```bash
# Fix file permissions
chmod +x ~/WifiForge/*.py
sudo chown -R $USER:$USER ~/WifiForge

# Check if scripts are executable
ls -la ~/WifiForge/WifiForge.py

# Verify Python can import required modules
python3 -c "import sys; print('\\n'.join(sys.path))"
```

### Issue: Mininet-WiFi Not Working
**Symptoms**: `sudo mn --wifi` command fails or not found

**Solution Steps**:
```bash
# Check if mininet-wifi is installed
sudo mn --wifi --version

# If not installed, install from source
cd /tmp
git clone https://github.com/intrig-unicamp/mininet-wifi.git
cd mininet-wifi
sudo util/install.sh -Wlnfv

# Verify installation
sudo mn --wifi --version

# Clean any previous network state
sudo mn -c
```

### Issue: Python Dependencies Missing
**Symptoms**: Import errors when running framework scripts

**Solution Steps**:
```bash
# Install common wireless security Python packages
pip3 install scapy netfilterqueue

# If using virtual environment
cd ~/WifiForge
python3 -m venv wififorge-env
source wififorge-env/bin/activate
pip install scapy netfilterqueue

# Check for other dependencies mentioned in repository
cat ~/WifiForge/README.md
```

### Issue: Permission Denied for Network Operations
**Symptoms**: Cannot create virtual interfaces or network operations fail

**Solution Steps**:
```bash
# Add user to required groups
sudo usermod -a -G netdev,sudo $USER
newgrp netdev

# Restart session to apply group changes
# Note: You may need to log out and back in
```

---

## Docker Issues

### Issue: Xterm Does Not Work
**Symptoms**: Graphical interfaces fail in Docker container or XHost errors

**Root Cause**: X11 forwarding restrictions between Docker container and host machine.

**Solution**:
```bash
# Enable X11 forwarding for root
xhost si:localuser:root

# Verify X11 environment variables
echo $DISPLAY
xhost

# If still having issues, try alternative X11 setup
xhost +local:docker
export DISPLAY=:0
```

### Issue: Dockerfile Stops at apt update
**Symptoms**: Docker installation hangs during package updates

**Root Cause**: Network state conflicts after running WifiForge.

**Solution**:
```bash
# Reboot the host system
sudo reboot

# After reboot, try running the Docker installation again
sudo docker pull redblackbird/wififorge:latest

# If the issue persists, clear Docker cache
sudo docker system prune -a

# Then retry installation
```

### Issue: Container Won't Start or Access Denied
**Symptoms**: Docker run command fails or container refuses to start

**Solution Steps**:
```bash
# Check Docker service status
sudo systemctl status docker
sudo systemctl restart docker

# Check if container already exists
sudo docker ps -a | grep mininet-wifi

# Remove existing container if needed
sudo docker rm mininet-wifi

# Try running with fresh container using full command:
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

### Issue: Docker Container Starts but WifiForge Won't Run
**Symptoms**: Can access container but framework fails to execute

**Solution Steps**:
```bash
# Inside the Docker container, navigate to WifiForge
cd /WifiForge/

# Start required services
service openvswitch-switch start

# Check if services are running
systemctl status openvswitch-switch

# Verify WifiForge files exist
ls -la WifiForge.py

# Try running with sudo
sudo python3 WifiForge.py

# Check for any error messages and ensure proper permissions
chmod +x WifiForge.py
```

---

## Virtual Environment and Network Issues

### Issue: VM Isolation Problems
**Symptoms**: Framework reports it's not running in a VM

**Solution Steps**:
```bash
# Verify you're in a virtual machine (recommended)
systemd-detect-virt || echo "VM environment recommended"
cat /proc/cpuinfo | grep hypervisor

# Check for VM indicators
ls /sys/devices/virtual/
dmesg | grep -i virtual | head -5

# Ensure no real wireless interfaces
iw dev | grep Interface | wc -l
# Should be 0 for virtual environment
```

### Issue: Virtual Wireless Interfaces Not Created
**Symptoms**: No wireless interfaces available for labs

**Solution Steps**:
```bash
# Load mac80211_hwsim module for virtual wireless
sudo modprobe mac80211_hwsim radios=2

# Verify virtual interfaces created
iw dev
iwconfig

# Make persistent across reboots (optional)
echo 'mac80211_hwsim' | sudo tee -a /etc/modules

# Check kernel module status
lsmod | grep mac80211
```

### Issue: Network Manager Conflicts
**Symptoms**: Virtual interfaces disappear or cannot be configured

**Solution Steps**:
```bash
# Restart NetworkManager
sudo systemctl restart NetworkManager

# Disable NetworkManager for virtual interfaces (if needed)
sudo systemctl stop NetworkManager
sudo systemctl disable NetworkManager

# Or configure NetworkManager to ignore virtual interfaces
sudo tee -a /etc/NetworkManager/NetworkManager.conf << 'EOF'
[keyfile]
unmanaged-devices=interface-name:wlan*
EOF

sudo systemctl restart NetworkManager
```

---

## Usage Issues

### Issue: Framework Components Not Responding
**Symptoms**: Scripts hang or don't provide expected output

**Solution Steps**:
```bash
# Check for running mininet processes
pgrep -f mininet
sudo mn -c  # Clean any hanging processes

# Kill any hung processes
sudo killall -9 python3
sudo killall -9 hostapd
sudo killall -9 dnsmasq

# Restart with clean environment
cd ~/WifiForge
ls -la WifiForge.py  # Verify file exists before launching
```

### Issue: Tool Integration Problems
**Symptoms**: Aircrack-ng or other tools not working properly

**Solution Steps**:
```bash
# Verify tools are installed
which aircrack-ng
which python3

# Install missing wireless tools
sudo apt update
sudo apt install -y aircrack-ng wireshark-common tshark

# Check tool versions
aircrack-ng --version
python3 --version
```

### Issue: Resource or Performance Problems
**Symptoms**: Slow execution or high resource usage

**Solution Steps**:
```bash
# Monitor system resources
htop
free -h
df -h

# Optimize VM settings:
# - Allocate 4-8GB RAM to VM
# - Enable hardware acceleration
# - Use SSD storage if available
# - Allocate 2-4 CPU cores

# Clear system cache
sudo sync && sudo sysctl vm.drop_caches=3

# Adjust system parameters
sudo sysctl vm.swappiness=10
```

---

## Diagnostic Information Collection

### Gathering System Information
```bash
# System environment
echo "=== System Information ==="
uname -a
lsb_release -a

echo "=== Virtualization Status ==="
systemd-detect-virt 2>/dev/null || echo "Unknown"

echo "=== Docker Status ==="
sudo docker --version
sudo docker ps | grep mininet-wifi || echo "No WifiForge container running"

echo "=== Python Environment ==="
python3 --version
which python3

echo "=== Network Interfaces ==="
ip link show

echo "=== Wireless Tools ==="
which aircrack-ng
which iw
which iwconfig

echo "=== Mininet Status ==="
sudo mn --wifi --version 2>/dev/null || echo "Not installed"

echo "=== Virtual Environment ==="
echo "VIRTUAL_ENV: ${VIRTUAL_ENV:-'Not activated'}"
```

### Docker-Specific Diagnostics
```bash
# Docker container diagnostics
echo "=== Docker Container Status ==="
sudo docker ps -a | grep mininet-wifi

echo "=== Docker Image Status ==="
sudo docker images | grep wififorge

echo "=== Docker System Information ==="
sudo docker system df

echo "=== Container Logs ==="
sudo docker logs mininet-wifi | tail -20
```

### Logs and Debug Information
```bash
# Check system logs for errors
sudo journalctl -u NetworkManager --since "1 hour ago" | tail -20
dmesg | grep -i "error\|fail" | tail -10

# Monitor network interface changes
ip monitor link

# Check for conflicting processes
sudo netstat -tulpn | grep -E ":80|:443|:53"
```

---

## Emergency Recovery

### Complete Environment Reset
```bash
# Stop all related services
sudo killall -9 python3 hostapd dnsmasq
sudo mn -c

# Reset network configuration
sudo systemctl restart NetworkManager
sudo rfkill unblock wifi

# Remove and reload wireless modules
sudo modprobe -r mac80211_hwsim
sudo modprobe mac80211_hwsim radios=2

# Verify clean state
iw dev
ip link show
pgrep -f mininet | wc -l  # Should be 0
```

### Docker Container Reset
```bash
# Stop and remove existing container
sudo docker stop mininet-wifi
sudo docker rm mininet-wifi

# Pull fresh image
sudo docker pull redblackbird/wififorge:latest

# Restart with clean container (use full docker run command from installation)
```

### Snapshot Recovery
If you've created snapshots:
- **VMware**: VM → Snapshot → Revert to Snapshot
- **VirtualBox**: Machine → Restore Snapshot
- **Hyper-V**: Action → Revert

---

## Getting Help

### Before Asking for Help
1. **Read the documentation**: Check [Overview.md](Overview.md) and [Installation.md](Installation.md) first
2. **Search existing issues**: Look for similar problems in [GitHub Issues](https://github.com/blackhillsinfosec/WifiForge/issues)
3. **Check for updates**: Ensure you're using the latest version from the [repository](https://github.com/blackhillsinfosec/WifiForge)
4. **Gather diagnostic information**: Use the diagnostic commands above to collect system info
5. **Try basic solutions**: Work through the common issues in this guide

### Where to Get Help
- **GitHub Issues**: Primary support channel for reporting problems and getting help
- **Documentation**: Check all documentation files in this folder for guidance
- **Lab 00**: Start with the framework basics lab for initial setup help

### Reporting Issues Effectively
When creating a GitHub issue, include:

**Required Information:**
- **WifiForge version**: Check with `git log --oneline -1` in WifiForge directory
- **Operating System**: `lsb_release -a` output
- **Installation method**: Docker or source installation
- **Python version**: `python3 --version`

**Problem Details:**
- **Clear title**: Describe the specific issue (e.g., "Docker container fails to start on Ubuntu 22.04")
- **Steps to reproduce**: Exact commands that cause the issue
- **Expected behavior**: What should happen
- **Actual behavior**: What actually happens
- **Complete error output**: Full error messages, not just snippets

**System Information:**
Run the "Gathering System Information" commands from the Diagnostic section above and include the output in your issue.

### Common Issue Patterns
These issues occur frequently and often have known solutions:
- **Docker X11/Graphics issues**: Usually resolved with proper X11 forwarding setup
- **Installation hanging**: Often fixed by rebooting and clearing Docker cache
- **Virtual interface problems**: Typically resolved by reloading wireless modules
- **Permission errors**: Usually fixed by proper group membership and session restart

### Self-Help Tips
- **Reboot first**: Many network-related issues resolve after a system restart
- **Check logs**: Use `dmesg`, `journalctl`, and Docker logs for error details
- **Virtual environment**: Always use VMs or Docker for safety and easier troubleshooting
- **Clean state**: Use `sudo mn -c` to clean mininet state between runs

---

**Remember**: WifiForge is actively developed and constantly evolving. Many issues can be resolved by updating to the latest version or following the "Emergency Recovery" procedures above.