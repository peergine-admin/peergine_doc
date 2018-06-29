## 10\. PG_CLASS_Table类: {#10-pg-class-table}

### 1) 描述： {#1}

数据表传输类

### 2) 选项： {#2}

#### PG_ADD_TABLE_Master {#pg-add-table-master}

掩码：0x1

说明：使能能主节点模式，只有主节点可以插入或修改，其他节点只能查询。（此功能未实现）

#### PG_ADD_TABLE_File {#pg-add-table-file}

掩码：0x2

说明：使能文件传输模式，数据表的每条记录用来同步一个文件。参考“[说明：文件传输模式](#6)”章节。

### 3) 方法： {#3}

#### PG_METH_TABLE_Init {#pg-meth-table-init}

ID：32

说明：初始化数据表。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(MaxRec){256}(FldSize){6}(Param){}

MaxRec：数据表的最大记录数，范围：1 ~ 65534。

FldSize：数据表的字段数，范围1 ~ 32。

Param：参数，不能包含OML标记字符，请用omlEncode()进行编码。使能文件传输模式时，通过此参数传递文件缓冲的目录路径。参考“[说明：文件传输模式](#6)”章节。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_TABLE_Sync {#pg-meth-table-sync}

ID：33

说明：强制同步数据表。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(Action){1}(Param){}

Action：同步的动作，参考“[常量：强制同步动作](#4)”

Param：同步的参数。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_TABLE_Index {#pg-meth-table-index}

ID：34

说明：在指定的字段上建立数据表的索引。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(SortMode){1}(FieldID){0}

SortMode：排序方式。0为降序，1为升序

FieldID：建立索引的字段ID

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_TABLE_Insert {#pg-meth-table-insert}

ID：35

说明：在数据表中插入一条记录

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(ValList){(0){aaaa}(1){bbb}(2){ccccccc}}

ValList：记录的各字段的值列表。格式为：(字段ID){字段的值}

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_TABLE_Delete {#pg-meth-table-delete}

ID：36

说明：从数据表中删除一条或多条记录。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(RecID){0}(RecSize){1}(Cond){(Operator){0}(FieldID){0}(Value){aaaa}}&quot;

RecID：匹配记录的起始记录ID

RecSize：指定删除记录的条数

Cond：匹配记录的条件。Operator为比较操作符，FieldID为比较的字段ID，Value为比较的值。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_TABLE_Update {#pg-meth-table-update}

ID：37

说明：修改一条记录的字段值。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(RecID){0}(Cond){(Operator){0}(FieldID){0}(Value){aaaa}}(ValList){(0){xxx}}

RecID：匹配记录的起始记录ID

Cond：匹配记录的条件。Operator为比较操作符，FieldID为比较的字段ID，Value为比较的值。

ValList：记录的各字段的值列表

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_TABLE_Query {#pg-meth-table-query}

ID：38

说明：查询数据表。查询之后通过PG_METH_TABLE_Report方法上报查询结果。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(RecID){0}(RecSize){3}(Cond){(Operator){0}(FieldID){0}(Value){aaabbb}} (FldIDList){(0)(1)(2)}&quot;

RecID：匹配记录的起始记录ID

RecSize：指定查询记录的条数

Cond：匹配记录的条件。Operator为比较操作符，FieldID为比较的字段ID，Value为比较的值。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_TABLE_Report {#pg-meth-table-report}

ID：39

说明：上报记录数据变化或查询结果给应用层。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：无此操作

接收请求参数：样例：(RecID){1}(TopID){10}(NextID){1}(Action){1}(ValSize){2}(ValList){(0){xxx} (1){aaaa}}

RecID：当前记录的ID

TopID：最大的记录ID

NextID：下一个记录的ID

Action：对记录的操作。1为记录被添加或修改，0为记录被删除。

ValSize：上报的字段数目

ValList：上报的字段值列表

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_TABLE_Import {#pg-meth-table-import}

ID：40

说明：从指定的数据源导入数据倒数据表（未实现）。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：样例：(Type){0}(Path){c:\peergine\tab1.pgtab}

Type：数据源的类型。0为*.pgtab文件。

Path：数据源的路径（受沙盒控制）。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_TABLE_Export {#pg-meth-table-export}

ID：41

说明：把数据表的内容导出或保存到数据源中（未实现）。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：样例：(Type){0}(Path){c:\peergine\tab1.pgtab}

Type：数据源的类型。0为*.pgtab文件。

Path：数据源的路径（受沙盒控制）。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

### 4) 常量：强制同步的动作 {#4}

#### PG_TABLE_SYNC_ACT_Request {#pg-table-sync-act-request}

ID：0

说明：立即执行一个同步请求操作。

#### PG_TABLE_SYNC_ACT_Hole {#pg-table-sync-act-hole}

ID：1

说明：强制跳过同步的记录空洞。如果数据表中某些记录已经没有源（添加这些记录的节点已经不在通信组里了），则数据表的同步操作就会停止在这些记录上，不能再继续传输数据，这种情况称为记录空洞(Hole)。执行此动作可以跳过这些没有源的记录继续同步后面有源的记录。

### 5) 常量：比较操作符 {#5}

#### PG_TABLE_OPTR_Equal {#pg-table-optr-equal}

ID：0

说明：相等

#### PG_TABLE_OPTR_Less {#pg-table-optr-less}

ID：1

说明：小于

#### PG_TABLE_OPTR_More {#pg-table-optr-more}

ID：2

说明：大于

#### PG_TABLE_OPTR_UnEqual {#pg-table-optr-unequal}

ID：3

说明：不相等

#### PG_TABLE_OPTR_LessEqual {#pg-table-optr-lessequal}

ID：4

说明：小于等于

#### PG_TABLE_OPTR_MoreEqual {#pg-table-optr-moreequal}

ID：5

说明：大于等于

#### PG_TABLE_OPTR_Prefix {#pg-table-optr-prefix}

ID：6

说明：匹配前缀

#### PG_TABLE_OPTR_Suffix {#pg-table-optr-suffix}

ID：7

说明：匹配后缀

#### PG_TABLE_OPTR_Include {#pg-table-optr-include}

ID：8

说明：包含子串

### 6) 说明：文件传输模式 {#6}

对等数据表支持传输文件功能，在创建数据表对象时通过PG_ADD_TABLE_File选项来使能。使能文件传输模式后，PG_METH_TABLE_Init方法的Param参数用来传递文件缓冲区的名称，该参数为OML格式，样例为：(Cache){MyFileCache}。文件缓冲区用[CacheSetDir](..\pgatxkong_jian_de_bian_cheng_can_kao_ff1a\5_kong_jian_de_ming_ling_lie_88683a.md#11-cachesetdir)命令来开启。由于该参数为OML格式，包含OML标记字符，所以要用omlEncode()函数来编码。代码示例(JavaScript)如下：

pgAtx.utilCmd(“CacheSetDir”, “(Name){MyFileCache}(Dir){c:\\Peergine\\FileCache}”);

var sParam = &quot;(Cache){MyFileCache}&quot;;

var sInEle = “(MaxRec){1024}(FldSize){8}(Param){“ + pgAtx.omlEncode(sParam) + “}”;

pgAtx.ObjectRequest(&quot;Table1&quot;, 32, sInEle, “TableInit”);

在文件传输模式时，数据表的每一条记录存储一个文件的属性，文件的属性存储在前6个字段里。文件属性与字段ID的对应分别为：

0：URL，文件在缓冲区中的唯一标识。

1：Path，文件在缓冲区中的存储路径。

2：Size，文件的长度（字节）。

3：Time，文件的修改时间。格式：YYYY-MM-DD,HH:MM:SS

4：Hash，文件的摘要。SHA256算法生成，Base64格式。

5：Status，文件的传输状态。参考“[常量：文件传输的状态](#4)”章节。

这些文件属性发生变化时，会通过PG_METH_TABLE_Report方法上报给应用层。

在文件传输模式初始化数据表时，如果指定的FldSize小于6，则控件会强制使FldSize等于6。如果FldSize大于6，则ID大于等于6的字段的用法由应用层定义。