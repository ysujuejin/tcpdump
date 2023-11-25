# tcpdump
analyze three abnormal cases in a TCP connection
##  研究三次握手异常情况，首先需要学会一个正常的TCP连接怎么用命令行敲出来！！！

*  首先找一个合适的监听端口，由于网络通信的端口范围是0~65535，且49152到65535属于私有端口，可供客户端应用程序临时使用，所以这里选择49152端口！！！为了以防万一，我还是希望看看49152端口是否被别的进程占用，于是输入以下命令：

```
lsof -i :49152
```
 
######                   <center> 发现输出是空，说明没有进程占用这个端口</center>
* 打开一个终端，输入以下命令，让主机监听49152端口，充当服务器
```
nc -l -p 49152
```
它的结果如下：
![](https://markdown.liuchengtu.com/work/uploads/upload_87dfcee5ecbe4f4c0b4504170e93a70a.png#pic_center)
* 再打开一个终端，监控tcp三次握手，输入以下命令,得到的结果如下：

```
sudo tcpdump -i any port '49152' -XX -nn -vv
```
![](https://markdown.liuchengtu.com/work/uploads/upload_5e4d815706fcbb1ec7da7235ede39cfb.png)
* 最后打开又一个终端，模拟客户端，与服务器建立连接，输入以下命令，执行后立刻观察监控终端的变化,没用自己的图，但是最后的输出结果类似

```
nc -v 127.0.0.1 49152
```
![](https://markdown.liuchengtu.com/work/uploads/upload_82feecedfffa002bd869cadeaad52992.png)
![](https://markdown.liuchengtu.com/work/uploads/upload_4cba857e019776921246dbfa06006ba7.png)
### 客户端和服务器之间有了三次握手过程，建立了连接！！！
