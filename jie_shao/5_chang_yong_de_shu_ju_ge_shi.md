## 5\. 常用的数据格式 {#5}

### 1) 地址的格式 {#1}

Peergine 系统中使用的地址格式为：X:X:X:X:Port:Info，其中4个X分别为32bit整数、HEX格式，Port为端口号，Info为选项信息(未使用)。此地址格式可以表示IPV4的地址端口和IPV6的地址端口。IPV4的地址端口样例：0:0:0:7F000001:80:0或0:0:0:127.0.0.1:80:0。IPV6的地址端口样例：FE800000:0:01B05996:42CFB70D:80:0。

IPV4和IPV6地址格式到Peergine地址格式的对应关系如下图：

IPV4地址到Peergine地址的对应关系

IPV6地址到Peergine地址的对应关系

### 2) 时间的格式 {#2}

Peergine系统中使用的时间格式为：YYYY-MM-DD,HH:MM:SS。样例：2011-10-22,18:20:09。

### 3) 文件摘要的格式 {#3}

Peergine 系统中使用的文件摘要格式为：SHA256算法生成，Base64编码。

### 4) 视频窗口的参数格式 {#4}

Peergine 系统中使用的视频窗口参数格式为：(PosX){0}(PosY){0}(SizeX){80}(SizeY){60}(Handle) {343454}。其中，PosX和PosY为视频左上角在窗口中的坐标，SizeX和 SizeY为视频的尺寸，Handle为窗口的句柄。