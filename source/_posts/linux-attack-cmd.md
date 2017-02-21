---
title: linux下简单shell攻击命令
date: 2017-02-15 20:55:02
tags: [linux, shell, attack]
categories: linux
---


### 发包命令
* udp发包命令：exec 3<>/dev/udp/ip/port; echo -e "test abc" >&3 // 发一个udp包
* tcp发包命令：exec 3<>/dev/tcp/ip/port;  // 发一个syn包
