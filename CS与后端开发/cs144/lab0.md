```shell
docker run --privileged -itd -p 50001:22 --name cs144-dev centos:latest /usr/sbin/init # 映射对应端口，并赋予systemctl权限

docker run --privileged -itd -p 50001:22 --name cs144-dev-v1 vidocqh/cs144:latest bin/bash

docker run --privileged -itd -p 50001:22 --name cs144-dev-v1 ubuntu:latest bash
```

# 写一个 Byte Stream 类

## byte_stream.hh
```c++
class ByteStream  
{  
protected:  
uint64_t capacity_ = 0;  
// Please add any additional state to the ByteStream here, and not to the Writer and Reader interfaces.  
std::deque<char> _buffer_ = {};  // 缓存双向队列用于存储数据
uint64_t read_count_ = 0;  
uint64_t write_count_ = 0;  
bool input_ended_flag_ = false;  
bool has_error_ = false;

// ....
```

## byte_stream.cc
**writer push()**
```
void Writer::push( string data )  
{  
// Your code here.  
(void)data;  
uint64_t data_length = data.length();  
if (data_length > capacity_ - buffer_.size()) {  
data_length = capacity_ - buffer_.size();  
}  
write_count_ += data_length;  
for (uint64_t i = 0; i < data_length; i++) {  
buffer_.push_back(data[i]);  
}  
}
```

