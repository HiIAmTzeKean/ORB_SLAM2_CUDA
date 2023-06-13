# ORB_SLAM2_CUDA

Originally forked from [here](https://github.com/dusty-nv/ORB_SLAM2_CUDA). This repository was modified for usage ROS ORB-SLAM with dual USB Cameras implementation as a monocular node. The purpose of this modification is meant to support this [NTU URECA project](https://github.com/HiIAmTzeKean/Jetson-Nano-SLAM).

## Specifications

### Hardware tested

- Jetson Nano Developer Kit
- Logitech C910 1080P Webcam (2)

### Software tested

OS: Linux Ubuntu 18.04.6 LTS
Packages: Nvidia Jetpack 4.5.1-b17, DeepstreamSDK 5.1.0, OpenCV 4.1.0
ROS distribution: melodic

## Installation on Jetson Nano (From forked repo)

- Follow the official [getting started](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#intro) to have a working Nano with latest image.
- Install OpenCV **4.1.0** on Jetson Nano (the `3.3.0` version installed with the [default image](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write) has some issues). Following the instructions in [this page](https://pysource.com/2019/08/26/install-opencv-4-1-on-nvidia-jetson-nano/) worked well for me.
- Install dependencies:
  - Pangolin: follow the instructions [here](https://github.com/stevenlovegrove/Pangolin).
  - Eigen 3:
     ```
     sudo apt install libeigen3-dev
     ```
  - PCL for ROS:
    ```
    sudo apt-get install libopenni2-dev
    sudo apt-get install ros-melodic-pcl-ros
    ```

- Clone the `jetson_nano` branch of the code (with modified `CMakeLists` for OpenCV 4.1.0 and fixed [some compatability issues](https://github.com/raulmur/ORB_SLAM2/issues/451)):
```bash
git clone https://github.com/hoangthien94/ORB_SLAM2_CUDA.git ORB_SLAM2_CUDA
cd ORB_SLAM2_CUDA 
git checkout jetson_nano
```
- Build like normal:
```
chmod +x build.sh
./build.sh
```

- Additionally, to run ROS on Jetson Nano, first follow this [JetsonHacks' blog post](https://www.jetsonhacks.com/2019/10/23/install-ros-on-jetson-nano/) to install ROS on Nano. Then build this repo with:

```bash
cd /path/to/ORB_SLAM2_CUDA/
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:/path/to/ORB_SLAM2_CUDA/Examples/ROS
chmod +x build_ros.sh
./build_ros.sh
```

## Run ROS launch file for Monocular node

Change the vocabulary and camera settings file accordingly. The directory is set in the launch file, located at ```ORB_SLAM2_CUDA/Examples/ROS/ORB_SLAM2_CUDA/launch/ros_mono.launch```. Ensure that your current directory is above of ```ORB_SLAM2_CUDA```.

Then launch:

```bash
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:$PWD/ORB_SLAM2_CUDA/Examples/ROS
roslaunch $PWD/ORB_SLAM2_CUDA/Examples/ROS/ORB_SLAM2_CUDA/launch/ros_mono.launch
```
