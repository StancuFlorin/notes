---
title: "Enable Wake-on-LAN in Ubuntu 22.04"
date: 2023-12-2
---

In order for Wake-on-LAN to function, your Ethernet card needs to be compatible with this feature. To determine if your Ethernet card supports Wake-on-LAN, start by identifying the name of your Ethernet interface. 

```bash
ip a
```

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether c0:3f:d5:69:15:2a brd ff:ff:ff:ff:ff:ff
    inet 192.168.50.164/24 metric 100 brd 192.168.50.255 scope global dynamic enp3s0
       valid_lft 82439sec preferred_lft 82439sec
    inet6 fe80::c23f:d5ff:fe69:152a/64 scope link
       valid_lft forever preferred_lft forever
```

MAC address: `c0:3f:d5:69:15:2a`, and the computer's network interface name is `enp3s0`. To access and modify the Wake-On-LAN settings, it is necessary to have the `ethtool` package installed.

```bash
sudo apt install ethtool -y
```

Next, ascertain whether the network card supports Wake-On-LAN:

```bash
sudo ethtool enp3s0
```

```bash
Settings for enp3s0:
    ...
        Speed: 1000Mb/s
        Duplex: Full
        Auto-negotiation: on
        master-slave cfg: preferred slave
        master-slave status: slave
        Port: Twisted Pair
        PHYAD: 0
        Transceiver: external
        MDI-X: Unknown
        Supports Wake-on: pumbg
        Wake-on: g
        Link detected: yes
```

`Wake-on: g` indicates that the Wake-on-LAN feature is activated. If you have `d` instead of `g`, the feature needs to be enabled with

```bash
sudo ethtool -s enp3s0 wol g
```

## systemd service

If the Wake-on-LAN settings are disabled after the server restarts, you can address this issue using systemd. Start by creating the `wol-enable` service using

```bash
sudo --preserve-env systemctl edit --force --full wol-enable.service
```

```
[Unit]
Description=Enable Wake-up on LAN

[Service]
Type=oneshot
ExecStart=/sbin/ethtool -s enp3s0 wol g

[Install]
WantedBy=basic.target
```

You need to replace `enp3s0` with your network interface name and enable the service with

```bash
sudo systemctl daemon-reload
sudo systemctl enable wol-enable.service
```

## Wake-on-LAN Client

I personaly use [Wolow](https://wolow.site) to wake-up my devices on LAN, but you can use any other app.

![wolow](/assets/img/posts/wolow-wake-up-on-lan-iphone-app.png)