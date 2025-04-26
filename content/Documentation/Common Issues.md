# Xterm does not work

## Error
You may receieve an error if you're using Kali Linux with XHost.

## Fix
Initializing graphical interfaces as root between the docker image and host machine is restricted on most modern distributions. Run the following command to provide the appropriate permissions - 
```bash
xhost si:localuser:root
```
If other issues are encountered, start a thread in the issues section of the repo.

# Dockerfile stops at apt update
## Error
The Dockerfile stops and hangs/breaks at apt update.

## Fix
Once in a while, the dockerfile will fail before installing packages. Though unconfirmed, this error usually occurs after running WifiForge (either on baremetal or within a docker). Rebooting and running the Dockerfile again typically solves the issue. 