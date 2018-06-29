## 1\. 类的通用选项和方法 {#1}

### 1) 描述： {#1-0}

本章节列出各种通信对象类都共用的选项和方法。

### 2) 选项： {#2}

#### PG_ADD_COMMON_Sync {#pg-add-common-sync}

掩码：0x10000

说明：使能该通信对象的PG_METH_COMMON_Sync方法

#### PG_ADD_COMMON_Error {#pg-add-common-error}

掩码：0x20000

说明：使能该通信对象的PG_METH_COMMON_Error方法

#### PG_ADD_COMMON_Encrypt {#pg-add-common-encrypt}

掩码：0x40000

说明：对该通信对象的通信数据进行加密传输。

#### PG_ADD_COMMON_Compress {#pg-add-common-compress}

掩码：0x80000

说明：对该通信对象的通信数据进行压缩传输。

### 3) 方法： {#3}

#### PG_METH_COMMON_Sync {#pg-meth-common-sync}

ID：0

说明：上报通信对象的同步状态。当通信对象同步或去同步时，系统会调用此方法。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：无此操作

接收请求参数：样例：(Action){1}

Action：同步的动作。0为去同步，1为已同步。

发送应答参数：无此操作

接收请求参数：无此操作

#### PG_METH_COMMON_Error {#pg-meth-common-error}

ID：1

说明：上报错误信息

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：无此操作

接收请求参数：样例：(Meth){32}(Error){1}

Meth：产生错误的方法

Error：错误码

发送应答参数：无此操作

接收请求参数：无此操作

#### PG_METH_COMMON_SetOption {#pg-meth-common-setoption}

ID：2

说明：设置通信对象的扩展选项参数。各个通信对象类根据实际需要实现此方法。。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(Item){1}(Value){}

Item：配置参数ID，具体值由各个通信对象类定义。

Value：配置参数的值

接收请求参数：无此操作

发送应答参数：无此操作

接收请求参数：无此操作

#### PG_METH_COMMON_GetOption {#pg-meth-common-getoption}

ID：3

说明：获取通信对象的扩展选项参数。各个通信对象类根据实际需要实现此方法。

交互方式：[方式5](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：样例：(Item){1}

Item：配置参数ID，具体值由各个通信对象类定义。

接收请求参数：无此操作

发送应答参数：无此操作

接收请求参数：样例：(Item){1}(Value){}

Item：配置参数ID，具体值由各个通信对象类定义。

Value：配置参数的值