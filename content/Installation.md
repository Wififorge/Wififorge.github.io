# Docker Installation
After two years of development we have migrated WifiForge to Docker support only. Install from source at your own peril.

## Step 1: Install Docker
```bash
# Update system packages
sudo apt update -y

# Install Docker
sudo apt install docker.io -y
```

## Step 2: Install WifiForge Container
```bash
# Pull the latest WifiForge Docker image
sudo docker pull redblackbird/wififorge:wwhf
```

**Note**: Installing the Docker container can take up to an hour but averages 30 minutes.

## Step 3: Run WifiForge Container
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
  redblackbird/wififorge:wwhf /bin/bash
```

## Step 4: Start WifiForge
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
