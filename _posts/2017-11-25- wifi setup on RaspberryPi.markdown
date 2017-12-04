---
layout: post
title:  "Wifi setup on Raspberry Pi"
date:   2017-11-26 11:43:53 +0900
tags: Raspberry-Pi PersonalProject
categories: ZiktoLab
---

Setting up wlan configuration on raspbery Pi.

### 1. Check Wifi device is recognized
{% highlight sh %}
sudo lsusb
{% endhighlight %}

### 2. Try Scanning with Wifi device
{% highlight sh %}
sudo iwlist wlan0 scan
{% endhighlight %}

### 3. Modify interface
Edit `wpa_supplicant.conf` to add network profile.

{% highlight sh %}
sudo vim /etc/wpa_supplicant/wpa_suplicant.conf
{% endhighlight %}

{% highlight sh %}
network={
  ssid=“AP_NAME”
  psk=“AP_PASSWORD"
}
{% endhighlight %}

Edit `interfaces` file.
{% highlight sh %}
sudo vim /etc/network/interfaces
{% endhighlight %}

{% highlight sh %}
auto lo
iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
auto wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
iface default net dhcp
{% endhighlight %}

<br>
wpa-roam :<br>
Reconfigure wifi setup automatically at reboot or wifi disconnect.<br>
If configuration above causes error(Some APs have troubles), try below:


{% highlight sh %}
auto lo
auto wlan0

iface lo net loopback
iface eth0 inet dhcp

allow-hotplug wlan0
iface wlan0 inet dhcp
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
iface default net dhcp
{% endhighlight %}

A more stable configuration, however need to reconnect manually when disconnected.

### 4. reboot and check
{% highlight sh %}
sudo reboot
sudo ifdown wlan0  # Response varies depending on status
sudo ifup wlan0
wpa_cli status  # Check status
{% endhighlight %}




