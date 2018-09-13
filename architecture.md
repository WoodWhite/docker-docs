```
# ps -ef|grep docker|grep -v grep
root      2745     1  0 11:51 ?        00:00:22 /usr/bin/dockerd
root      2752  2745  0 11:51 ?        00:00:37 docker-containerd --config /var/run/docker/containerd/containerd.toml
root      3008  2752  0 11:51 ?        00:00:00 docker-containerd-shim -namespace moby -workdir /var/lib/docker/containerd/daemon/io.containerd.runtime.v1.linux/moby/dafe6a9f7e08be2d8a414cd0704c483f5c85bba0e5b3a90a48f049207f42684e -address /var/run/docker/containerd/docker-containerd.sock -containerd-binary /usr/bin/docker-containerd -runtime-root /var/run/docker/runtime-runc
```

```
# ll /usr/bin/docker*
-rwxr-xr-x 1 root root 33069608 Aug 22 01:26 /usr/bin/docker
-rwxr-xr-x 1 root root 38088856 Aug 22 01:25 /usr/bin/docker-containerd
-rwxr-xr-x 1 root root 20895160 Aug 22 01:25 /usr/bin/docker-containerd-ctr
-rwxr-xr-x 1 root root  4173632 Aug 22 01:25 /usr/bin/docker-containerd-shim
-rwxr-xr-x 1 root root 68608880 Aug 22 01:26 /usr/bin/dockerd
-rwxr-xr-x 1 root root   849224 Aug 22 01:24 /usr/bin/docker-init
-rwxr-xr-x 1 root root  2411096 Aug 22 01:26 /usr/bin/docker-proxy
-rwxr-xr-x 1 root root  7639448 Aug 22 01:26 /usr/bin/docker-runc
```


# Docker 组件

- docker
- docker-containerd-ctr
- dockerd
- docker-containerd
- docker-containerd-shim
- docker-runc
- docker-init
- docker-proxy

# Docker 组件关系
```
docker     ctr
  |         |
  V         V
dockerd -> containerd ---> shim -> runc -> runc init -> process
                      |-- > shim -> runc -> runc init -> process
                      +-- > shim -> runc -> runc init -> process
```

docker： dockerd 的 client。

docker-containerd-ctr：docker-containerd 的 client。

dockerd：docker engine 守护进程。

docker-containerd：dockerd 启动时会启动 docker-containerd 子进程，dockerd 和 docker-containerd 之间通过rpc通信。

docker-containerd-shim：containerd 通过 shim 直接调用 runc 的包函数，shim 与 containerd 之前通过rpc通信。

docker-runc：runc 真正控制容器生命周期，用户想启动的容器内进程由 runc 的 init 进程启动。

docker-init：

docker-proxy：



