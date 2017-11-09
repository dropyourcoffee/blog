---
layout: post
title:  "Available hardwares on nRF52 SoC"
date:   2017-07-03 12:43:53 +0900
categories: Embedded nRF52
---




### Summary

 - CPU - Cortex-M4F
 - NVM - 512KB with NVMController which can be manipulated by provided library called pstorage.
 - SDRAM - 64KB
 - Oscillators - Existing RC oscillator(LFCLK) + HFCLK(32MHZ).  Doesn't need external xTal for RF.
 - Timer - 5 Available.
 - Serial - 1 UART + 3 more Serials for(I2C/ SPI)

[https://devzone.nordicsemi.com/blogs/792/new-features-in-nrf52/](https://devzone.nordicsemi.com/blogs/792/new-features-in-nrf52/)
