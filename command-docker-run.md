命令：docker run -d centos /bin/bash

都做了什么呢？

client 发命令给 dockerd

dockerd 通过rpc通知 containerd

containerd 通过rpc通知 shim

shim 直接调用runc 

runc init 调用命令 /bin/bash

再具体一点呢？

