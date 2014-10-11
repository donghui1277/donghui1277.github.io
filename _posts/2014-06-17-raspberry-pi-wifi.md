---
layout: post
title: "树莓派无线上网设置"
description: "树莓派 wifi"
category: geek
tags: [raspberry pi]
modified: 2014-06-17

imagefeature: Edge_of_Tomorrow.jpg
comments: true
share: true
---
由于学校的校园网是限制一个学号一个ip登录，所以电脑登录后，树莓派就没有办法上网了。

于是上网买了一个无线网卡，经过浏览，发现那种mini的基本都比较便宜，但是都是只支持150M。经过选择，确定了TP-LINK的TL-WN823N，快递，06-13 01：14：59下的订单，今天17号才送到。

拿到后回来，插上后ssh登录，lsusb显示识别正常。

STEP 1
----
修改/etc/network/interfaces内容

原来内容

    auto lo
    
    iface lo inet loopback
    iface eth0 inet dhcp
    
    allow-hotplug wlan0
    iface wlan0 inet manual
    wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
    iface default inet dhcp

修改后为

    auto lo
    
    iface lo inet loopback
    iface eth0 inet dhcp
    
    allow-hotplug wlan0
    auto wlan0
    iface wlan0 inet manual
    wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
    iface default inet dhcp

STEP 2
----
修改/etc/wpa_supplicant/wpa_supplicant.conf

原来为

    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1

修改为

    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1

    network={
        ssid="无线网络名称"
        psk="无线网络密码"
        proto=RSN
        key_mgmt=WPA-PSK
        pairwise=CCMP TKIP
        group=CCMP TKIP
    }

然后sudo reboot就行了，记得拔掉网线。
