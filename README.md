# ROSberryPi_Kinetic No Ubuntu
1.
```
sudo apt-get install dirmngr
```
2.
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
3.
```
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```
or
```
wget http://packages.ros.org/ros.key -O - | sudo apt-key add -
```
4.
```
$ sudo apt-get update
$ sudo apt-get upgrade
```
5.
```
$ sudo apt remove libboost1.67-dev
$ sudo apt autoremove
$ sudo apt install -y libboost1.58-dev libboost1.58-all-dev
$ sudo apt install -y g++-5 gcc-5
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 10
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 20
$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 10
$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 20
$ sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc 30
$ sudo update-alternatives --set cc /usr/bin/gcc
$ sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++ 30
$ sudo update-alternatives --set c++ /usr/bin/g++
$ sudo apt install -y python-rosdep python-rosinstall-generator python-wstool python-rosinstall build-essential cmake
```
6.Create a catkin Workspace
```
$ mkdir -p ~/ros_catkin_ws
$ cd ~/ros_catkin_ws
```
6.ROS-Comm: (recommended) ROS package, build, and communication libraries. No GUI tools.
```
$ rosinstall_generator ros_comm --rosdistro kinetic --deps --wet-only --tar > kinetic-ros_comm-wet.rosinstall
$ wstool init src kinetic-ros_comm-wet.rosinstall
```
7.Raspbian Buster:
```
$ cd ~/ros_catkin_ws
$ rosdep install -y --from-paths src --ignore-src --rosdistro kinetic -r --os=debian:buster
```
8.
```
sudo ./src/catkin/bin/catkin_make_isolated --install -DCMAKE_BUILD_TYPE=Release --install-space /opt/ros/kinetic
```
9.
```
$ echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
$ . ~/.bashrc
```
10. Updating the Workspace : Desktop: ROS, rqt, rviz, and robot-generic libraries
```
$ rosinstall_generator desktop --rosdistro kinetic --deps --wet-only --tar > kinetic-desktop-wet.rosinstall
$ wstool merge -t src kinetic-desktop-wet.rosinstall
$ wstool update -t src
$ rosdep install -y --from-paths src --ignore-src --rosdistro kinetic -r --os=debian:buster
$ sudo ./src/catkin/bin/catkin_make_isolated --install -DCMAKE_BUILD_TYPE=Release --install-space /opt/ros/kinetic
```
10.1 error install ros desktop
1. /home/pi/ros_catkin_ws/src/opencv3/modules/python/src2/cv2.cpp:885:34: error: invalid conversion from ‘const char*’ to ‘char*’ [-fpermissive]
     char* str = PyString_AsString(obj);
```
const char* str = PyString_AsString(obj);
```
2. Traceback (most recent call last):
  File "/opt/ros/kinetic/share/python_qt_binding/cmake/sip_configure.py", line 85, in <module>
    sip_dir, sip_flags = get_sip_dir_flags(config)
  File "/opt/ros/kinetic/share/python_qt_binding/cmake/sip_configure.py", line 65, in get_sip_dir_flags
    raise FileNotFoundError('The sip directory for PyQt5 could not be located. Please ensure' +
NameError: global name 'FileNotFoundError' is not defined