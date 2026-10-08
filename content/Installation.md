# Installation

WifiForge 4.0.0 can be run from a ready-made Docker image (recommended) or installed from source on Kali Linux.

## Option 1: Docker (Recommended)

The Docker image comes with mininet-wifi and every lab tool already installed. Each time the container starts it automatically:

- pulls the latest WifiForge code from GitHub,
- starts the Open vSwitch service that the labs need,
- clears out anything left over from a previous lab,

and then drops you into a shell in `/wififorge`.

### Step 1: Install Docker
```bash
# Update system packages
sudo apt update -y

# Install Docker and the X11 utilities used for lab windows (e.g. the browser)
sudo apt install -y docker.io x11-xserver-utils

# Start Docker
sudo systemctl start docker
```

### Step 2: Pull the WifiForge Image
```bash
sudo docker pull her3ticavi/wififorge:latest
```

**Note**: The image is large. The first download can take a while depending on your connection.

### Step 3: Run the WifiForge Container
```bash
# Allow the container to open windows on your desktop
xhost +local:root

# Create and start the container
sudo docker run --privileged=true -it \
  --env="DISPLAY" \
  --env="QT_X11_NO_MITSHM=1" \
  -v /tmp/.X11-unix:/tmp/.X11-unix:rw \
  -v /sys/:/sys \
  -v /lib/modules/:/lib/modules/ \
  --name mininet-wifi \
  --network=host \
  --hostname mininet-wifi \
  her3ticavi/wififorge:latest /bin/bash
```

You only run this command once. It creates a container named `mininet-wifi`.

### Step 4: Start WifiForge
Once inside the container:
```bash
wififorge
```

There is no need to change directories or start Open vSwitch yourself; the container does both when it starts.

### Starting the Container Again
After the first run, start the same container instead of creating a new one:
```bash
xhost +local:root
sudo docker start -ai mininet-wifi
```

Then run `wififorge`. The latest WifiForge code is pulled every time the container starts.

To start without pulling updates (for example, when offline), the container falls back to the copy it already has. You can also skip the update on purpose by adding `-e WIFIFORGE_AUTO_UPDATE=0` to the `docker run` command in Step 3.

### Troubleshooting

**`The container name "/mininet-wifi" is already in use`**: a container with that name already exists. Either start it with `sudo docker start -ai mininet-wifi`, or remove it and run Step 3 again:
```bash
sudo docker rm -f mininet-wifi
```

**`xhost: command not found`**: install it with `sudo apt install -y x11-xserver-utils`. It is only needed for labs that open a window, such as the browser.

**`repository name must be lowercase`**: Docker image names must be all lowercase (`her3ticavi/wififorge`, not `Her3ticAVI/wififorge`).

## Option 2: Install from Source (Kali Linux)

Installing from source is supported on Kali Linux, Debian and Ubuntu. Run every command below as root or with `sudo`.

### Step 1: Clone WifiForge
```bash
git clone -b 4.0.0 https://github.com/blackhillsinfosec/WifiForge.git
cd WifiForge
```

### Step 2: Install System Dependencies
This installs mininet-wifi and the wireless tooling the labs use. It can take 30 minutes or more.
```bash
sudo ./install-system-deps.sh
```

### Step 3: Install WifiForge
```bash
sudo pip install --break-system-packages .
```

### Step 4: Start WifiForge
```bash
sudo wififorge
```

WifiForge starts the Open vSwitch service automatically when it launches.

## Useful Options

| Command | What it does |
| :-- | :-- |
| `wififorge` | Open the lab menu |
| `wififorge --list` | List every lab and exit |
| `wififorge --allow-non-root` | Browse the menu without root (labs will not run) |
| `wififorge --version` | Show the installed version |
