---
title: '获取目录大小'
description: 'get directory size, like du -sh command'
tag: math,du
date: 2015-10-18 20:45
id: kGwwQWHK
---

Python获取目录的大小, 单位是byte. 类似于Linux的`du`命令: `du -sh .`

摘自 [Calculating a directory size using Python?](http://stackoverflow.com/a/1392549)

    import os
    def get_size(start_path = '.'):
        total_size = 0
        for dirpath, dirnames, filenames in os.walk(start_path):
            for f in filenames:
                fp = os.path.join(dirpath, f)
                total_size += os.path.getsize(fp)
        return total_size
