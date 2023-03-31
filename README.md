# VSOMEIP
使用vsomeip三方库实现了基于someip协议的双机通信
@[TOC](目录)
## 1、目的
根据someip抓包信息分析，复现出当时的通信流程中的subscribe/notify部分
## 2、部署
*注：客户端与服务端需分别部署在ipv4不同的设备上*
### 2.1、总体结构
拉取项目后总体结构如下：
vsomeip_sub/notify

├─client------------------------------------>客户端文件

│  ├─CMakeLists.txt ------------------->编译文件

│  ├─sample-ids.hpp ------------------>设置服务实例事件id头文件

│  ├─subscribe-sample.cpp --------->客户端代码

│  └─vsomeip-subscribe.json ------->客户端配置文件

├─server----------------------------------->服务端文件

│  ├─CMakeLists.txt ------------------->编译文件

│  ├─sample-ids.hpp ------------------>设置服务实例事件id头文件

│  ├─notify-sample.cpp --------------->服务端代码

│  └─vsomeip-local.json -------------->服务端配置文件

├─coldon_allpass_ok_ivi.pcap ------> 待复现抓包信息

├─result.pcap ----------------------------> 复现抓包结果

└─README.md-------------------------->说明文档


### 2.2、运行环境
系统：Linux、Ubuntu
库：vsomeip、c++std标准库
### 2.3、修改配置文件
#### 2.3.1、vsomeip-subscribe.json客户端
将地址改为新客户端的ipv4地址：
```json
"unicast" : "192.168.254.129"
```
#### 2.3.2、vsomeip-local.json服务端
将地址改为新服务端的ipv4地址：
```json
"unicast" : "192.168.254.128"
```
## 3、运行
cd 进入代码所在路径；
创建文件夹build并进入，使用cmake编译代码；
```powershell
mkdir build
cd build
cmake -DENABLE_SIGNAL_HANDLING=1 ..
make
```
编译完成后使用各自的配置文件运行：
### 3.1、客户端
```shell
VSOMEIP_CONFIGURATION=../vsomeip-subscribe.json \
VSOMEIP_APPLICATION_NAME=subscribe-sample \
./subscribe-sample
```
### 3.2、服务端
```shell
VSOMEIP_CONFIGURATION=../vsomeip-local.json \
VSOMEIP_APPLICATION_NAME=notify-sample \
./notify-sample
```
## 4、结果
使用wireshark抓包：
因为测试使用的是两个不同的虚拟机进行通信，故对**VMware Network Adapter VMnet8**进行抓包
结果详见：
result.pcap
