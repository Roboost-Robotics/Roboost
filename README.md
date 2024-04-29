# Roboost

🤖 Roboost - Enabling Development of Cost-Effective Companion Robots 🤖

Welcome to the Roboost repository! This repository is the central hub for the Roboost project. It contains the documentation and links to all other repositories that are part of the project. Originally named after my robot models (Roboost V1 and V2), I've expanded its scope. Roboost is now a collection of repositories that are intended to make the development of companion robots more accessible. The project is still in its early stages, but I'm working hard to make the dream of a useful and affordable companion robot a reality. If you're interested in the project, feel free to reach out to me via using the contact information on the project [website](https://technologiehub.at/Roboost/).

Goals of the Roboost project:

- Minimize the development cost and time for companion robots
- Provide a modular software framework based on ROS2
  - Adaptable for different hardware setups
- Document the entire process of building a companion robot from the ground up
  - Including hardware, software, and integration with ROS2

Here is a little teaser of the Roboost-Mecanum robot with vector control. Documentation for this project can be found on the [project website](https://technologiehub.at/Roboost/) and soon in the docs folder of this repository.

![Roboost Demo](res/Roboost-Demo.gif "Roboost Demo")

## Overview

The Roboost project is a collection of multiple repositories, each handling a specific aspect of the robotic system. These repositories do not depend on each other and can be used independently. However, they are designed to work together seamlessly.

Each Roboost component mimics a brain region with a similar function. For instance, the low-level motor control component aligns with the Primary Motor Cortex in the brain. Just as this brain region handles executing motion commands that are received from "higher-level" regions, this component manages the intricacies of motion execution. The following sections provide a brief overview of each repository and its purpose.

### Cerebrum

Link to the repository: [Roboost Cerebrum](https://github.com/Roboost-Robotics/Roboost-Cerebrum)

🧠 Cerebrum: High-Level Decision Making 🤖

The Cerebrum repository contains all ROS2 packages that are used to run the Roboost robotic system. It is the central hub of the entire software stack and is responsible for all higher-level features. The Cerebrum repository is the only repo that is deployed to the robot itself and is not designed to run on a microcontroller, but rather on a board computer like a Radxa Rock 5B, Jetson Nano, or Raspberry Pi using Docker.

While it is currently in development, the Cerebrum repository will eventually handle the following tasks:

- Navigation
- Path Planning
- Obstacle Avoidance
- Object Detection
- Behavior Control
- ...

### Primary Motor Cortex

Link to the repository: [Roboost Primary Motor Cortex](https://github.com/Roboost-Robotics/Roboost-Primary-Motor-Cortex)

🏃‍♂️ Primary Motor Cortex: Low-Level Motion Control 🤖

The Primary Motor Cortex contains code related to the motor control of the robotic system. It is based on a PlatformIO project for an ESP32 and listens to the /cmd_vel topic in the ROS network. The received messages then are converted into individual motor speeds which then are used to control the given motors using different motor drivers and control algorithms.

### Entorhinal Cortex

Link to the repository: [Roboost Entorhinal Cortex](https://github.com/Roboost-Robotics/Roboost-Entorhinal-Cortex)

🛰️ Entorhinal Cortex: Low-Level Sensor Data Processing 🤖

The Entorhinal Cortex is a PlatformIO project that contains the firmware for an ESP32. It is responsible for reading sensor data (currently LiDAR, IMU, and battery-level) and publishing it onto the corresponding ROS topics.

## Further Resources

- [ROS2 Humble documentation](https://docs.ros.org/en/humble/)
- [Official micro-ROS documentation](https://micro.ros.org/)


### Embarrassingly Naive Vision for the Roboost Companion Robot:

*Design Aesthetic and Structural Features*:
- Inspired by a sleek, modern design (based on the [NEMO-2 submarine](https://nemo-submarine.com/)), the robot features a transparent dome that houses the camera and advanced sensors.
- LEDs encircle the camera dome, providing visual cues that reflect the robot’s emotional state.
- The robot is built for both indoor and outdoor use, equipped with three swerve drives with suspension, allowing omnidirectional movement across varied terrains.

*Communication and Emotional Expression*:
- The robot communicates through a combination of LED light patterns, animalistic sounds, and movement, all of which vary in response to its 'emotions'.
- Movement is an integral part of its communication; the robot's motions will change in speed, fluidity, and style to convey its feelings and intentions.

*Autonomy and Interaction*:
- The robot is designed to be curious and capable of autonomous exploration, learning about its environment as it moves.
- It is engineered to have a level of 'free will', enabling it to make choices about its behavior and interactions.

*Functionality*:
- It possesses the functionality to carry small items and navigate autonomously while avoiding obstacles.
- It includes environmental sensors that monitor and relay information about its surroundings, with user-friendly LED indicators.

*Learning and Adaptation*:
- The robot learns behaviors from its human companions through observation and interaction, in a manner akin to a pet learning from its owner.
- These learned behaviors and characteristics form a unique personality over time, allowing the robot to act as a bridge between generations, retaining and reflecting the mannerisms of its original companion.

*Objective*:
- The goal is to create a robot that not only serves practical functions but also forms emotional bonds with its users, adapting to their lifestyles and preferences.
- While providing utility and assistance, the robot is also intended to be a living memory of its human companions, adapting over time to create a seamless and personalized experience.

This vision statement should reflect the innovative and futuristic aspects of the robot, highlighting its functional utility, emotional interaction capabilities, and its potential to form a lasting legacy that connects past and future generations.
