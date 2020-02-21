# 开放式社交公共网络整体架构

&emsp;&emsp;开放式社交公共网络的底层通讯采用了基于DHT结构的P2P技术。每一家接入的企业都将以一个节点的形式接入到OSPN中。其结构图如下图所示

![image](/img/pic1.png)


&emsp;&emsp;企业作为节点接入需要三个部分，connector，IM服务（IMS），客户端（APP、小程序、或者web等等）。三者之间的关系如下图所示

![image](/img/pic2.jpg)

connector的作用是与其他企业的connector进行数据交换。

## 示例
我们以USER1首次发送跨界消息给USER2为例，数据流程如下图所示：

![image](/img/pic3.jpg)

IMS1代表USER1使用的IM服务。    
connector1代表与IMS1配套的服务。  
IMS2代表USER2使用的IM服务。  
connector2代表与IMS2配套的服务。  

1. USER1首次给USER2发送消息时会将消息发送给IMS1，IMS1发送寻人命令给connector1，connector1到OSPN网络里广播寻人。  
2. connector2收到广播找人消息以后会将命令发送给IMS2,IMS2判断USER2是否在自己的服务上。如果user2在线，IMS2才会去获取用户源列表。  
3. IMS1接收到获取用户列表命令以后发送关于某一用户的列表。  
4. USER2收到列表以后根据自己的需求，筛选所需消息，发送获取消息命令。  
5. IMS1接收到获取消息命令以后发送消息。  
6. USER2接收到消息以后验证签名，并发送回执。  
7. IMS1接收到回执，删除滞留的消息。
8. 建立了首次通信以后，双方只需要发送获取消息的命令即可完成消息发送与接收。

