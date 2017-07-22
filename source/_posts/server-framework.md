---
title: 后台服务框架
date: 2017-02-25 15:21:32
tags: ["server","framework"]
categories: svr_framework
---


设置服务器最大文件描述符个数，控制资源。
linux中是通过文件方式来管理系统的。因此，系统能够承载的tcp连接数和系统文件打开数目能力相关，对于linux，系统最多能够打开的文件数目可通过/proc/sys/fs/file-max查看。
使用select的方式，tcp最多只能打开1024各文件描述符；若使用poll，可以自己定义个数。

可设置服务端打开秒数符总数限制：
TCPServerNum + AcceptClientNum + UDPServerNum + TCPClientNum + OtherFdNum(std, 文件fd， mysql fd等)
