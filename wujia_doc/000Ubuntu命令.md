# 命令



```shell
#创建文件
touch 文件名 

#删除文件，删除一个文件或多个文件
rm 文件名 文件名  

#创建文件夹
mkdir 目录

#删除空文件夹
rmdir 目录名

#删除非空文件，参数-f表示force
rm -rf 目录名

#重命名文件（夹） / 移动文件（夹）到指定文件夹
#将文件file1更改文件名为file2
mv file1 file2

#将文件file1，移到目录 dir1下，文件名仍为 file1
mv file1 dir1   

#若目录dir2存在，则将目录 dir1，及其所有文件和子目录，移到目录 dir2 下，新目录名称为 dir1。若目录 dir2 不存在，则将dir1，及其所有文件和子目录，更改为目录 dir2。
mv dir1 dir2  

# 返回最近一次访问的目录
cd -

# 返回根目录
cd ~

# 查看端口进程
netstat -ntpl

# 即可重新启动
shutdown -r now 
# 过10分钟自动重启
shutdown -r 10
# 在时间为20:35时候重启
shutdown -r 20:35 

# 立刻关机（一般加-p 关闭电源）
halt   
# 立刻关机
poweroff 
# 立刻关机(root用户使用)
shutdown -h now 
# 10分钟后自动关机
shutdown -h 10 

# 关闭 node 服务
pkill node   

# 查看文件夹大小，cd到该目录下
du -sh

#查找文件
find / -name "X"
```



## 报错集合

### 1. 报错

```
Ubuntu Error: ENOSPC:System limit for number of file watchers reached
```

- 解决方法：

- 修改系统监控文件数量
  - Ubuntu

    ```
    sudo gedit /etc/sysctl.conf
    ```
  
  - 添加一行在最下面
  
      ```
      fs.inotify.max_user_watches=524288
      ```
  
  - 然后保存退出！
  
  - 执行
  
      ```
      sudo sysctl -p
      ```
  
  - 然后就解决了！



