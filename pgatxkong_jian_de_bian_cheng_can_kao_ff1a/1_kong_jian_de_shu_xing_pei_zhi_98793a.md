## 1\. 控件的属性配置项: {#1}

### 1) Control {#1-control}

**描述：**

指定使能pgATX控件的哪些功能。在缺省情况下，可以使用“[控件的OML解析器函数](3_kong_jian_de_oml_jie_xi_qi_han_65703a.md)”和“[控件的辅助函数](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\11_pgclasslive_7c7b3a.md#4)”。

**参数：**

Type：用bit位或操作组合多个值可以同时使能多种功能。控件目前支持以下功能：

1：使能对等通信节点功能。使能对等通信节点功能后“[控件的节点功能函数](..\fu_lu_1_ff1a_yang_li_cheng_xu\1_jian_dan_liao_tian_shi_ff08_xiang_xi_zhu_shi_ff0.md#2)”才能生效。

Update：是否启用在线升级。0为禁用，1为启用。缺省为启用。

Sandbox：设置中间件的沙盒目录路径。必须指定绝对路径且不能包含‘=’、‘;’字符。目录路径必须是存在的。

LogName：LOG文件的文件名前缀。

LogLevel0：第0级LOG信息打印开关。0为关闭，1为打开。缺省为打开。

LogLevel1：第1级LOG信息打印开关。0为关闭，1为打开。缺省为打开。

LogLevel2：第2级LOG信息打印开关。0为关闭，1为打开。缺省为关闭。

LogLevel3：第3级LOG信息打印开关。0为关闭，1为打开。缺省为关闭。

LogFileNum：LOG文件的最多保存个数。

LogFileSize：每个LOG文件的最大长度（字节）。

**示例(JavaScript)：**

// 使能控件的Node功能

pgAtx.Control = “Type=1”;

### 2) Node {#2-node}

**描述：**

配置节点的性能参数。

**参数：**

Type：节点类型。0为普通节点，1为登录服务器节点

Cert：证书文件的路径。作为登录服务器时必须指定此参数（请从本软件作者处获取证书）

MaxPeer：节点对象的最大数目，取值范围：1 ~ 32768

MaxGroup：组对象的最大数目，取值范围：1 ~ 32768

MaxObject：对象的最大数目，取值范围：1 ~ 65534

MaxMCast：组播句柄的最大数目，取值范围：1 ~ 65534

MaxHandle：常驻接口事件队列的最大长度，取值范围：1 ~ 65534

MaxNotify：常驻内部事件队列的最大长度，取值范围：1 ~ 65534

SKTBufSize0：消息流的Socket队列长度（报文个数），取值范围：1 ~ 32768

SKTBufSize1：音频流的Socket队列长度（报文个数），取值范围：1 ~ 32768

SKTBufSize2：视频流的Socket队列长度（报文个数），取值范围：1 ~ 32768

SKTBufSize3：文件流的Socket队列长度（报文个数），取值范围：1 ~ 32768

P2PTryTime：指定P2P穿透尝试的时间(秒)。如果超过这个时间后还不能穿透，则使用转发方式通信。本参数的有效值范围：

等于0：使用默认的P2P穿透尝试时间，默认为6秒。

大于0 且 小于等于 3600：使用本参数指定的P2P穿透尝试时间进行尝试。

大于3600：禁用P2P穿透，直接使用转发通信。

SocketMode：节点的Socket模式（同节点类型Type）

ParamMode：节点函数接口的参数模式。0为二进制（在C/C++编程中使用），1为OML格式。

SocketMDU：指定传输层的最大数据单元(Max Data Unit)，默认为1024字节，上限为1280字节。最大数据单元决定传输层发送数据包的大小。如果数据包太大了，遇到MTU比较小的网络时，将导致IP报文分片，传输性能降低。

Option：本节点实例的选项，分别为以下的掩码组合：

0x01：启用网络异常时自动重新尝试登录（客户端有效）

0x02：启用集群模式的P2P穿透握手机制（服务器端有效）

0x04：启用踢出重复登录的用户功能（服务器端有效）

0x08：启用节点协助转发功能的握手功能（服务器端有效）

**示例(JavaScript)：**

// 指定该节点为服务器和最大的对象数目。如果不指定某个参数的值，则使用系统的缺省值。

pgAtx.Node = “Type=1;MaxObject=256”;

### 3) Local {#3-local}

**描述：**

配置节点的本地参数。

**参数：**

Name: 本地Peer对象的名称。如果该节点为普通节点，则不要指定本地Peer对象的名称。

Addr: 本地节点的网络地址。作为普通节点时，即使指定了本地地址，系统依然会根据服务器的地址选择合适的本地地址使用。只有无法根据服务器地址选择本地地址时，才会使用指定的本地地址。

FwdSpeed：设置本地节点的转发带宽（Kbps）。设置为0，则禁用本节点做转发。缺省为0。

**示例(JavaScript)：**

// 指定服务器节点的名称为“Server”，地址为“0:0:0:192.168.1.6:3000:0”

pgAtx.Local = “Name=Server;Addr=0:0:0:192.168.1.6:3000:0”;

### 4) Server {#4-server}

**描述：**

配置节点的服务器参数。

**参数：**

Name: 服务器Peer对象的名称。如果该节点为服务器，则不要指定服务器Peer对象的名称。也就是说只有作为客户端的时候才需要指定服务器Peer对象的名称。

Addr: 服务器节点的网络地址

Digest: 是否以摘要的方式发送登录密码。0为明文方式，1为摘要方式。如果启用摘要方式，则需要调用PG_METH_PEER_DigVerify方法对密码进行验证。

**示例(JavaScript)：**

// 指定服务器节点的名称为“Server”，地址为“0:0:0:192.168.1.6:3000:0”，以摘要方式发送密码

pgAtx.Server = “Name=Server;Addr=0:0:0:192.168.1.6:3000:0;Digest=1”;

### 5) Relay {#5-relay}

**描述：**

配置中继服务的器的隧道参数，可以同时指定多个隧道。节点会自动选择可用的隧道。参考“[配置和运行中继服务器](README.md)”章节

**参数：**

Type：中继转发的隧道协议类型。0为TCP隧道，1为HTTP隧道，2为WebSocket隧道（未支持）

Load：中继服务器的负荷

Addr：中继服务器的侦听地址

**示例(JavaScript)：**

// 指定2个隧道参数。第1个为HTTP隧道/IPV6地址，第2个为TCP隧道/IPV4地址。

pgAtx.Relay = “(Relay0){(Type){1}(Load){0}(Addr){FE800000:0:01B05996:42CFB70D:80:0}} (Relay1){(Type){0}(Load){0}(Addr){0:0:0:202.101.1.20:443:0}}”;

### 6) Class {#6-class}

**描述：**

指定使能的Peergine 功能类以及每种类的最大实例数。本配置项的格式为“类名称:类的最大实例数”，可以同时配置多个类，用分号“;”隔开。注：PG_CLASS_Peer 和PG_CLASS_Group类是系统的内建类，由系统在控件初始化时默认使能。

**参数：**

PG_CLASS_Data：消息传输类

PG_CLASS_File：文件传输类

PG_CLASS_Audio：音频传输类

PG_CLASS_Video：视频传输类

PG_CLASS_Board：白板共享类

PG_CLASS_Share：文件分块共享类

PG_CLASS_Table：数据表分发类

PG_CLASS_Live：媒体流直播类

**示例(JavaScript)：**

// 类名称的冒号后面的数字指定该类的最大实例数。

pgAtx.Class=“PG_CLASS_Data:8;PG_CLASS_File:16;PG_CLASS_Audio:4;PG_CLASS_Video:4”;

### 7) OnExtRequest {#7-onextrequest}

**描述：**

指定一个处理请求的回调函数。当控件接收到其他节点的请求时，通过此函数上报给应用程序，处理该请求。

**原型：**

int OnExtRequest(sObject, uMeth, sIn, uHandle, sPeer)

**参数：**

sObject: [字符串] 对象名称

uMeth: [整型] 操作方法，参考每种类型的方法定义。

sIn: [字符串] 请求的输入参数，OML格式

uHandle: [整型] 请求句柄，在ObjectExtReply()函数中返回控件。

sPeer: [字符串] 发出请求的对等节点

**返回值：**

[整型] -1: 异步处理，0: 成功，&gt;0: 失败的[错误码](#1)。如果返回值为-1，表示处理还没有完成，后续需要调用ObjectExtReply()函数发送应答。如果返回值大于等于0，则表示处理已经完成，返回值就是应答的错误码。

**示例(JavaScript)：**

function pgOnExtRequest(sObject, uMeth, sIn, uHandle, sPeer)

{

// TO DO …

pgAtx.ObjectExtReply(sObject, 0, “”, uHandle);

return -1;

}

pgAtx.OnExtRequest = pgOnExtRequest;

### 8) OnReply {#8-onreply}

**描述：**

指定一个处理应答的回调函数。当接收到异步操作应答时，系统调用该函数。

**原型：**

int OnReply(sObject, uErr, sOut, sParam)

**参数：**

sObject：[字符串] 对象名称

uErr：[整型] [错误码](#1)

sOut：[字符串] 应答的输出参数，OML格式

sParam：[字符串] 用户参数，就是在ObjectRequest()函数调用时输入的sParam参数。

**返回值：**

[整型] 0: 成功，&gt;0: 失败的[错误码](#1)。

**示例(JavaScript)：**

function pgOnReply(sName, uErr, sOut, sParam)

{

// TO DO ...

return 0;

}

pgAtx.OnReply = pgOnReply;