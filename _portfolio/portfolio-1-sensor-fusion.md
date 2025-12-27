---
title: "Robotics Sensor Fusion and Navigation System"
excerpt: "ROS2 driver development & GPS/IMU data integration for robot navigation<br/><img src='/images/portfolio/sensor-fusion.jpg'>"
collection: portfolio
date: 2025-09-01
---

## Overview

Developed a comprehensive sensor fusion system for robot navigation as part of graduate coursework in Robot Sensing and Navigation (EECE 5554).

## Environment Setup

- Configured Ubuntu 24.04 development environment in VirtualBox with ROS2 Jazzy
- Set up Gazebo Harmonic simulation for testing navigation algorithms
- Integrated USB sensors with virtual machine through device passthrough

## Sensor Integration & Data Collection

- Developed ROS2 drivers for GPS (NMEA protocol) and IMU (VectorNav) sensors
- Implemented real-time data acquisition at 40Hz (IMU) and 1-10Hz (GPS)
- Created rosbag recording pipeline for synchronized multi-sensor data collection
- Configured guvcview and OpenCV for camera-based image recognition experiments

## Sensor Fusion & Navigation

- Implemented magnetometer calibration (hard/soft iron compensation) for heading estimation
- Developed complementary filter combining gyroscope integration with magnetometer readings
- Applied dead reckoning using accelerometer integration for velocity and position estimation
- Performed Allan Variance analysis to characterize IMU noise parameters (ARW, bias instability)

## Analysis Tools

- Built Python analysis pipeline for processing rosbag data
- Generated trajectory comparisons between GPS ground truth and IMU-based estimates
- Created visualization tools for sensor calibration and navigation performance evaluation

## Technical Skills

ROS2, Python, MATLAB, Ubuntu/Linux, VirtualBox, Gazebo, OpenCV, Sensor Fusion, GPS/IMU Integration, Kalman Filtering, Git
