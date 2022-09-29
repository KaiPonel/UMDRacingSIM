Welcome to the Carla-Based Driverless UMD Simulation Framework
=============================================================

Welcome to the documenation of the Carla-Based Driverless UMD Simulation Framework!
This documenation includes a brief overview about the simulation and its architecture and explains how you can work with the simulation or set it up from scratch.

## Quick Start - Find what you need

This file explains the overall architecture of Carla itself and the container enviorment it has been deployed in. <br/>
*It is highly recommended to keep **reading this file first** in order to obtain a brief overview about the project and its structure*

If you have an enviorment setup and want to start working, please refer to the [User Documentation](User.md)

If you want to setup the simulation enviorment from scratch or need to make changes to the container please refer to the [Admin Documentation](Admin.md)

# About this Framework

## Purpose of the Project
The framework was build during a student project at the faculty for computer science at the OVGU Magdeburg. The goal of this project was to build a foundation on which the autonoumous behavior of the UMD Racing Car could be simulated and improved to achieve better results in future Driverless disciplines of the Formula Students competitions. 

## Current state of the Project
This project only includes a framework aswell as a sample script on which simulation can be build upon. The framework is fairly expensive in terms of computing costs which is why we decided to bundle it into Containers which can be run on the Computing Cluster of the OVGU. 

## Used technologies in the framework

### Quick Overview
- **[CARLA Simlulator](https://github.com/carla-simulator/carla)** - Base of our Framework
- **[UnrealEngine (4.26)](https://www.unrealengine.com/en-US)** - Foundation of the Carla Simulator
- **[Apptainer](https://apptainer.org/)** - Container Enviorment to run the Framework remotely on a computing cluster
- **[Ubuntu 20.04](https://releases.ubuntu.com/focal/)** - Required operation system for carla.


This simulation-framework is build on the open-source [CARLA Simlulatior](https://github.com/carla-simulator/carla) which allows to build a broad variety of simulations. <br/>
CARLA itself is build using a fork of [UnrealEngine](https://www.unrealengine.com/en-US) (Version 4.26) with modifications to the engine, cutting of some unneeded features and making it overall more suitable for its usecase.

### Carla: Packaged vs Unpackaged Version
If you have read the documenation of Carla you might have noted that there are two different "versions" of the projects. A tiny **packaged** version which allows the user to start writing scripts within minutes and an **unpackaged** version which has drastictly higher system requirements and takes longer to install.  <br/>

The difference is that using the unpackaged version you can make major changes to the carla simulation using the forked UnrealEngine editor, which is not available in the packaged version. This allows you to modify/add maps or vehicles. Some of these features are planned to be supported in the packaged version, but are not as of CARLA Version 0.9.13. <br/>
In this framework **only the unpackaged version of Carla is used**, which allows major changes to maps and the used vehicles as explained above.

## Running Carla & Container enviorment
Using the unpackaged version of the CARLA simulator a lot more computing ressources are necessary, compared to the packaged version. To build and run Carla you should fulfill the following requirements for a good user experience:
- **Ubuntu 18.04 or newer** <br/>
- **130gb disk space (200gb+ for building the simulation)**<br/>
- **Minimum of 6-8gb GPU Vram** - Using the following cards (or better) are suitable 1080Ti, 2070+, 3060+, 40XX <br/>
- **(Recommended) High amount of CPU Cores** - Especially when building the project for the first time, however also in some production workflows a high amount of CPU cores is beneficial to speed up loading times. <br/>

Due to these hardware requirements we decided to bundle the simulation in an [Apptainer](https://apptainer.org/) Container which can be run on the Computing Cluster of the OVGU and accessed from outside via a VNC Connection


