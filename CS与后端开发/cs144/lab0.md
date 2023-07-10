```shell
docker run --privileged -itd -p 50001:22 --name cs144-dev centos:latest /usr/sbin/init # 映射对应端口，并赋予systemctl权限
```