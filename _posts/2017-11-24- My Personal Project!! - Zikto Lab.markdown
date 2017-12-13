---
layout: post
title:  "MY PERSONAL PROJECT - Zikto Lab"
date:   2017-11-24 11:43:53 +0900
tags: Raspberry-Pi NodeJS PersonalProject
categories: ZiktoLab
---

I started up a small personal project, named Zikto Lab.

### Motivation
Activity tracking with wearable devices is being more and more generalised.
Basic trackings such as step counts, sleep tracking are available in most wearable devices, however
functionally enhanced activity tracking with more insights (eg. [walking posture](http://www.sportswearable.net/zikto-walk-is-an-activity-and-a-walking-posture-wearable/), [recognising repetitive fitness exercise](https://www.youtube.com/watch?v=zpa4rVGlO68))
needs preliminary researches.

In order to develop such motion recognition algorithms, data-sampling is a must, however there is no development environments available in public.
The goal of this project is to build a web-based console platform that can manipulate BLE peripherals to extract or analyse collected inertial/angular speed data collected by accelerometer and gyroscrope,
to let researcher(s) in interest be able to focus on research with few or no efforts on concerning data-sampling environments.

### Project Overview
The project consists of:
 - a Raspberry Pi (effectively a role of beacon) running as both as a BLE server(central) and NodeJS application
 - a Zikto-Walk with customised firmware<br>
 (or possibly any kind of wearable device or evaluation kit that includes an IMU sensor and a BLE peripheral module)


The dashboard console will be implemented as a stand-alone NodeJS Web Application.
For the BLE central, I used a nodeJS module called [Noble](https://github.com/sandeepmistry/noble), developed by sandeepmistry.

I also customised an embedded firmware inside my company's product Zikto-Walk (a huge thanks to our CEO Ted Kim who happily supported on this project)

![Block Diagra(Prediction)]({{ site.baseurl }}/img/block_diagram.png)<br>

### Source

NodeJS part will be available on [public ziktoLab repository](https://github.com/dropyourcoffee/ziktoLab) on my github page, however the customised firmware will not be available yet.

For more inquiries, please email [dropyourcoffee@gmail.com](mailto:dropyourcoffee@gmail.com).

---
#### Update on 2017-12-13
Uploaded milestone 1 and demo.
[See Post]({{ site.baseurl }}/ziktolab/2017/12/13/Zikto-Lab-Milestone1.html)


