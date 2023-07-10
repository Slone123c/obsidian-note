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
```c++
#include <stdexcept>  
  
#include "byte_stream.hh"  
  
using namespace std;  
  
ByteStream::ByteStream(uint64_t capacity) : capacity_(capacity) {}  
  
void Writer::push(string data) {  
// Your code here.  
(void) data;  
uint64_t data_length = data.length();  
if (data_length > capacity_ - buffer_.size()) {  
data_length = capacity_ - buffer_.size();  
}  
write_count_ += data_length;  
for (uint64_t i = 0; i < data_length; i++) {  
buffer_.push_back(data[i]);  
}  
}  
  
void Writer::close() {  
// Your code here.  
input_ended_flag_ = true;  
}  
  
void Writer::set_error() {  
// Your code here.  
has_error_ = true;  
}  
  
bool Writer::is_closed() const {  
// Your code here.  
return input_ended_flag_;  
}  
  
uint64_t Writer::available_capacity() const {  
// Your code here.  
if (buffer_.size() >= capacity_) {  
return 0;  
}  
return capacity_ - buffer_.size();  
}  
  
uint64_t Writer::bytes_pushed() const {  
// Your code here.  
return write_count_;  
}  
  
string_view Reader::peek() const {  
// Your code here.  
if (buffer_.empty()) {  
return std::string_view();  
}  
return std::string_view(&buffer_.front(), 1);  
} 
  
bool Reader::is_finished() const {  
// Your code here.  
return input_ended_flag_ && buffer_.size() == 0;  
}  
  
bool Reader::has_error() const {  
// Your code here.  
return has_error_;  
}  
  
void Reader::pop(uint64_t len) {  
// Your code here.  
(void) len;  
uint64_t data_length = len;  
if (data_length > buffer_.size()) {  
data_length = buffer_.size();  
}  
read_count_ += data_length;  
while (data_length--) {  
buffer_.pop_front();  
}  
}  
  
uint64_t Reader::bytes_buffered() const {  
// Your code here.  
return buffer_.size();  
}  
  
uint64_t Reader::bytes_popped() const {  
// Your code here.  
return read_count_;  
}
```
