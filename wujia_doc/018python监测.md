## Python监测删除



```python
'''
Description: henggao_learning
version: v1.0.0
Author: henggao
Date: 2020-12-18 16:33:01
LastEditors: henggao
LastEditTime: 2020-12-18 16:49:15
'''
# -*- coding: utf-8 -*-

#
# 开线程检测文件夹大小，超过指定大小，则按文件最后修改时间排序并删除一部分旧图片
# 在线程里每隔一段时间检测一次
#

import os
import threading
import time


# 文件按最后修改时间排序
def get_file_list(file_path):
    dir_list = os.listdir(file_path)
    if not dir_list:
        return
    else:
        dir_list = sorted(dir_list, key=lambda x: os.path.getmtime(
            os.path.join(file_path, x)))
        # print(dir_list)
        return dir_list

# 获取文件夹大小


def get_size(file_path):
    totalsize = 0
    for filename in os.listdir(file_path):
        totalsize = totalsize + \
            os.path.getsize(os.path.join(file_path, filename))
    #print(totalsize / 1024 / 1024)
    return totalsize / 1024 / 1024

# 1文件目录   2文件夹最大大小(M)   3超过后要删除的大小(M)


def detect_file_size(file_path, size_Max, size_Del):
    print(get_size(file_path))
    if get_size(file_path) > size_Max:
        fileList = get_file_list(file_path)
        for i in range(len(fileList)):
            if get_size(file_path) > (size_Max - size_Del):
                print("del :%d %s" % (i + 1, fileList[i]))
                os.remove(file_path + fileList[i])


# 检测线程，每个5秒检测一次
def detectPicSize():
    while True:
        print('======detect============')
        # detect_file_size("../pic/", 30, 5)
        detect_file_size("./mongeostore_env/pic/", 30, 5)
        time.sleep(5)


if __name__ == "__main__":

    # 创建检测线程
    detect_thread = threading.Thread(target=detectPicSize)
    detect_thread.start()

```





```python
import os
import sys
import time
import datetime


def delDir(dir, t=120):
    # 获取文件夹下所有文件和文件夹
    files = os.listdir(dir)
    for file in files:
        filePath = dir + "/" + file
        # 判断是否是文件
        if os.path.isfile(filePath):
            # 最后一次修改的时间
            last = int(os.stat(filePath).st_mtime)
            # 上一次访问的时间
            #last = int(os.stat(filePath).st_atime)
            # 当前时间
            now = int(time.time())
            # 删除过期文件
            if (now - last >= t):
                os.remove(filePath)
                print(filePath + " was removed!")
        elif os.path.isdir(filePath):
            # 如果是文件夹，继续遍历删除
            delDir(filePath, t)
            # 如果是空文件夹，删除空文件夹
            if not os.listdir(filePath):
                os.rmdir(filePath)
                print(filePath + " was removed!")


if __name__ == '__main__':

    # 获取现在时间
    now_time = datetime.datetime.now()
    print(now_time)
    # 获取明天时间
    next_time = now_time + datetime.timedelta(days=+1)
    next_year = next_time.date().year
    next_month = next_time.date().month
    next_day = next_time.date().day
    # 获取明天3点时间
    next_time = datetime.datetime.strptime(str(
        next_year)+"-"+str(next_month)+"-"+str(next_day)+" 03:00:00", "%Y-%m-%d %H:%M:%S")
    print(next_time)
    # 获取距离明天3点时间，单位为秒
    timer_start_time = (next_time - now_time).total_seconds()
    print(timer_start_time)
    # 获取路径
    path = 'tem_data'
    # 获取过期时间
    # t = 20
    t = 3600*24
    # 获取定期清理时间
    ts = timer_start_time
    # ts = 20
    while True:
        delDir(path, t)
        time.sleep(ts)

```

