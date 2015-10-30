---
title: '检查端口是否已被监听'
description: 'check if port listened'
tag: linux,port,service
date: 2015-10-23 22:23
id: Cz3NeseT
---

Python检查端口是否被监听.

关于`socket.connect_ex`和`socket.connect`, 前者是返回状态值而不是抛出异常. 适合这种判断可连接的情景.

> Like connect(address), but return an error indicator instead of raising an exception for errors returned by the C-level connect() call

当然, 复杂的判断还可以增加连接后和服务的交互, 使用`send/sendall`来发送数据以及`recv/recvall`来接收数据.


    import socket

    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    result = sock.connect_ex(('127.0.0.1',80))

    if result == 0:
       print "Port is open"
    else:
       print "Port is not open"

    sock.close()

另外, [psutils](https://pypi.python.org/pypi/psutil)也可以在这里使用.
