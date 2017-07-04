## 2\. PG_CLASS_Peer类: {#2-pg-class-peer}

### 1) 描述： {#1}

节点类。

### 2) 选项： {#2}

#### PG_ADD_PEER_Self {#pg-add-peer-self}

掩码：0x1

说明：指定该Peer对象为本地节点的自身对象

#### PG_ADD_PEER_Server {#pg-add-peer-server}

掩码：0x2

说明：指定该 Peer对象为登录服务器节点对象

#### PG_ADD_PEER_Static {#pg-add-peer-static}

掩码：0x4

说明：指定该 Peer对象为静态节点对象。静态节点对象要调用PG_METH_PEER_SetAddr方法设置地址后才能使用。

#### PG_ADD_PEER_Digest {#pg-add-peer-digest}

掩码：0x8

说明：登录的时候使用摘要方式发送密码。只能与PG_ADD_PEER_Serve选项组合使用。

#### PG_ADD_PEER_Disable {#pg-add-peer-disable}

掩码：0x10

说明：禁用该Peer节点的所有访问权限。后续可以使用PG_METH_PEER_AccessCtrl方法修改该Peer的访问权限。

### 3) 方法： {#3}

#### PG_METH_PEER_Login {#pg-meth-peer-login}

ID：32

说明：登录到服务器。登录成功后，系统会自动创建本地节点的自身对象，对象名就是用户名。

交互方式：

方式1

发送请求参数：样例：(User){NodeA}(Pass){****}(Param){}

User：用户名，就是客户端节点自身对象的名称

Pass：密码

Param：参数，由应用程序定义

接收请求参数：样例：(Addr){0:0:0:192.168.1.6}(User){NodeA}(Pass){****}(Param){}

Addr：登录节点的地址

User：登录用户名，就是客户端节点自身对象的名称

Pass：密码

Param：参数，由应用程序定义

发送应答参数：样例：(Expire){30}(Type){0}(Sess){}(Param){}

Expire：登录老化时间（秒）

Type：用户的类型，缺省为0（将来使用）

Option：选项，bit位掩码的组合。指定为0x01时，在登录应答完成后，内部删除该节点对象。

Sess：登录会话信息，由应用程序定义

Param：参数，由应用程序定义

接收应答参数：样例：(Type){0}(Sess){}(Parm){}

Type：用户的类型，缺省为0（将来使用）

Sess：登录会话信息，由应用程序定义

Param：参数，由应用程序定义

#### PG_METH_PEER_Logout {#pg-meth-peer-logout}

ID：33

说明：注销登录。注销后，系统会自动删除本地节点的Peer对象。

交互方式：[方式4](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#5-4)

发送请求参数：空

接收请求参数：样例：(User){NodeA}

User：注销登录的节点名称

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_Status {#pg-meth-peer-status}

ID：34

说明：根据节点对象的名称解析该节点的地址、代理地址和登录状态。此方法只有在组网中有多个登录服务器节点组成集群功能时使用。如果请求解析的节点和被解析的节点都登录到同一个登录服务器节点上，则此方法不会被调用。系统在控件内部处理完解析请求并返回应答，不会上报到应用程序。当请求解析的节点和被解析的节点登录在不同的登录服务器节点上时，系统调用此方法把请求上报给应用程序。由应用程序通过集群组网从被解析的节点所登录的登录服务器节点获取解析结果，并返回给请求解析的节点。

交互方式：

方式3

发送请求参数：无此操作（控件内部自行发送请求）

接收请求参数：样例：(User){NodeA}

User：指定节点对象的名称。

发送应答参数：样例： (Type){0}(Addr){0:0:0:192.168.1.6:1234:0} (Proxy){0:0:0:192.168.1.12:1112:0}

Type：用户的类型，缺省为0（将来使用）

Addr：指定节点的地址

Proxy：指定节点的Proxy地址

接收应答参数：无此操作（控件内部自行处理应答）

#### PG_METH_PEER_Call {#pg-meth-peer-call}

ID：35

说明：对指定节点对象执行一个RPC操作

交互方式：

方式1

发送请求参数：任意字符串，内容和格式由用户定义

接收请求参数：同发送请求参数

发送应答参数：任意字符串，内容和格式由用户定义

接收应答参数：同发送应答参数

#### PG_METH_PEER_Message {#pg-meth-peer-message}

ID：36

说明：给指定节点对象发送一个消息

交互方式：[方式4](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#5-4)

发送请求参数：任意字符串，内容和格式由用户定义

接收请求参数：同发送请求参数

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_SetAddr {#pg-meth-peer-setaddr}

ID：37

说明：设置节点对象的自身地址和代理地址

交互方式：

方式7

发送请求参数：样例：(Addr){0:0:0:192.168.1.6:1234:0}(Proxy){0:0:0:192.168.1.1:4567:0}

Addr：指定节点的地址

Proxy：指定节点的代理地址

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_GetInfo {#pg-meth-peer-getinfo}

ID：38

说明：获取节点对象的自身地址、代理地址和隧道地址。

交互方式：

方式5

发送请求参数：空

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Type){0}(Through){4}(Proxy){202.112.1.100:7781}(AddrLcl){67.89.2.10:56734}(AddrRmt){218.10.4.50:12345}(TunnelLcl){67.89.2.10:56734}(TunnelRmt){218.10.4.50:12345}(PrivateRmt){192.168.1.23:56721}

Type：节点类型，由服务器定义

Through：P2P连接通道的类型，参考“[P2P连接通道类型](#5-p2p)”章节。

Proxy：服务器节点的地址

AddrLcl：本端节点的登录地址

AddrRmt：对端节点的登录地址

TunnelLcl：本端节点的通道地址

TunnelRmt：对端节点的通道地址

PrivateRmt：本端节点的本地地址

#### PG_METH_PEER_DigGen {#pg-meth-peer-diggen}

ID：39

说明：产生数据的签名。

交互方式：

方式5

发送请求参数：样例：(Data){01234567890}(Value){}

Data：需要产生签名的数据（任意字符串）。

Value：（空）。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Data){}(Value){YHEm82O44Vhtn05wxue2V4w0TOTXBSZVu9u9Imip1S4=}

Data：（空）。

Value：产生的签名值（Base64格式）。

#### PG_METH_PEER_DigVerify {#pg-meth-peer-digverify}

ID：40

说明：校验数据的签名。

交互方式：

方式7

发送请求参数：样例：(Data){01234567890}(Value){YHEm82O44Vhtn05wxue2V4w0TOTXBSZVu9u9Imip1S4=}

Data：需要校验签名的数据。

Value：需要校验的签名值（Base64格式）。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_CheckInfo {#pg-meth-peer-checkinfo}

ID：41

说明：检查节点的状态信息。

交互方式：

方式7

发送请求参数：样例：(Check){}(Value){}(Opion){}

Check：检查类型。

Value：对比的值。

Opion：选项。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_LanScan {#pg-meth-peer-lanscan}

ID：42

说明：搜索同一个局域网内的P2P节点。

交互方式：

方式5

发送请求参数：样例：(Timeout){3}

Timeout：搜索等待的时间（秒）。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Size){2}(PeerList){(Peer0){192.168.1.2:7654}(Peer1){192.168.1.3:7654}}

Size：搜索到的节点个数。

PeerList：节点的地址信息列表

#### PG_METH_PEER_AgentLogin {#pg-meth-peer-agentlogin}

ID：43

说明：代理节点登录到服务器。登录成功后，系统会自动创建代理节点对象，对象名就是用户名。

交互方式：

方式1

发送请求参数：样例：(User){AgentUser1}(Pass){****}(Param){}

User：用户名，就是客户端节点自身对象的名称

Pass：密码

Param：参数，由应用程序定义

接收请求参数：样例：(User){AgentUser1}(Pass){****}(Param){}

User：登录用户名，就是客户端节点自身对象的名称

Pass：密码

Param：参数，由应用程序定义

发送应答参数：样例：(Param){}

Param：参数，由应用程序定义

接收应答参数：样例：(Param){}

Param：参数，由应用程序定义

#### PG_METH_PEER_AgentLogout {#pg-meth-peer-agentlogout}

ID：44

说明：代理节点注销登录。注销后，系统会自动删除代理节点对象。

交互方式：

方式4

发送请求参数：样例：(User){AgentUser1}

User：注销登录的节点名称

接收请求参数：样例：(User){AgentUser1}

User：注销登录的节点名称

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_AgentMessage {#pg-meth-peer-agentmessage}

ID：45

说明：给代理Peer节点发送一个消息。

交互方式：

方式4

发送请求参数：样例：(Peer){AgentUser1}(Data){123456abcdef}

Peer：对端的Peer节点名称

Data：消息的数据（字符串）

接收请求参数：样例：(Peer){AgentUser1}(Data){123456abcdef}

Peer：对端的Peer节点名称

Data：消息的数据（字符串）

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_ReloginReply {#pg-meth-peer-reloginreply}

ID：46

说明：本Peer节点自动重新登录服务器返回时，上报返回的登录结果信息。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：无此操作

接收请求参数：样例：(ErrCode){0}(Expire){30}(Type){0}(Sess){}(Param){}

ErrCode：错误码

Expire：登录老化时间（秒）

Type：用户的类型，缺省为0（将来使用）

Sess：登录会话信息，由应用程序定义

Param：参数，由应用程序定义

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_KickOut {#pg-meth-peer-kickout}

ID：47

说明：本Peer节点已经被服务器踢下线（原因是本Peer节点的节点名与其他节点的冲突了）。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：无此操作

接收请求参数：样例：(Param){0}

Param：保留，必须为0

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_AccessCtrl {#pg-meth-peer-accessctrl}

ID：48

说明：设置指定Peer节点对各个业务类的访问权限。

交互方式：

方式7

发送请求参数：样例：(Class){PG_CLASS_Video}(Ctrl){0}

Class：需要控制权限的业务类名称。

Ctrl：控制权限。0：禁止发送和接收，1：只允许发送，2：只允许接收，3：允许发送和接收。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_PEER_PushOption {#pg-meth-peer-pushoption}

ID：49

说明：下发配置选项给指定的Peer节点（只能在服务器节点上调用）。

交互方式：[方式9](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#10-9)

发送请求参数：样例：(Item){0}(Value){}

Item：选项ID，参考“[PG_METH_PEER_PushOption方法的选项](#6-pg-meth-peer-pushoption)”章节。

Value：选项的值

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

### 4) 扩展选项： {#4}

#### PG_OPTION_PEER_SocketMDU： {#pg-option-peer-socketmdu}

Item: 0

说明：给每个节点单独指定最大数据单元(Max Data Unit)。

格式：(Item){0}(Value){1024}

范围：本节点发送给所指定节点的数据在分片时单独使用所指定的最大数据单元。

#### PG_OPTION_PEER_SocketLAN {#pg-option-peer-socketlan}

Item: 1

说明：使能节点的局域网搜索功能，使其他节点能够搜索到本节点。

格式：“ (Item){1}(Value){ ” + omlEncode(“(Enable){0}(Peer){}(Label){}” + “}”。Enable：1使能，0禁止；Peer：指定搜索的节点名；Label：匹配标签。

范围：可在任何一个节点对象上操作，影响全局。

#### PG_OPTION_PEER_LoginTimeout {#pg-option-peer-logintimeout}

Item: 2

说明：设置登录的超时时间。

格式：(Item){2}(Value){10}，Value的单位为秒。

范围：可在任何一个节点对象上操作，影响全局。

#### PG_OPTION_PEER_CallTimeout {#pg-option-peer-calltimeout}

Item: 3

说明：设置Call请求的超时时间。

格式：(Item){3}(Value){10}，Value的单位为秒。

范围：可在任何一个节点对象上操作，影响全局。

#### PG_OPTION_PEER_SocketSelect {#pg-option-peer-socketselect}

Item: 4

说明：设置本节点与指定节点之间通信的方式。

格式：(Item){4}(Value){0}。Value为0：自动选择，Value为1：只用P2P穿透，Value为2：只用Relay转发。

范围：影响当前操作的节点对象。

#### PG_OPTION_PEER_RecvBacklogSize {#pg-option-peer-recvbacklogsize}

Item: 5

说明：设置接收backlog缓冲区的长度。

格式：(Item){5}(Value){0}。Value为0：默认长度（32），Value大于0：指定缓冲区长度。

范围：影响所有的节点对象。

#### PG_OPTION_PEER_SendBacklogSize {#pg-option-peer-sendbacklogsize}

Item: 6

说明：设置发送backlog缓冲区的长度。

格式：(Item){6}(Value){0}。Value为0：默认长度（32），Value大于0：指定缓冲区长度。

范围：影响所有的节点对象。

#### PG_OPTION_PEER_RelayList {#pg-option-peer-relaylist}

Item: 7

说明：设置“中继转发服务器列表”。

格式：“(Item){7}(Value){” + omlEncode(“(Relay0){(Type){0}(Load){0}(Addr){127.0.0.1:443}}”) + “}”

范围：本节点生效。

#### PG_OPTION_PEER_ForwardSpeed {#pg-option-peer-forwardspeed}

Item: 8

说明：设置“节点转发速率限制”。

格式：(Item){8}(Value){32768}。Value的值：0为禁止该节点转发，非0为允许转发的速率（单位为字节/秒）

范围：本节点生效。

#### PG_OPTION_PEER_ForwardGate {#pg-option-peer-forwardgate}

Item: 9

说明：设置“节点转发关闭门限”，如果该本节点自身使用的带宽超过该门限时，自动关闭节点转发，保留带宽给本节点自身使用。

格式：(Item){9}(Value){8192}，Value的值，关闭转发的门限速率（单位为字节/秒）

范围：本节点生效。

#### PG_OPTION_PEER_ForwardTryTime {#pg-option-peer-forwardtrytime}

Item: 10

说明：设置“节点转发连接尝试超时时间”。

格式：(Item){10}(Value){5}，Value的值为连接尝试超时时间（单位为秒）

范围：本节点生效。

#### PG_OPTION_PEER_ForwardUse {#pg-option-peer-forwarduse}

Item: 11

说明：设置“使用其他节点转发的标志”。

格式：(Item){11}(Value){0}，Value的值：0为不使用其他节点做转发，非0为使用其他节点做转发。

范围：本节点生效。

#### PG_OPTION_PEER_SocketInitWnd {#pg-option-peer-socketinitwnd}

Item: 12

说明：设置数据传输拥塞控制滑动窗口的初始大小。

格式：(Item){12}(Value){1}，Value的值：滑动窗口的初始大小（连续发送报文的个数），缺省为1。

范围：影响所有的节点对象。

#### PG_OPTION_PEER_SocketLoopSpeed {#pg-option-peer-socketloopspeed}

Item: 13

说明：设置服务器端接受客户端环回请求的速度。

格式：(Item){13}(Value){64}，Value的值：每秒接受环回请求的次数，缺省为64次/秒。

范围：影响所有的节点对象。

### 5) P2P连接通道类型： {#5-p2p}

#### PG_SKT_THROUGH_Unknown {#pg-skt-through-unknown}

值：0

说明：未知（类型没有检测出来）

#### PG_SKT_THROUGH_IPV4_Pub {#pg-skt-through-ipv4-pub}

值：4

说明：公网IP地址

#### PG_SKT_THROUGH_IPV4_NATConeFull {#pg-skt-through-ipv4-natconefull}

值：5

说明：完全锥型NAT

#### PG_SKT_THROUGH_IPV4_NATConeHost {#pg-skt-through-ipv4-natconehost}

值：6

说明：主机限制锥型NAT

#### PG_SKT_THROUGH_IPV4_NATConePort {#pg-skt-through-ipv4-natconeport}

值：7

说明：端口限制锥型NAT

#### PG_SKT_THROUGH_IPV4_NATSymmet {#pg-skt-through-ipv4-natsymmet}

值：8

说明：对称型NAT

#### PG_SKT_THROUGH_IPV4_Private {#pg-skt-through-ipv4-private}

值：12

说明：私网直连

#### PG_SKT_THROUGH_IPV4_NATLoop {#pg-skt-through-ipv4-natloop}

值：13

说明：NAT环回（Local NAT）

#### PG_SKT_THROUGH_IPV4_TunnelTCP {#pg-skt-through-ipv4-tunneltcp}

值：16

说明：TCP转发

#### PG_SKT_THROUGH_IPV4_TunnelHTTP {#pg-skt-through-ipv4-tunnelhttp}

值：17

说明：HTTP转发

#### PG_SKT_THROUGH_IPV4_PeerForward {#pg-skt-through-ipv4-peerforward}

值：24

说明：借助第三方节点转发

#### PG_SKT_THROUGH_IPV6_Pub {#pg-skt-through-ipv6-pub}

值：32

说明：IPV6公网IP地址

#### PG_SKT_THROUGH_IPV6_TunnelTCP {#pg-skt-through-ipv6-tunneltcp}

值：40

说明：TCP V6转发

#### PG_SKT_THROUGH_IPV6_TunnelHTTP {#pg-skt-through-ipv6-tunnelhttp}

值：41

说明：HTTP V6转发

#### PG_SKT_THROUGH_Offline {#pg-skt-through-offline}

值：65535

说明：对端节点不在线

### 6) PG_METH_PEER_PushOption方法的选项： {#6-pg-meth-peer-pushoption}

#### PG_PEER_PUSH_OPTION_RelayList {#pg-peer-push-option-relaylist}

Item: 0

说明：下发“中继转发服务器列表”给客户端节点。

格式：“(Item){0}(Value){” + omlEncode(“(Relay0){(Type){0}(Load){0}(Addr){127.0.0.1:443}}”) + “}”

范围：所操作的客户端节点生效。

#### PG_PEER_PUSH_OPTION_ForwardSpeed {#pg-peer-push-option-forwardspeed}

Item: 1

说明：下发“节点转发速率限制”给客户端节点。

格式：(Item){1}(Value){32768}。Value的值：0为禁止该节点转发，非0为允许转发的速率（单位为字节/秒）

范围：所操作的客户端节点生效。

#### PG_PEER_PUSH_OPTION_ForwardGate {#pg-peer-push-option-forwardgate}

Item: 2

说明：下发“节点转发关闭门限”给客户端节点，如果该客户端节点自身使用的带宽超过该门限时，自动关闭节点转发，保留带宽给节点自身使用。

格式：(Item){2}(Value){8192}，Value的值，关闭转发的门限速率（单位为字节/秒）

范围：所操作的客户端节点生效。

#### PG_PEER_PUSH_OPTION_ForwardTryTime {#pg-peer-push-option-forwardtrytime}

Item: 3

说明：下发“节点转发连接尝试超时时间”给客户端节点。

格式：(Item){3}(Value){5}，Value的值为连接尝试超时时间（单位为秒）

范围：所操作的客户端节点生效。

#### PG_PEER_PUSH_OPTION_ForwardUse {#pg-peer-push-option-forwarduse}

Item: 4

说明：下发“使用其他节点转发的标志”给客户端节点。

格式：(Item){4}(Value){0}，Value的值：0为不使用其他节点做转发，非0为使用其他节点做转发。

范围：所操作的客户端节点生效。