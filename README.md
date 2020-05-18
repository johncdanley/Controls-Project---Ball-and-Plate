# Ball and Plate Balancing
#### Angel Mendoza, Chen Hung Yang, Jonathan Gomez, Marco Machuca, John Danley
-----------------------------------------------------------------------------------------
## 1. Introduction
 **test** using **test2** dataset.

test

test

test

#### Table of Contents
- [1. Introduction](#1-Introduction)
- [2. Modeling](#2-Modelling)
- [3. Basic Algorithm](#3-Basic-Algorithm)
- [4. Controller Design and Simulations](#4-Controller Design and Simulations)
  - [4.1. test](#41-test)
  - [4.2. test](#42-test)
- [5. Checklist](#5-Checklist)
  - [5.1. EKF SLAM with Known Correspondence](#51-EKF-SLAM-with-Known-Correspondence)
  - [5.2. EKF SLAM with Unknown Correspondence](#52-EKF-SLAM-with-Unknown-Correspondence)
-----------------------------------------------------------------------------------------
## 2. Modelling
**CoppeliaSim** [test](http://google.com).

Each dataset contains five files:
* **Odometry.dat**: Control data (translation and rotation velocity)
* **Measurement.dat**: Measurement data (range and bearing data for visually observed landmarks and other robots)
* **Groundtruth.dat**: Ground truth robot position (measured via Vicon motion capture – use for assessment only)
* **Landmark_Groundtruth.dat**: Ground truth landmark positions (measured via Vicon motion capture)
* **Barcodes.dat**: Associates the barcode IDs with landmark IDs.

The data is processed in the following way:
* test
* test
* test
* test
* test

-----------------------------------------------------------------------------------------
## 3. Sensor Calibration
Vision system needs calibration:
* test
* test


<p align = "center">
  <img src = "doc/Odometry.png" height = "360px" style="margin:10px 10px">
</p>

-----------------------------------------------------------------------------------------
## 4. Controller Design and Simulations
test:
* test
* test

test

### 4.1. Subheading Test
test: **test**.

<p align = "center">
  <img src = "doc/EKF_Localization_known_correspondences.png" height = "360px" style="margin:10px 10px">
</p>

### 4.2. Subheading Test 2
test: **test**.

<p align = "center">
  <img src = "doc/PF_Localization_known_correspondences.gif" height = "360px" style="margin:10px 10px">
</p>

-----------------------------------------------------------------------------------------
## 5. EKF SLAM
EKF SLAM applies EKF to SLAM problem with the following features:
* Feature-based map (landmarks)
* Assume Gaussian noise for motion and measurement models
* Maximum Likelihood data association

### 5.1. EKF SLAM with Known Correspondence
Probabilistic Robotics Page 314: **Algorithm EKF_SLAM_known_correspondences**.

The overall process is not very smooth because of inaccurate odometry data and a lack of information in measurement (each measurement only observes single landmark). But with known correspondences, the algorithm can still converge.

<p align = "center">
  <img src = "doc/EKF_SLAM_known_correspondences.gif" height = "360px" style="margin:10px 10px">
</p>

### 5.2. EKF SLAM with Unknown Correspondence
Probabilistic Robotics Page 321: **Algorithm EKF_SLAM**.

The algorithm generates very similar estimate at the beginning compared with algorithm 5.1. However, with inaccurate odometry data, data association cannot work as expected and gives bad correspondences at the end, which degrades both landmark and robot state estimates.

<p align = "center">
  <img src = "doc/EKF_SLAM_unknown_correspondences.gif" height = "360px" style="margin:10px 10px">
</p>

-----------------------------------------------------------------------------------------
## 6. Checklist
test

<p align = "center">
  <img src = "doc/Graph_SLAM_known_correspondences.png" height = "600px" style="margin:10px 10px">
</p>

-----------------------------------------------------------------------------------------
