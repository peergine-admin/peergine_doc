## 3\. 使用通信组类(PG_CLASS_Group) {#3-pg-class-group}

### 1) 手动控制成员 {#1}

通过调用通信组类的PG_METH_GROUP_Modify方法来手动添加、删除通信组的成员，必须启用PG_ADD_GROUP_Modify选项后才允许调用该方法。通信组对象添加成员后，该通信组对象会与其成员所对应的节点上的同名通信组对象建立同步，其成员列表也会复制到与其成员所对应的节点上的同名通信组对象。

举例说明：有NodeA、NodeB和NodeC三个节点，它们都有通信组对象Group0，开始Group0的成员列表都是空的。在节点NodeA上给Group0添加成员“NodeA”、“NodeB”和“NodeC”，则节点NodeA上的Group0会与节点NodeB和NodeC上的Group0建立同步，同时节点NodeA上的Group0的成员列表也复制到节点NodeB和NodeC上的Group0，使节点NodeB和NodeC上的Group0都包含成员“NodeA”、“NodeB”和“NodeC”。当然节点NodeB和NodeC上的Group0都包含了对方节点作为成员后，它们之间也会建立同步。

**注：给通信组对象添加一个成员后，如果该成员名称所对应的节点对象还不存在，则系统会自动创建该节点对象。**

### 2) 自动控制成员 {#2}

Peergine还提供了一种自动控制通信组对象的成员的方法：

(1) 当一个通信组对象启用了PG_ADD_GROUP_Refered选项时，则允许其他同名通信组对象引用该通信组对象的成员，它的成员列表将自动复制到引用它的同名通信组对象。当它的成员发生变化时，会实时地通知给引用它的同名通信组对象。

(2) 一个通信组对象引用了另一个通信组对象的成员时，它自身的节点也同时加入了被引用的通信组对象的成员列表。当它取消了引用或被删除时，它自身的节点就离开了被引用的通信组对象的成员列表。

举例说明：有NodeA、NodeB和NodeC三个节点，它们都有通信组对象Group0，开始Group0的成员列表都是空的，其中节点NodeA启用了PG_ADD_GROUP_Refered选项。节点NodeB和NodeC上的Group0在创建时指定关联了节点NodeA，那么节点NodeB和NodeC就加入了节点NodeA上的Group0的成员列表，同时节点NodeA上的Group0的成员列表也复制到节点NodeB和NodeC上的Group0。如果节点NodeB上的Group0取消关联节点NodeA或被删除，则节点NodeB就离开了节点NodeA上的Group0的成员列表，同时节点NodeA上的Group0会通知节点NodeC上的Group0把节点NodeB从其成员列表中删除。

代码示例(JavaScript)：

// 在节点NodeA上创建Group0，选项为PG_ADD_GROUP_Refered=0x4

pgAtx.ObjectAdd(“Group0”, “PG_CLASS_Group”, “”, 0x04);

// 在节点NodeB和NodeC上创建Group0，关联节点NodeA。

pgAtx.ObjectAdd(“Group0”, “PG_CLASS_Group”, “NodeA”, 0);

### 3) 邻近成员控制 {#3}

在对等通信场景中，有时候一个通信组内的成员会很多，但一个节点只希望与离它最近的几个节点交互。Peergine针对这种情况提供了一种邻近节点控制的功能。一个通信组对象启用了PG_ADD_GROUP_Refered选项作为成员引用对象，如果同时启用了PG_ADD_GROUP_NearPeer选项，则它就使能了邻近节点控制功能。使能了邻近节点控制功能通信组对象只把在邻近范围内的成员复制到引用它的通信组对象。邻近范围的大小缺省为6，可以通过PG_METH_COMMON_SetOption方法的修改。

举例说明：节点NodeA上的Group0已经包含了很多成员，节点NodeB和NodeC是其中的两个成员。那么，节点NodeA上的Group0给节点NodeB上的Group0复制了离节点NodeB最近的6个成员。同样，节点NodeA上的Group0给节点NodeC上的Group0复制了离节点NodeC最近的6个成员。以此类推，每个成员节点上的Group0都复制到了离该节点最近的6个成员。

### 4) 主成员控制 {#4}

在某些应用场景中，一个通信组中需要有一个权限更高的成员来管理其他成员。Peergine针对这种情况提供了一种主成员控制功能。通信组对象启用了PG_ADD_GROUP_Master选项后才可以使用主成员控制功能。通过调用PG_METH_GROUP_Master方法向通信组内的成员公告主成员的名称，成员接收到公告后，通过返回应答的错误码确认是否接受该主成员公告。