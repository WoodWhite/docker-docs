centos 7.x

不使用docker 命令行，直接调用 docker engine api

```
# vi /usr/lib/systemd/system/docker.service
ExecStart=/usr/bin/dockerd -H unix://var/run/docker.sock -H tcp://0.0.0.0:2375

systemctl daemon-reload

systemctl restart docker

netstat -ntlp|grep 2375

```
docker engine api使用文档详见 docker官网。
