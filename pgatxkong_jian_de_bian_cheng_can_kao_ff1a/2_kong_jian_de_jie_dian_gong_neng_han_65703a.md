## 2\. 控件的节点功能函数: {#2}

### 1) int ObjectAdd(sObject, sClass, sGroup, uFlag) {#1-int-objectadd-sobject-sclass-sgroup-uflag}

**描述：**

增加一个对象。

**参数：**

sObject：[字符串] 对象的名称。注意：如果一个同名对象已经存在，则直接返回成功。

sClass：[字符串] 该对象的类型，参考“节点功能类的编程参考”章节。

sGroup：[字符串] 该对象关联的组。它是一个PG_CLASS_Peer或PG_CLASS_Group类型的对象的名称。为空表示不指定关联的组。

uFlag：[整型] 指定创建对象的选项标志，参考“节点功能类的编程参考”中的“标志”章节。

**返回值：**

[整型] 1: 成功，0: 失败。

**示例(JavaScript)：**

// 添加一个名为“OnlineGroup”的通信组对象。该对象的关联组为节点“Server”。

pgAtx.ObjectAdd(“OnlineGroup”, “PG_CLASS_Group”, “Server”, 0x1);

### 2) void ObjectDelete(sObject) {#2-void-objectdelete-sobject}

**描述：**

删除一个对象。

**参数：**

sObject：[字符串] 对象的名称

**返回值：**

无

**示例(JavaScript)：**

// 删除名为“OnlineGroup”的对象

pgAtx.ObjectDelete(“OnlineGroup”);

### 3) String ObjectGetClass(sObject) {#3-string-objectgetclass-sobject}

**描述：**

获取对象的类型。

**参数：**

sObject：[字符串] 对象的名称

**返回值：**

[字符串] 该对象的类型。

**示例(JavaScript)：**

// 获取名为“OnlineGroup”的对象的类型

var sClass = pgAtx.ObjectGetClass(“OnlineGroup”);

### 4) int ObjectSetGroup(sObject, sGroup) {#4-int-objectsetgroup-sobject-sgroup}

**描述：**

指定对象的关联组。

**参数：**

sObject：[字符串] 对象的名称

sGroup：[字符串] 该对象关联的组。它是一个PG_CLASS_Peer或PG_CLASS_Group类型的对象的名称。当此参数为空时，删除之前关联的组。

**返回值：**

[整型] 1: 成功，0: 失败。

**示例(JavaScript)：**

// 删除对象“OnlineGroup”的关联组

pgAtx.ObjectSetGroup(“OnlineGroup”, “”);

### 5) String ObjectGetGroup(sObject) {#5-string-objectgetgroup-sobject}

**描述：**

获取对象的关联组。

**参数：**

sObject：[字符串] 对象的名称

**返回值：**

[字符串] 该对象的组。

**示例(JavaScript)：**

// 获取对象“OnlineGroup”的关联组

var sGroup = pgAtx.ObjectGetGroup(“OnlineGroup”);

### 6) int ObjectSync(sObject, sPeer, uAction) {#6-int-objectsync-sobject-speer-uaction}

**描述：**

主动触发通信对象同步，也就是主动触发通信对象建立会话连接。

**参数：**

sObject：[字符串] 对象的名称

sPeer：[字符串] 对等节点名称。如果此参数为空，则与通信范围内的所有节点都进行同步。

uAction：[整型] 同步动作，1: 已同步，0: 去同步。

**返回值：**

[整型] 1: 成功，0: 失败。

**示例(JavaScript)：**

// 触发“OnlineGroup”对象在“Server”节点上进行同步。

pgAtx.ObjectSync(“OnlineGroup”, “Server”, 1);

### 7) int ObjectRequest(sObject, uMeth, sIn, sParam) {#7-int-objectrequest-sobject-umeth-sin-sparam}

**描述：**

发送一个请求操作。

**参数：**

sObject：[字符串] 对象的名称

uMeth：[整型] 请求的方法ID，参考类型的方法定义。

sIn：[字符串] 请求的输入参数。

sParam：[字符串] 用户定义参数，在OnReply()回调函数中原样返回。

**返回值：**

[整型] -1: 异步处理，0: 成功，&gt;0: [错误码](..\fu_lu_1_ff1a_yang_li_cheng_xu\1_jian_dan_liao_tian_shi_ff08_xiang_xi_zhu_shi_ff0.md)。如果返回-1，说明操作正在异步处理，等待处理完成后通过OnReply()回调函数上报结果。如果返回&gt;=0，则操作已经完成，返回值表示执行结果。

**示例(JavaScript)：**

// 给“Server”节点发送一个RPC请求。

// PG_CLASS_Peer类的PG_METH_PEER_Call方法的ID为35

pgAtx.ObjectRequest(“Server”, 35, “How are you?”, “SendCall”);

### 8) int ObjectExtReply(sObject, uErr, sOut, uHandle) {#8-int-objectextreply-sobject-uerr-sout-uhandle}

**描述：**

应答一个异步请求。

**参数：**

sObject：[字符串] 对象的名称

uErr：[整型] [错误码](..\fu_lu_1_ff1a_yang_li_cheng_xu\1_jian_dan_liao_tian_shi_ff08_xiang_xi_zhu_shi_ff0.md)。

sOut：[字符串] 应答的输出参数

uHandle：[整型] 请求句柄，由OnExtRequest()函数输入的uHandle参数。

**返回值：**

[整型] 0: 成功，&gt;0: 失败的[错误码](..\fu_lu_1_ff1a_yang_li_cheng_xu\1_jian_dan_liao_tian_shi_ff08_xiang_xi_zhu_shi_ff0.md)。

**示例(JavaScript)：**

// 应答一个请求。

pgAtx.ObjectExtReply(“Server”, 0, “I am fine.”, uHandle);

### 9) String ObjectEnum(sObject, sClass) {#9-string-objectenum-sobject-sclass}

**描述：**

枚举遍历指定类型的所有对象。

**参数：**

sObject：[字符串] 上一个对象的名称，起始的对象名称为空字符串。

sClass：[字符串] 对象的类型。

**返回值：**

[字符串] 下一个对象的名称，返回空字符串表示枚举结束。

**示例(JavaScript)：**

var sObj = &quot;&quot;; // 起始的对象名称为空

while (true) {

var sObjNext = pgAtx.ObjectEnum(sObj, &quot;PG_CLASS_Video&quot;);

if (sObjNext == &quot;&quot;) {

// 返回对象名为空时，结束枚举。

break;

}

alert(&quot;Object: &quot; + sObjNext);

sObj = sObjNext;

}

### 10) int PostMessage(sMsg) {#10-int-postmessage-smsg}

**描述：**

发送消息给控件的消息队列。控件处理消息后，会通过OnExtRequest()回调函数上报消息。上报的消息内容与发送的消息内容一致。

**参数：**

sMsg：[字符串] 任意字符串。

**返回值：**

[整型] 0: 成功，&gt;0: 失败的[错误码](..\fu_lu_1_ff1a_yang_li_cheng_xu\1_jian_dan_liao_tian_shi_ff08_xiang_xi_zhu_shi_ff0.md)。

**示例(JavaScript)：**

// 发送消息给控件。

pgAtx.PostMessage(“012345679acbdef”);

### 11) int PumpMessage(uLoop) {#11-int-pumpmessage-uloop}

**描述：**

处理控件的消息循环。控件与应用程序之间的交互需要通过消息队列投递消息。在没有界面线程的JavaScript容器（或者Java应用程序）中运行控件时，由于没有消息循环，不能与应用程序交互。这种情况下，可以在JavaScript容器的运行线程中主动调用PumpMessage()函数来处理消息。

**参数：**

uLoop：[整型] 0：每处理完一个消息后，该函数返回；1：该函数循环处理消息，直到进程退出前才返回。

**返回值：**

[整型] 1: 成功，0: 失败（收到WM_QUIT消息）。

**示例(JavaScript)：**

// 循环处理消息。

while (pgAtx.PumpMessage(0)) {

// TO DO

}

### 12) int Start(uOption) {#12-int-start-uoption}

**描述：**

启动节点功能

**参数：**

uOption：[整型] 选项，必须为0。

**返回值：**

[整型] 0: 成功，&gt;0: 失败的错误码。

**示例(JavaScript)：**

// 启动一个 Node的功能

pgAtx.Start(0);

### 13) void Stop() {#13-void-stop}

**描述：**

停止节点功能。（C++、JNI、Object-C接口封装的中间件支持此函数，ActiveX不支持此函数。）

重要：不能在OnExtRequest()和OnReply()回调函数中调用此Stop()函数。

**参数：**

无

**返回值：**

无

**示例(Java)：**

// 停止一个 Node的功能

Node.Stop();