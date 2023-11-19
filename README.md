# Raspberry Pi 4 (SBC) @TBot2

Connect your RPi4 SBC to a suitable power supply and a monitor.

Your SD card already has ROS2 Humble. Therefore, no need to setup ROS2 there.

After booting, Change the **WiFi credentials** as guided in the lab sheet [provided PDF].

Install Cyclone DDS:
```
sudo apt install ros-humble-rmw-cyclonedds-cpp
```

Now, open and edit the **.bashrc** file:
```
nano .bashrc
```

Insert the following line to avoid sourcing ros environment every time:
```
source /opt/ros/humble/setup.bash
``` 

Insert the following line for ROS2 to freely discover and send messages between ROS2 nodes in the same physical network:
```
export ROS_DOMAIN_ID=30
``` 

Insert the following line to use the Cyclone DDS:

```
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
```
Finally, save the .bashrc file and exit.

---
**TIPS:**

You can use SSH from your remote computer to connect to the RPi4 after setting up the LAN. 

Use the following commands to install SSH in your remote computer:
```
sudo apt install openssh-client
```
```
sudo apt install openssh-server
```
In the RPi4:

Find the IP address:
```
sudo apt install net-tools
```
```
ifconfig
```

Open a new terminal and use the IP address of the RPi4 to connect using the remote computer. In the remote computer:
```
ssh ubuntu@<IP_ADDRESS_RPI4>
```
You have to enter the password of the RPi4: SUTD1234

Now, you can remotely interact with the RPi4 using the remote computer.

DO NOT CLOSE this terminal. This is where you remotely interact with the RPi4.
---

