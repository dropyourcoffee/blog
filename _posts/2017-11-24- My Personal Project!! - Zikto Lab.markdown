---
layout: post
title:  "MY PERSONAL PROJECT - Zikto Lab"
date:   2017-11-24 11:43:53 +0900
tags: Raspberry-Pi
categories: Linux/bash
---

I started up a small personal project, named Zikto Lab.

### Motivation
Activity tracking with wearable devices is being more generalised.
Basic trackings such as step counts, sleep tracking are available in most wearable devices, however
these activity tracking functionality is evolving into enhanced tracking with more insights to meet consumer demands.
Wearable devices with specialised purposes such as [walking posture detection](http://www.sportswearable.net/zikto-walk-is-an-activity-and-a-walking-posture-wearable/) or [recognising repetitive fitness exercise](https://www.youtube.com/watch?v=zpa4rVGlO68)
are good examples.

In order to develop such motion recognition algorithms, relevant data-sampling is a must, however there is no elegant solution available in public for many algorithm researchers
in organization without any internal development man-force. (Zikto has actually received few love calls from universities and research groups for collaboration).
The goal of this project is to build a web-based console platform that can communicate objects that supports BLE(Bluetooth Low Energy, or Bluetooth 4.0) to extract or analyse motional (inertial/angular speed) data collected by accelerometer and gyroscrope,
to let researchers in interest be able to focus on research with few or no efforts on concerning data-sampling environments.

### Project Overview

Zikto Lab is a BLE solution built in NodeJS, to sample datas from devices (BLE Peripherals).

The project consists of:
 - a Raspberry Pi (effectively a role of BLE beacon) running both as a BLE central (client role) and NodeJS application
 - a Zikto-Walk with customised firmware<br>
 (or possibly any kind of wearable device or evaluation kit that includes an IMU sensor and a BLE peripheral module)


The dashboard console will be implemented as a stand-alone NodeJS Web Application.
For the BLE central, I used a nodeJS module called [Noble](https://github.com/sandeepmistry/noble), developed by sandeepmistry.

I also customised an embedded firmware inside my company's product Zikto-Walk.

![Block Diagra(Prediction)]({{ site.baseurl }}/img/block_diagram.png)<br>

### Source

NodeJS part will be available on [public ziktoLab repository](https://github.com/dropyourcoffee/ziktoLab) on my github page, however the customised firmware will not be available yet.

For more inquiries, please email [dropyourcoffee@gmail.com](mailto:dropyourcoffee@gmail.com).

### Special Thanks

I give huge thanks to my CEO, Ted Kim, who happily supported allowance for intellectual properties of Zikto-Walk on this project.


