The following walk through can be used to deploy WifiForge with minimal understanding and within minutes.
## Compatibility
WifiForge should work on any linux operating system using the docker container. The following Operating Systems have been tested and are confirmed to work.
- Kali Linux 
- Parrot OS
- Ubuntu
## Docker Installation
This is the easiest and quickest method of installation. You will need to have docker installed to make the work properly.
To install docker run the following command:
```bash
sudo apt update -y
sudo apt install docker.io -y
```
Then install WifiForge
```bash
sudo docker pull redblackbird/wififorge:latest
sudo docker run --privileged=true -it --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" -v /tmp/.X11-unix:/tmp/.X11-unix:rw -v /sys/:/sys -v /lib/modules/:/lib/modules/ --name mininet-wifi --network=host --hostname mininet-wifi redblackbird/wififorge:latest /bin/bash
service openvswitch-switch start
cd /WifiForge/
sudo python3 WifiForge.py
```
Installing the docker container can take up too an hour but averages 30 minutes.

## Starting Existing Docker Container
After installation you can start an existing docker container and resume the labs with the following command:
```bash
sudo docker exec -it mininet-wifi /bin/bash
```

## Installing from source
This is less simple and may have more issues, however gives you more control over your experience.
```bash
git clone https://github.com/blackhillsinfosec/WifiForge.git
cd WifiForge/framework/setup
sudo ./setup.sh
cd ../..
sudo python3 WifiForge.py
```
Note: Installation may take a while, this tool is massive.
## Bring Your Own Tools (BYOT)
If you install the tool from source the tools you may need may not be included with the Operating System you chose.
The following tools will need to be installed to run through the labs and are up to the end user to install.
### Tools Required
- Wifiphisher
- Wifite
- Aircrack-ng
- Bettercap
- Hashcat
- John
- Airgeddon
- iperf

#### How to BYOT on Kali (Recommended OS)
1. APT Packages
```bash
sudo apt install wifiphisher
sudo apt install wifite
sudo apt install aircrack-ng
sudo apt install iperf
sudo apt install bettercap
sudo apt install john
```
2. Git Tools
```bash
git clone --depth 1 https://github.com/v1s1t0r1sh3r3/airgeddon.git
cd airgeddon
sudo bash airgeddon.sh
```

#### How to BYOT on Ubtuntu
1. To install the tools on Ubuntu you will need to import the Kali Apt Repositories 
```bash
sudo sh -c "echo 'deb https://http.kali.org/kali kali-rolling main non-free contrib' > /etc/apt/sources.list.d/kali.list"
sudo apt install gnupg -y
wget 'https://archive.kali.org/archive-key.asc'
sudo apt-key add archive-key.asc
sudo sh -c "echo 'Package: *'>/etc/apt/preferences.d/kali.pref; echo 'Pin: release a=kali-rolling'>>/etc/apt/preferences.d/kali.pref; echo 'Pin-Priority: 50'>>/etc/apt/preferences.d/kali.pref"
sudo apt update -y
```
2. APT Packages
```bash
sudo apt install -t kali-rolling wifiphisher -y
sudo apt install -t kali-rolling wifite -y
sudo apt install -t kali-rolling aircrack-ng -y
sudo apt install -t kali-rolling iperf -y 
sudo apt install -t kali-rolling bettercap -y
sudo apt install -t kali-rolling john -y
```
3. Git Tools
```bash
git clone --depth 1 https://github.com/v1s1t0r1sh3r3/airgeddon.git
cd airgeddon
sudo bash airgeddon.sh
```

#### How to BYOT on Parrot
1. APT Packages
```bash
sudo apt install wifiphisher
sudo apt install wifite
sudo apt install aircrack-ng
sudo apt install iperf
sudo apt install bettercap
sudo apt install john
```
2. Git Tools
```bash
git clone --depth 1 https://github.com/v1s1t0r1sh3r3/airgeddon.git
cd airgeddon
sudo bash airgeddon.sh
```
