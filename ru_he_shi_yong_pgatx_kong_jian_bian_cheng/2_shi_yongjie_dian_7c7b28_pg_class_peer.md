## 2\. 使用节点类(PG_CLASS_Peer) {#2-pg-class-peer}

### 1) 创建节点对象 {#1}

动态节点对象：创建节点对象时不带任何选项，所创建的就是一个动态节点对象。在通信组对象添加成员时，如果该成员所对应的节点对象不存在，则系统自动创建一个对应的动态节点对象。所以，动态节点对象一般都由系统自动创建，无须直接调用控件的API创建。请参考“

使用通信组类

”章节。动态节点对象创建后，系统使用PG_METH_PEER_Status方法从登录服务器获取该节点的地址，并配置该动态节点对象的网络资源。

静态节点对象：创建静态节点对象使用PG_ADD_PEER_Static选项。静态节点对象不会从登录服务器获取地址，需要调用PG_METH_PEER_SetAddr方法来设置地址。

登录服务器节点对象：创建登录服务器节点对象使用PG_ADD_PEER_Server选项。在一个节点上只能有一个登录服务器节点对象，如果创建第二个，则前面一个自动销毁。在实际使用中不需要直接创建登录服务器节点对象，而是在控件初始化时，由系统自动创建。代码示例(JavaScript)：

pgAtx.Control = &quot;Type=1&quot;;

pgAtx.Node = &quot;Type=0&quot;; // 作为普通节点

pgAtx.Class = &quot;PG_CLASS_Data:8;PG_CLASS_File:64;PG_CLASS_Audio:8;PG_CLASS_Video:8&quot;;

pgAtx.Local = &quot;Addr=0:0:0:127.0.0.1:0:0&quot;;

**// Name参数指定登录服务器节点对象的名称，Addr参数指定登录服务器节点的地址。**

**pgAtx.Server = &quot;Name=PGServer;Addr=0:0:0:127.0.0.1:1112:0&quot;;**

pgAtx.Relay = &quot;(Relay0){(Type){1}(Load){0}(Addr){FE800000:0:01B05996:42CFB70D:7777:0}}&quot;;

pgAtx.OnExtRequest = pgOnExtRequest;

pgAtx.OnReply = pgOnReply;

pgAtx.Start(0);

节点自身对象：创建登录服务器节点对象使用PG_ADD_PEER_Self选项。在一个节点上只能有一个节点自身对象，如果创建第二个，则前面一个自动销毁。在实际使用中不需要直接创建节点自身对象，而是在控件初始化或调用登录方法时，有系统自动创建。

节点作为登录服务器节点(服务器端)时，在控件初始化时创建节点自身对象，代码示例(JavaScript)：

pgAtx.Control = “Type=1”;

pgAtx.Node = “Type=1”; // 作为登录服务器节点

**// Name参数指定节点自身对象的名称，Addr参数指定节点的地址。**

**pgAtx.Local = “Name= PGServer;Addr=0:0:0:127.0.0.1:1112:0”;**

pgAtx.OnExtRequest = pgOnExtRequest;

pgAtx.OnReply = pgOnReply;

pgAtx.Start(0);

节点作为普通节点(客户端)时，在调用登录方法时创建节点自身对象，代码示例(JavaScript)：

**// User参数指定节点自身对象的名称，节点的地址由系统自动分配。**

**var sData = &quot;(User){UserName000}(Pass){}(Param){}&quot;;**

var uErr = pgAtx.ObjectRequest(“PGServer”, 32, Data, &quot;Login&quot;);

### 2) 简单的两点直接通信 {#2}

为了便于开始理解节点对象，我们编写一个两点直接通信的程序。代码示例(JavaScript)：

&lt;object id=&quot;pgAtx&quot; classid=&quot;clsid:FFC9369F-A8D9-4598-8E22-ED07C7628BFC&quot; width=&quot;0&quot; height=&quot;0&quot;&gt;&lt;/object&gt;

&lt;script language=&quot;javascript&quot;&gt;

// 初始化控件实例。

pgAtx.Control = “Type=1”;

pgAtx.Node = “Type=1”;

pgAtx.Local = “Name=” + sLocalName + “;Addr=” + sLocalAddr;

pgAtx.OnExtRequest = pgOnExtRequest;

pgAtx.OnReply = pgOnReply;

pgAtx.Start(0);

// 创建对端节点对象，并设置地址。

pgAtx.ObjectAdd(sRemoteName, “PG_CLASS_Peer”, “”, 0x4);

var sInEle = “(Addr){“ + sRemoteAddr + “}(Proxy){}”;

pgAtx.ObjectRequest(sRemoteName, 37, sInEle, “SetAddr”);

// 给对端节点发送消息“Hello!”。

pgAtx.ObjectRequest(sRemoteName, 36, “Hello!”, “SendMsg”);

// 回调函数。

function pgOnExtRequest(sObj, uMeth, sData, uHandle, sPeer) {

if (sObj == sLocalName &amp;&amp; uMeth == 36) {

alert(sData); // 显示接收到的“Hello!”消息

}

}

function pgOnReply(sObj, uErr, sData, sParam) {

}

&lt;/script&gt;

但是，这个程序在实际中很难使用，因为要事先知道对端节点的网络地址。对此，Peergine提供了自动交换节点网络地址的方法，请看参考下文的“

登录、注销和地址解析

”章节。

### 3) 登录、注销和地址解析 {#3}

在Peergine系统中，通信节点是用节点对象的名称来标识的，但在通信过程中需要根据节点的网络地址来传输报文。所以，需要一种机制把节点对象名称转换成节点的网络地址（也称为地址解析）。Peergine提供了一种特殊的通信节点(登录服务器节点)，用来完成地址解析功能。在控件初始化时，把Node配置项的Type参数赋值为1，则该节点就是登录服务器节点。登录服务器节点比普通节点增加了以下几点功能：

(1) 接受其他普通节点的登录、验证账号和记录登录状态。

(2) 处理其他普通节点的地址解析请求，返回指定节点的地址信息和登录状态。

(3) 协助普通节点处理NAT穿越和中继隧道类型的协商。

普通节点通过调用登录服务器节点对象的PG_METH_PEER_Login和PG_METH_PEER_Logout方法来请求登录和注销。当在普通节点上创建了一个新的节点对象时，控件会自行调用登录服务器节点对象的PG_METH_PEER_Status方法来解析该节点的地址信息和登录状态。如果解析返回该节点已经登录，则与该节点建立通信会话。

**注：PG_METH_PEER_Login和PG_METH_PEER_Logout方法只能在登录服务器节点对象上调用，在其他节点对象上调用这两个方法将返回失败。**

### 4) 远程过程调用 {#4}

调用节点类的PG_METH_PEER_Call方法可进行两个节点之间的远程过程调用，该方法的请求参数和应答参数的内容由应用程序定义，控件透明传输。

### 5) 两点消息传输 {#5}

调用节点类的PG_METH_PEER_Message方法可进行两个节点之间的单向消息传输。该方法的请求参数的内容由应用程序定义，控件透明传输。

### 6) 数据的签名和校验 {#6}

调用节点类的PG_METH_PEER_DigGen方法产生数据的签名，调用节点类的PG_METH_PEER_DigVerify方法校验数据的签名。

### 7) 异常离线(掉线)的判断 {#7}

普通节点登录到服务器几点上后，由于网络中断、服务器关闭重启等，都会导致异常离线，也就是常说的掉线。在普通节点上需要及时判断异常离线，并尝试重新登录上线。原则上讲，普通节点与服务器节点之间通信时，如果中断或者访问超时，则说明异常离线了。下面以一段伪码说明如何判断异常离线：

// 假设服务器节点的节点名为：

var sObjSvr = “PGServer”;

// 假设需要登录的普通节点的节点名为：

var sObSelf = “123@peergine.com”;

// 在OnExtRequest 回调函数中

function OnExtRequest(sObj, uMeth, sData, uHandle, sPeer) {

// 自身节点与服务器节点之间的去同步事件

if (sObj == sObSelf) {

if (uMeth == 0) { // PG_METH_COMMON_Sync=0方法

var sAct = pgAtx.omlGetContent(sData, &quot;Action&quot;);

if (sAct != &quot;1&quot; &amp;&amp; sPeer == sObjSvr) {

// 异常离线了。如果设置了自动重新登录选项，则无需处理。

}

}

}

// 服务器节点事件

if (sObj == sObjSvr) {

if (uMeth == 0) { // PG_METH_COMMON_Sync=0方法

var sAct = pgAtx.omlGetContent(sData, &quot;Action&quot;);

if (sAct != &quot;1&quot;) { // 服务器节点的去同步事件

// 异常离线了。如果设置了自动重新登录选项，则无需处理。

}

}

else if (uMeth == 1) { // PG_METH_COMMON_Error=1方法

var sMeth = pgAtx.omlGetContent(sData, &quot;Meth&quot;);

if (sMeth &amp;&amp; parseInt(sMeth) == 32) { // PG_METH_PEER_Login= 32方法

// 服务器节点的登录方法，上报错误事件

// 异常离线了。如果设置了自动重新登录选项，则无需处理。

}

}

return 0;

}

}

// 在OnReply 回调函数中

function OnReply(sObj, uErr, sData, sParam) {

// 访问服务器节点时返回 PG_ERR_Network=11和PG_ERR_Timeout=12错误码。

if (sObj == sObjSvr) {

if (uErr == 11 || uErr == 12) {

// 登录失败。

// 需要调用PG_METH_PEER_Logout注销，然后再调用PG_METH_PEER_Login登录。

}

}

}