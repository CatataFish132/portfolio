+++
title = "ROS2 Autonomous Waypoint Robot"
description = ""
weight = 1
date = 2021-06-10

[extra]
tags = ["ROS2", "Gazebo", "python", "C++"]
+++
{{ video(src="video.mp4", autoplay=true) }}
# Introduction
Developed a differential-drive (two-wheel with caster) mobile robot capable of autonomous waypoint navigation and real-time obstacle avoidance. The project bridged the gap between virtual prototyping and physical hardware by first building a complete physics simulation in Gazebo and then deploying the control stack directly onto a physical robot.
# Project Details
- **Core Tech:** ROS2 (Robot Operating System), Gazebo (Physics Simulator), Python/C++.
- **Hardware:** Differential-drive mobile platform (2 active drive wheels, 1 passive roller/caster wheel), 3x infrared/ultrasonic distance sensors (front-facing).
- **Concepts:** Robot kinematics, state machines, sensor fusion, obstacle avoidance algorithms.
# Key Features & Actions
- **Virtual Prototyping (Gazebo):** Designed a 3D simulation of the robot in Gazebo, defining its physical properties (mass, friction, wheel torque) and sensor limits to test navigation.
- **ROS2 Control Stack:** Built modular ROS2 nodes to handle sensor data acquisition, waypoint tracking, and wheel velocity commands ($/cmd\_vel$), utilizing ROS2 topics and parameters for clean node communication.
- **Reactive Obstacle Avoidance:** Programmed an algorithm that analyzed the three front-facing distance sensors to dynamically adjust the robot's heading when obstacles were detected.
- **Waypoint Navigation State Machine:** Created a coordination system that calculated the distance and heading to a target coordinate, smoothly driving the robot forward while actively overriding the trajectory if an obstacle crossed its path.