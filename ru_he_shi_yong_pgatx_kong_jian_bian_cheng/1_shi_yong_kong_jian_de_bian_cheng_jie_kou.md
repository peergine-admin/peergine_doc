## 1\. 使用控件的编程接口 {#1}

### 1) 初始化控件 {#1-0}

有两种方式创建pgATX控件的实例：HTML的&lt;object&gt;标签和JavaScript的ActiveXObject()函数。

控件运行在浏览器中时，建议用HTML的&lt;object&gt;标签创建，这种方式不仅可以使用控件的所有功能，还可以使用控件的窗口来显示视频和白板。代码示例(HTML)：

&lt;object id=&quot;pgAtx&quot; classid=&quot;clsid:FFC9369F-A8D9-4598-8E22-ED07C7628BFC&quot; width=&quot;320&quot; height=&quot;240&quot;&gt;&lt;/object&gt;

控件运行在Windows Script Host中时，使用JavaScript的ActiveXObject()函数创建，代码示例(JavaScript)：

var pgAtx = new ActiveXObject(&quot;pgATX.pgATXCtrl&quot;);

创建控件实例后，通过给控件的配置属性变量赋值进行配置，然后调用Start()函数启动控件的节点功能。代码示例(JavaScript)：

pgAtx.Control = &quot;Type=1&quot;;

pgAtx.Node = &quot;Type=0&quot;;

pgAtx.Class = &quot;PG_CLASS_Data:8;PG_CLASS_File:64;PG_CLASS_Audio:8;PG_CLASS_Video:8&quot;;

pgAtx.Local = &quot;Addr=0:0:0:127.0.0.1:0:0&quot;;

pgAtx.Server = &quot;Name=PGServer;Addr=0:0:0:127.0.0.1:1112:0&quot;;

pgAtx.Relay = &quot;(Relay0){(Type){1}(Load){0}(Addr){FE800000:0:01B05996:42CFB70D:7777:0}}&quot;;

pgAtx.OnExtRequest = pgOnExtRequest;

pgAtx.OnReply = pgOnReply;

if (!pgAtx.Start(0)) {

alert(&quot;Initialize failed&quot;);

}

请参考“[控件的属性配置项](#1)”章节。

### 2) 使用通信对象 {#2}

初始化控件实例之后，就可以使用[控件的节点功能函数](#2)。

用ObjectAdd()函数创建通信对象，用ObjectDelete()删除通信对象。用ObjectSetGroup()函数设置或修改通信对象的关联通信组。虽然在ObjectAdd()函数中已经指定了通信对象的关联通信组，但可以使用此函数进行修改。如果指定的通信组参数为空，则取消与通信组关联。

通信对象在创建之后或用ObjectSetGroup()修改关联通信组之后会自动与通信范围内的其他节点上的同名通信对象进行同步。但由于网络不稳定或者通信对象创建的先后顺序等因素，会导致同步失败。这时可以使用ObjectSync()函数主动触发通信对象进行同步。

通信对象同步以后，就可以调用通信对象的方法。需要ObjectRequest()、ObjectExtReply()、OnExtRequest()和OnReply()这4 个函数配合才可以完成一次方法的调用。其中OnExtRequest()和OnReply()是回调函数，需要在控件初始化时注册，请参考“[控件的属性配置项](#1)”章节。首先请求端节点的应用程序调用控件的ObjectRequest()函数发起请求，控件通过网络交互发送请求数据到接收端节点，接收端节点的控件回调OnExtRequest()函数上报请求给应用程序。应用程序处理完请求后调用控件的ObjectExtReply()函数发送应答，控件通过网络交互发送应答数据给请求端节点，请求端节点的控件回调OnReply()函数上报应答给应用程序。这样就完成了一次方法的调用。参考“[pgATX控件与应用程序的交互方式](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\11_pgclasslive_7c7b3a.md#4)”章节和“[简单聊天室例子](#1)”章节。

### 3) 处理消息循环 {#3}

控件与应用程序的交互过程需要通过系统的消息队列投递消息。当控件运行在界面线程中 (例如运行在浏览器中)时，界面线程能够处理消息循环。但运行在Windows Script Host中时，线程没有消息循环，无法完成交互消息的投递。这时就需要应用程序调用控件的PumpMessage()函数主动处理消息队列。代码示例(JavaScript)：

while (pgAtx.PumpMessage(0)) {

// DO TO

}

### 4) 使用OML解析器 {#4-oml}

调用控件的通信对象的方法时，输入、输出的参数都是OML格式。控件提供了一组OML解析器函数来辅助构造和解析OML字符串。请参考“[控件的OML解析器函数](..\pgatxkong_jian_de_bian_cheng_can_kao_ff1a\3_kong_jian_de_oml_jie_xi_qi_han_65703a.md)”和“[对象标记语言(OML)](..\dui_xiang_biao_ji_yu_8a0028_oml\README.md)”章节。OML解析器的每个函数都是无状态的，函数之间也没有关联。函数的每一次调用都是独立的，调用完成后通过返回值输出处理后的OML字符串。

### 5) 获取控件的窗口参数 {#5}

控件运行在浏览器中时，一个重要用途是做为视频显示和白板共享的窗口。控件提供了辅助函数utilGetWndRect()来获取控件窗口的尺寸和句柄，以便用来初始化视频或白板窗口。

### 6) 使用控件的辅助命令 {#6}

在构建应用程序的过程中，除了网络通信外，还需要调用操作系统的某些资源或功能才能构成完整的应用程序。控件提供了一些常用的辅助功能，例如，常用文件操作、文件缓冲区操作、本地HTTP服务器控制和AVI文件播放等。通过辅助函数utilCmd()来调用这些辅助功能。请参考“[控件的命令列表](#5)”章节。

### 7) 使用安全沙盒目录 {#7}

Peergine是一个对等通信中间件，不可避免地要访问本地的文件系统。比如，发送接收文件、缓存文件等。为了防止某些恶意的应用程序使用Peergine进行偷窃用户数据、传输恶意代码等不良操作，Peergine通过使用沙盒目录来控制文件系统的访问范围。控制规则如下：

(1) 所有涉及到网络传输的文件访问都限制在沙盒目录内。

(2) 本地的文件操作，可以访问沙盒目录之外的文件。比如，拍摄照片保存到本地文件，装载本地图片到白板中。

在下文各个功能的编程参考章节中，涉及访问文件系统时，将会逐个说明是否受到沙盒目录限制。缺省情况下，沙盒目录是当前用户的“Documents”目录下的“Peergine”目录。可以通过控件的右键菜单或Setting()命令弹出设置对话框，让用户修改沙盒目录的父目录位置。

**注：沙盒目录必须具有：创建、删除、写、读等文件操作的权限，否则Peergine的某些功能将失效。**

沙盒目录中的文件的移入和移出通过[FileCopy()](..\pgatxkong_jian_de_bian_cheng_can_kao_ff1a\5_kong_jian_de_ming_ling_lie_88683a.md#3-filecopy)命令完成，FileCopy()的Src参数和Dst参数的使用规则如下：

(1) Src和Dst都指定了文件路径（非空），则Src和Dst指定的文件都必须在沙盒目录内，否则命令调用执行失败。

(2) Src指定了文件路径且Dst为空，则Src指定的文件必须在沙盒目录内。当命令执行时，Peergine弹出文件对话框，让用户选择Dst文件路径，进行文件移出操作。

(3) Src为空且Dst指定了文件路径，则Dst指定的文件必须在沙盒目录内。当命令执行时，Peergine弹出文件对话框，让用户选择Src文件路径，进行文件移入操作。

**注：如果使用Peergine之外的途径移入/移出文件，则 Peergine将无法保证其安全性。比如，使用控制台copy命令复制文件，在资源管理器里手工复制、粘贴文件，或者调用操作系统API复制文件等。**