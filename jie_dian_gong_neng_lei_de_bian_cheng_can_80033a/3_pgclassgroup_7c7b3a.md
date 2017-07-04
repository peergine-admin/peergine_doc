## 3\. PG_CLASS_Group类: {#3-pg-class-group}

### 1) 描述： {#1}

通信组类。通信组对象的成员就是节点对象的名称。

### 2) 选项： {#2}

#### PG_ADD_GROUP_Update {#pg-add-group-update}

掩码：0x1

说明：使能PG_METH_GROUP_Update方法，允许组成员更新时通过PG_METH_GROUP_Update方法上报给应用层。

#### PG_ADD_GROUP_Master {#pg-add-group-master}

掩码：0x2

说明：使能PG_METH_GROUP_Master方法，允许在组中指定Master成员。

#### PG_ADD_GROUP_Refered {#pg-add-group-refered}

掩码：0x4

说明：允许其他节点引用该组的成员，当该组成员更新时，自动同步到其成员节点。

#### PG_ADD_GROUP_NearPeer {#pg-add-group-nearpeer}

掩码：0x8

说明：使能邻近节点功能，此选项只能与PG_ADD_GROUP_Refered选项组合使用。当组内的成很多时，一个成员节点没有必要关心所有其他成员节点，它只要知道与它相邻近的节点就可以了。被引用的组对象启用此选项后，在同步成员列表时，它只把与该成员节点相邻近的其他成员发送给该成员节点。

#### PG_ADD_GROUP_Modify {#pg-add-group-modify}

掩码：0x10

说明：使能PG_METH_GROUP_Modify方法，允许调用该方法修改组的成员。

#### PG_ADD_GROUP_Index {#pg-add-group-index}

掩码：0x20

说明：使能用HASH表的机制索引组成员。

#### PG_ADD_GROUP_Offline {#pg-add-group-offline}

掩码：0x40

说明：组成员节点对象去同步时，自动离开组。

#### PG_ADD_GROUP_HearOnly {#pg-add-group-hearonly}

掩码：0x80

说明：只接收其他组成员的同步，不把本对象已经获取到的组成员信息发送给其他节点。

### 3) 方法： {#3}

#### PG_METH_GROUP_Modify {#pg-meth-group-modify}

ID：32

说明：修改该组的成员

交互方式：

方式7

发送请求参数：样例：(Action){0}(PeerList){(Peer1){}(Peer2){}}

Action：1为增加成员，0为删除成员。

PeerList：指定要修改的成员列表，成员名称位于OML元素的名称。成员名称就是节点对象的名称。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_GROUP_Update {#pg-meth-group-update}

ID：33

说明：该组的成员有更新时，上报给应用程序。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：无此操作

接收请求参数：样例：(Action){1}(PeerList){(Peer1){}(Peer2){}}

Action：1为增加成员，0为删除成员。

PeerList：指定要修改的成员列表，成员名称位于OML元素的名称。成员名称就是节点对象的名称。

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_GROUP_Master {#pg-meth-group-master}

ID：34

交互方式：[方式4](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#5-4)

说明：指定组里的Master成员。用OnExtRequest()函数的返回值确认是否接受Master请求，返回值等于0表示接受，返回值大于0表示拒绝及其原因。

发送请求参数：样例：(Peer){NodeA}

Peer：指定的Master成员名称。

接收请求参数：样例：(Peer){NodeA}

Peer：指定的Master成员名称。

发送应答参数：无此操作

接收应答参数：无此操作

### 4) 扩展选项 {#4}

#### PG_OPTION_GROUP_NearSize {#pg-option-group-nearsize}

Item：0

说明：设置邻近节点的范围。

格式：(Item){0}(Value){6}

范围：在需要调节邻近节点范围的“PG_CLASS_Group”类对象上操作，只影响该对象。