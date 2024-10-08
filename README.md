# FAST_LIO_LC


**FAST-LIO** (Fast LiDAR-Inertial Odometry) is a computationally efficient and robust LiDAR-inertial odometry package. It fuses LiDAR feature points with IMU data using a tightly-coupled iterated extended Kalman filter. But it doesn't have a loop closure module to eliminate the accumulated drift.

Therefore, this project implements the pose graph optimization with a radius-search-based loop closure module which refers to [FAST_LIO_SLAM](https://github.com/gisbi-kim/FAST_LIO_SLAM). And the pose and map in the iterated extended Kalman filter of FAST-LIO will be updated according to the optimization which is a key difference with [FAST_LIO_SLAM](https://github.com/gisbi-kim/FAST_LIO_SLAM).

All the packages have been modified in order to build the packages using catkin_make command . Git clone these files directly in order to run the simulation in UBUNTU 20.04  ROS Noetic version ( Compatible) & necessary changes might need to be done if used in other versions such as 18.04 or 20.04

- [FAST_LIO_LC](#fast_lio_lc)
  - [1. Prerequisites](#1-prerequisites)
  - [2. Build](#2-build)
  - [3. Quick test](#3-quick-test)
    - [3.1 For Velodyne 16](#31-for-velodyne-16)
  - [4. Example results](#4-example-results)
  - [Acknowledgements](#acknowledgements)

## 1. Prerequisites

- Ubuntu 20.04 and ROS Noetic
- PCL 
- Eigen 
- GTSAM
- All the above three can be git cloned/updated if required for the version mentioned .

## 2. Build

```bash
cd YOUR_WORKSPACE/src
git clone  https://github.com/Jayamvs369/fliolc.git
cd ..
catkin_make
```

## 3. Quick test

### 3.1 For Velodyne 16

You can test this project with [our data](https://drive.google.com/file/d/1NGTN3aULoTMp3raF75LwMu-OUtzUx-zX/view?usp=sharing) which includes `/velodyne_points`(10Hz) and `/imu/data`(400Hz).

```bash
roslaunch fast_lio mapping_velodyne.launch
roslaunch aloam_velodyne fastlio_velodyne_VLP_16.launch
rosbag play  T3F2-2021-08-02-15-00-12.bag  -r 2
```

> If you want to test the original FAST LIO (i.e. without the loop closure module), you can set `lc_enable` in the `mapping_velodyne.launch` to `false` and run following commands.
>
> ```bash
> roslaunch fast_lio mapping_velodyne.launch
> rosbag play  T3F2-2021-08-02-15-00-12.bag  -r 2
> ```


## Acknowledgements 
The LIO module refers to [FAST-LIO](https://github.com/hku-mars/FAST_LIO) and the pose graph optimization refers to [FAST_LIO_SLAM](https://github.com/gisbi-kim/FAST_LIO_SLAM).



