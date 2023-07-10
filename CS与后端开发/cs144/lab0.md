```shell
docker run --privileged -itd -p 50001:22 --name cs144-dev centos:latest /usr/sbin/init # 映射对应端口，并赋予systemctl权限

docker run --privileged -itd -p 50001:22 --name cs144-dev-v1 vidocqh/cs144:latest bin/bash

docker run --privileged -itd -p 50001:22 --name cs144-dev-v1 ubuntu:latest bash
```

# 写一个 Byte Stream 类
**byte_stream.hh**
```c++
class ByteStream  
{  
protected:  
uint64_t capacity_ = 0;  
// Please add any additional state to the ByteStream here, and not to the Writer and Reader interfaces.  
std::deque<char> _buffer = {};  // 缓存双向队列用于存储数据
uint64_t _read_count = 0;  
uint64_t _write_count = 0;  
bool _input_ended_flag = false;  
bool _has_error = false;

// ....
```
