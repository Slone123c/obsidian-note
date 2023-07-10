```shell
docker run --privileged -itd -p 50001:22 --name cs144-dev centos:latest /usr/sbin/init # 映射对应端口，并赋予systemctl权限

docker run --privileged -itd -p 50001:22 --name cs144-dev-v1 vidocqh/cs144:latest bin/bash

docker run --privileged -itd -p 50001:22 --name cs144-dev-v1 ubuntu:latest bash
```