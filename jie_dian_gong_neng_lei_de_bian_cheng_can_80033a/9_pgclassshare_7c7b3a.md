## 9\. PG_CLASS_Share类: {#9-pg-class-share}

### 1) 描述： {#1}

文件分块共享类。

### 2) 选项： {#2}

#### PG_ADD_SHARE_Distribute {#pg-add-share-distribute}

掩码：0x1

说明：使能分散传输模式。此选项没有使能时，控件缺省以从前到后的顺序获取文件的数据块。但此选项使能后，控件尽力避免按照从前到后的顺序来获取文件的数据块。

### 3) 方法： {#3}

#### PG_METH_SHARE_Open {#pg-meth-share-open}

ID：32

说明：打开文件分块共享对象。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(Path){c:\temp\xxxxx.avi}(HttpURL){}(Hash){}(FileSize){}(BlockSize){0} (TimerVal){3}

Path：共享文件的存储路径（受沙盒控制）。

HttpURL：共享文件数据实时转发到本地HTTP服务器时的URI。如果不需要转发到本地HTTP服务器，则此参数为空。

Hash：共享文件的摘要，SHA256算法生成，Base64格式。如果本节点已经获取到完整的文件，则作为共享的种子，这时不需要指定文件的摘要，此参数为空。

FileSize：共享文件的长度（字节）。如果本节点已经获取到完整的文件，则作为共享的种子，这时不需要指定文件的长度，此参数为空。

BlockSize：文件分块传输的块大小（字节）。如果此参数为0，则块的大小为缺省的1M字节。

TimerVal：周期自动上报文件传输状态的时间间隔（秒）。如果不需要自动上报文件传输状态，则此参数为0。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_SHARE_Close {#pg-meth-share-close}

ID：33

说明：关闭文件分块共享对象。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：空

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_SHARE_FileInfo {#pg-meth-share-fileinfo}

ID：34

说明：获取共享文件的信息。

交互方式：[方式6](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#7-6)或[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：空

接收请求参数：样例：(Name){xxxx.avi}(Hash){}(FileSize){564564}(CurSize){89879}(IsSeed){1}

Name：共享文件名。

Hash：共享文件的摘要，SHA256算法生成，Base64格式。

FileSize：共享文件的长度（字节）。

CurSize：当前已经传输的长度（字节）

IsSeed：本节点是否为共享种子。当本节点获取到完整的文件时，就成为共享种子。0为不是种子，1为是种子。

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_SHARE_FileStatus {#pg-meth-share-filestatus}

ID：35

说明：获取共享文件的传输状态。

交互方式：[方式6](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#7-6)或[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：空

接收请求参数：样例：(Path){}(Hash){}(FileSize){564564}(CurSize){3378}(Speed){3433}(BlockNum) {27}(BlockSta)(0-2){1}(3-26){0}}

Path：文件的路径

Hash：文件的摘要

FileSize：共享文件的总长度（字节）

CurSize：当前已经传输的长度（字节）

Speed：当前传输的速度（字节/秒）

BlockNum：共享文件的总的块数目

BlockSta：数据块的状态。通过一个OML列表来表示数据块的状态，OML元素的名称是数据块的序号，OML元素的内容是数据块的状态。如果多个连续的数据块的状态相同，合并到一个OML元素中，元素名由这些连续数据块的起始块号和终止块号组成，中间用‘-’号连接。例如：(0-2){1}。状态值参考“[常量：数据块的状态](#4)”章节。

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_SHARE_PeerStatus {#pg-meth-share-peerstatus}

ID：36

说明：获取共享文件的源节点的数据块传输状态。

交互方式：[方式6](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#7-6)

发送请求参数：样例：(Peer){NodeA}(Index){0}

Peer：指定获取数据块状态的源节点名称。如果此参数不为空，则忽略下文的Index参数。

Index：指定获取数据块状态的源节点序号。上文的Peer参数为空时，使用此参数。通过依次递增序号，可以遍历所有源节点的数据块状态。

接收请求参数：样例：(Peer){NodeA}(SendSpeed){8983}(RecvSpeed){2325}(SendBytes){565009} (RecvBytes){1767}(BlockNum){27}(BlockSta){(0-2){1}(3-26){0}}

Peer：原节点的名称

SendSpeed：发送速率（字节/秒）

RecvSpeed：接收速率（字节/秒）

SendBytes：已发送的字节

RecvBytes：已接收的字节

BlockNum：总的数据块数目

BlockSta：数据块的状态。

发送应答参数：无此操作

接收应答参数：无此操作

### 4) 常量：数据块的状态 {#4}

#### PG_SHARE_BLOCK_ST_Empty {#pg-share-block-st-empty}

ID：0

说明：该数据块还没有源。

#### PG_SHARE_BLOCK_ST_Source {#pg-share-block-st-source}

ID：1

说明：该数据块已经找到源，但还没有开始传输。

#### PG_SHARE_BLOCK_ST_Getting {#pg-share-block-st-getting}

ID：2

说明：该数据块正在传输。

#### PG_SHARE_BLOCK_ST_Stored {#pg-share-block-st-stored}

ID：3

说明：该数据块已经获取完成并存储到本地的文件中。