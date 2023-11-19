# TBot2_Humble

Connect your RPi4 SBC to a suitable power supply and a monitor.

After booting, Change the **WiFi credentials** as guided in the lab sheet.

Open the **.bashrc** file:
```
nano .bashrc
```

Insert the following line to avoid sourcing ros environment every time:
```
source /opt/ros/humble/setup.bash
``` 
