# Instructions
## Raspberry Pi 4 (SBC) @TBot2

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

## Remote computer
Now, use the following commands in the SSH terminal (from remote PC to the RPi4) to setup the TurtleBot2. Notice that, here, you are basically making changes to the RPi4, not to the remote PC.
```
sudo apt install ros-humble-ecl-build
sudo apt install ros-humble-ecl-tools
sudo apt install ros-humble-kobuki-ros-interface
sudo apt install ros-humble-sophus
sudo apt install ros-humble-diagnostic-updater
sudo apt install ros-humble-xacro
sudo apt install ros-humble-joint-state-publisher
sudo apt install ros-humble-rmw-cyclonedds-cpp
```
The sophus needs some changes to avoid several warnings. Use following commands to apply them.
```
git clone https://github.com/CPrem95/sophusCorrection.git
sudo rm -r /opt/ros/humble/include/sophus
sudo cp -r ~/sophusCorrection/sophus /opt/ros/humble/include
```

Now, create a new workspace to work with the TBot2.
```
mkdir -p ~/tbot2_ws/src && cd ~tbot2_ws/src
```
Get all the necessary files from github.
```
git clone https://github.com/CPrem95/TBot2_Humble.git
```
Go back to the root of the workspace and build the package.
```
cd ..
colcon build --symlink-install --cmake-args -DCMAKE_CXX_FLAGS="-w"
```
Once everything is built, go back to the home directory and insert the following lines to the end of .bashrc file.

```
export ROS_DOMAIN_ID=30
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
```
With this, setting up the RPi4 and the remote computer is completed!!!

---
