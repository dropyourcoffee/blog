---
layout: post
title:  "nRF51/52 Checking Serial No. / MAC Address"
date:   2017-07-28 12:43:53 +0900
categories: Embedded/nRF52
---

Nordic softdevice provides APIS regarding BLE and MAC address on nRF51 and 52.
(function calls may be slightly different depending on the softdevice version).

#### 1. Get BLE MAC Address
{% highlight c %}

sd_ble_gap_address_get((*ble_gapp_addr_t))
{% endhighlight %}
<br>
#### 2. Change MAC Address

There are two ways; one is randomised mac, another is change as given address.

{% highlight c %}


(ble_gapp_addr_t).addr_type = BLE_GAP_ADDR_TYPE_RANDOM_PRIVATE_NON_RESOLVABLE // Random
sd_ble_gap_address_set(BLE_GAP_ADDR_CYCLE_MODE_AUTO,(*ble_gapp_addr_t));

// OR
(ble_gapp_addr_t).addr_type = BLE_GAP_ADDR_TYPE_PUBLIC // Fixed
sd_ble_gap_address_set(BLE_GAP_ADDR_CYCLE_MODE_NONE,(*ble_gapp_addr_t));

{% endhighlight %}
<br>
#### 3. How to check factory BLE address and H/W Serial No. using Segger and nrfjprog(nRFgo Studio)

MAC Address
{% highlight cmd %}
./nrfjprog --memrd 0x100000a4 --n 8 --family nrf52
{% endhighlight %}


H/W Serial No.
{% highlight cmd %}
./nrfjprog --memrd 0x1000005c --n 8 --family nrf52
{% endhighlight %}


ref :

[https://devzone.nordicsemi.com/question/49876/switching-between-random-and-normal-mac-address/](https://devzone.nordicsemi.com/question/49876/switching-between-random-and-normal-mac-address/)

[https://devzone.nordicsemi.com/question/43047/sd_ble_gap_address_set-works-for-normal-mode-only/](https://devzone.nordicsemi.com/question/43047/sd_ble_gap_address_set-works-for-normal-mode-only/])

[https://devzone.nordicsemi.com/question/1691/how-to-get-nrf51822-serial-number-and-hw-id-through-segger/](https://devzone.nordicsemi.com/question/1691/how-to-get-nrf51822-serial-number-and-hw-id-through-segger/)
