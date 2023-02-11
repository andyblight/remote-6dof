# Software Implementation

This page is a record of how the software used on the controller and the configuration of supporting software was chosen.

Worked out a rough plan:

1. Get screen and RPi working.
2. Get Arduino working with joysticks with JSON output.

## Waveshare screen and Raspberry Pi setup

I installed Ubuntu Server 22.04.1 LTS (64-bit) using the RPi Imager tool.  The server image should run OK as the RPI 3A+ only has 512kB of RAM.
**Important note:** Click on the Gear icon on the Raspberry Pi Imager and setup the Wi-Fi network SSID and password before writing the image to the SD card.  This saves a lot of time later.

The screen and RPi worked was expected so that was a big relief.

Under-voltage messages appear regularly.  Changed USB plug tops until I found on that outputs 5.2V and now no more error messages.  Two others output 5.1V and 5.0V and these showed the under-voltage messages.

After logging in for the first time, I install my bash scripts:

```bash
cd ~
git clone https://github.com/andyblight/bash_scripts.git
cd bash_scripts
./install.sh ubuntu22.04lts
```

The log out and in again.  The colours for the prompt didn't work but the rest is fine.  I was also able to login remotely using SSH so this made things a lot easier.  Applied all updates.

```bash
upgrade.sh
```

There is not much spare RAM on this board. `top` shows

```text
MiB Mem :    422.9 total,     26.5 free,    139.7 used,    256.7 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    265.1 avail Mem
```

So whatever we run it needs to be minimal.

## ROS2

Installed according to instructions [here](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html#). Worked correctly once I re-installed the OS (had installed the 32-bit version by mistake).  Packages installed:

```bash
sudo apt install ros-humble-ros-base
```

Added this to the end of `~/.bash_aliases`.

```bash
# Add ROS2
. /opt/ros/humble/setup.bash
```

ROS2 basics setup OK.  No idea what else is needed so this is done.

## Arduino

