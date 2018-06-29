## 5\. PG_CLASS_File类: {#5-pg-class-file}

### 1) 描述： {#1}

文件传输类。

### 2) 选项： {#2}

#### PG_ADD_FILE_TcpSock {#pg-add-file-tcpsock}

掩码：0x1

说明：从TCP Socket读取数据，以及写入数据到TCP Socket。

#### PG_ADD_FILE_Flush {#pg-add-file-flush}

掩码：0x2

说明：将所有接收到的数据写入到文件。

#### PG_ADD_FILE_PeerStop {#pg-add-file-peerstop}

掩码：0x4

说明：文件传输的对端Peer节点去同步时，停止文件传输。

### 3) 方法： {#3}

#### PG_METH_FILE_Put {#pg-meth-file-put}

ID：32

说明：上传文件

交互方式：[方式1](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#2-1)

发送请求参数：样例：(Path){c:\temp\xxxx.txt}(PeerPath){xxxx.txt}(TimerVal){3}(Offset){0}(Size){0}

Path：文件在本地的路径（受沙盒控制）。

PeerPath：指定文件在对端的路径。如果不指定此参数，则控件从Path参数中获取文件名作为此参数。

TimerVal：自动上报文件传输状态的周期（秒），0为不自动上报文件传输状态。

Offset：传输文件的起始位置（字节）

Size：传输文件的长度。0为传输到文件的末尾。如果Offset+Size超过文件的长度时，也传输到文件的末尾。

接收请求参数：样例：(PeerPath){xxxx.txt}(Offset){0}(Size){0}

PeerPath：指定文件在对端的路径

Offset：传输文件的起始位置（字节）

Size：传输文件的长度。0为传输到文件的末尾。如果Offset+Size超过文件的长度时，也传输到文件的末尾。

发送应答参数：样例：(Path){c:\MyDoc\xxxx.txt}(TimerVal){1}

Path：文件在本地的路径（受沙盒控制）。

TimerVal：自动上报文件传输状态的周期（秒），0为不自动上报文件传输状态。

接收应答参数：空

#### PG_METH_FILE_Get {#pg-meth-file-get}

ID：33

说明：下载文件

交互方式：[方式1](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#2-1)

发送请求参数：样例：(Path){c:\temp\xxxx.txt}(PeerPath){xxxx.txt}(TimerVal){3}(Offset){0}(Size){0}

Path：文件在本地的路径（受沙盒控制）。

PeerPath：指定文件在对端的路径。如果不指定此参数，则控件从Path参数中获取文件名作为此参数。

TimerVal：自动上报文件传输状态的周期（秒），0为不自动上报文件传输状态。

Offset：传输文件的起始位置（字节）

Size：传输文件的长度。0为传输到文件的末尾。如果Offset+Size超过文件的长度时，也传输到文件的末尾。

接收请求参数：样例：(PeerPath){xxxx.txt}(Offset){0}(Size){0}

PeerPath：指定文件在对端的路径

Offset：传输文件的起始位置（字节）

Size：传输文件的长度。0为传输到文件的末尾。如果Offset+Size超过文件的长度时，也传输到文件的末尾。

发送应答参数：样例：(Path){c:\MyDoc\xxxx.txt}(TimerVal){1}

Path：文件在本地的路径（受沙盒控制）。

TimerVal：自动上报文件传输状态的周期（秒），0为不自动上报文件传输状态。

接收应答参数：空

#### PG_METH_FILE_Status {#pg-meth-file-status}

ID：34

说明：查询或上报文件传输的状态

交互方式：[方式6](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#7-6)或[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：空

接收请求参数：样例：(Path){c:\temp\xxxx.txt}(PeerPath){xxxx.txt}(Speed){1056}(Status){2}(Request) {1}(Side){0}(Offset){0}(ReqSize){39946}(CurSize){27548}

Path：文件在本地的路径

PeerPath：对端文件路径

Speed：传输速率（字节/秒）

Status：文件传输的状态。1为开始传输(Start)，2为正在传输(Data)，3为结束传输(Stop)。

Request：请求的方法。0为GET，1为PUT

Side：传输的发送。0为接收，1为发送。

Offset：传输的起始位置（字节）

ReqSize：需要传输的总字节数

CurSize：当已经传输的字节数

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_FILE_Cancel {#pg-meth-file-cancel}

ID：35

说明：取消文件传输

交互方式：[方式4](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#5-4)

发送请求参数：空

接收请求参数：空

发送应答参数：无此操作

接收应答参数：无此操作

### 4) 常量：文件传输的状态 {#4}

#### PG_FILE_ST_Start {#pg-file-st-start}

ID：1

说明：开始传输

#### PG_FILE_ST_Data {#pg-file-st-data}

ID：2

说明：正在传输数据

#### PG_FILE_ST_Stop {#pg-file-st-stop}

ID：3

说明：结束传输