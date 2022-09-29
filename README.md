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

## Used technologies
This simulation-framework is build on the open-source [CARLA Simlulatior](https://github.com/carla-simulator/carla) which allows to build a broad variety of simulations. <br/>
CARLA itself is build using a fork of [UnrealEngine](https://www.unrealengine.com/en-US) (Version 4.26) with modifications to the engine, cutting of some unneeded features and making it overall more suitable for its usecae.
