# Hardware installation manual

## Geomaigc Touch/ Phantom Omni
```bash
sudo PHANToMConfiguration
mkdir catkin_ws
cd catkin_ws/
mkdir src
cd src/
catkin_init_workspace 
git clone git@github.com:WPI-AIM/ros_geomagic.git
cd ..
catkin_make
source devel/setup.bash 
roslaunch geomagic_control geomagic_headless.launch 
sudo chmod a+x /dev/fw*
roslaunch geomagic_control geomagic_headless.launch device_name:="Default PHANToM"

cd ambf/
cd external/chai3d/extras/hdPhantom/
ls
sudo ./linux-installation.sh 
```

If the Phantom Omni device was not recognised during the initialization.
Please try the following command again.

```bash
chmod a+rwx /dev/fw*
```

## Head Mount Display
We are using VIVE PRO for this project. 
From https://gitlab.freedesktop.org/monado/utilities/xr-hardware, download the config file, "70-xrhardware.rules."
copy to the directory, "/etc/udev/rules.dev" using the following command.
```bash
sudo cp 70-xrhardware.rules /etc/udev/rules.d/
```
You should alos check your group by command
```bash
id
```
You can add you to the group "plugdev" by the follwoing command:
```bash
sudo usermod -a -G plugdev <username>
```

Please refer to the follwing website: https://github.com/OpenHMD/OpenHMD/wiki/Xorg .

[Warning] If you create the 99-HMD.conf, the laptop screen will be disabled. Please be careful and be sure to have external monitor.

```bash
cd /usr/share/X11/xorg.conf.d/
sudo mv 99-HMD.conf 99-HMD.conf.bak # rename the file to enable your laptop screen
```

### Trouble shooting
If HMD was flipped use the follwing commmand to fix this issue:
**<your_output_monitor>** can be **DP-2** and you can flip with respect to any axis.
```bash
xrandr --output <your_output_monitor>  --reflect x
```
