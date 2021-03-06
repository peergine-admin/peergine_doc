## 2\. Peergine的功能特性 {#2-peergine}

### 1) 全新的网络编程模式 {#1}

以面向对象的方法，把复杂的多点对等通信交互过程封装成通信对象，提供简单、直观的编程接口。即便是对网络通信知识缺乏了解的编程人员，也能够构建出功能强大的对等通信应用。参考“

基于对象的多点通信会话

”章节。

### 2) 强大的对等通信功能 {#2}

以通信对象类的形式实现各种对等通信功能，目前支持的通信对象类为：

节点类：提供对象的两点通信范围控制。节点的登录/注销，两个节点之间的远程过程调用，两个节点之间的消息传输，数据签名的生成和校验。参考“[使用节点类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\2_pgclasspeer_7c7b3a.md)”章节。

通信组类：提供对象的多点通信范围控制。支持手动控制组成员、自动控制组成员和主(Master)成员控制功能。参考“[使用通信组类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\3_pgclassgroup_7c7b3a.md)”章节

消息传输类：多个节点之间单向传输消息。参考“[使用消息传输类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\4_pgclassdata7c7b3a.md)”章节。

文件传输类：两个节点之间的文件传输。支持PUT和GET传输方式，文件的断点续传。参考“[使用文件传输类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\5_pgclassfile_7c7b3a.md)”章节

音频传输类：实时捕捉和传输音频。支持两点对话模式和多点会议模式。支持会议发言控制，实时音量变化显示，音频录制。参考“[使用音频传输类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\6_pgclassaudio_7c7b3a.md)”章节

视频传输类：实时捕捉和传输视频。支持本地预览模式、两点对话模式和多点会议模式。支持会议模式中视频的加入/离开，视频显示窗口的调整和转移，抓拍视频照片，视频录制。参考“[使用视频传输类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\7_pgclassvideo_7c7b3a.md)”章节。

白板共享类：多个节点共享白板，可设置绘制每种图形的参数，可设置绘制每种图形时的鼠标光标，保存白板内容到图片文件，从图片文件装入内容到白板。参考“[使用白板共享类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\8_pgclassboard_7c7b3a.md)”章节。

文件分块共享类：类似BitTorrent和eMule，多个节点以分块的方式对等传输文件。顺序传输模式，分散传输模式，可设置文件传输的数据块大小，实时将获取到的文件数据转发到本地HTTP服务器上以便使用播放器或浏览器来播放文件。参考“[使用文件分块共享类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\9_pgclassshare_7c7b3a.md)”章节。

数据表传输类：多个节点之间用访问数据库的方式传输数据。支持文件传输模式，每个文件对应到数据表的一条记录进行传输，实现文件的批量同步。参考“[使用数据表传输类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\10_pgclasstable_7c7b3a.md)”章节。

媒体流直播类：多个节点之间对等直播媒体流。支持实时捕捉音频流、实时捕捉视频流和AVI文件播放的方式提供媒体源。支持媒体源的快速切换，丢帧重传，自动选择网络状况好的节点进行中继转发。支持媒体流录制。参考“[使用媒体流直播类](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\11_pgclasslive_7c7b3a.md)”章节。

### 3) 自适应的网络互通机制 {#3}

以IPV4和IPV6的UDP协议为基础进行网络通信。对于UDP协议通信受限的节点，通过承载在TCP之上的隧道连接到中继服务器，然后转换成UDP协议通信。支持TCP、HTTP和WebSocket三种协议的隧道，以适应多种通信环境。通过中继服务器还可以完成 IPV4和IPV6之间的转换。支持位于IPV4私网中的节点的NAT穿越，自动探测NAT会话的老化时间，以恰当的时间间隔刷新NAT会话，防止老化。各种协议之间的转换互通，由Socket适配层自动适应，对上层通信对象透明。参考“[配置和运行中继服务器](..\pgatxkong_jian_de_bian_cheng_can_kao_ff1a\README.md)”章节。

一个通信节点只占用一个UDP端口，并此端口上实现出多点通信机制，因此占用防火强或NAT的会话资源少。

支持HTTP代理方式通信，在代理后面的主机也能连接到Peergine网络。

实现QOS机制，每个节点都有4个优先级队列，分别对消息/信令、音频、视频和文件4种流量进行优先级调度，保证高优先级流量的服务质量。

支持对通信数据进行加密，加密的密钥自动协商生成，无需配置。

### 4) 控件提供丰富的辅助功能 {#4}

Peergine在封装成控件时，又增加实现了辅助功能，包括常用的文件操作、文件缓冲区操作、本地Cookie存储、本地HTTP服务器、AVI文件播放等。这些辅助功能通过命令执行函数utilCmd()来调用。请参考“[控件的命令列表](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\11_pgclasslive_7c7b3a.md#5)”章节。

### 5) 多种OS平台和软件形态 {#5-os}

Peergine封装成了ActiveX控件、NPAPI插件、JNI插件和静态库等接口形式，支持Windows、Linux、Android、IOS和MacOSX操作系统。可用C/C++、JavaScript、Java和Object-C编程语言构建各种设备端、客户端、浏览器端和服务器端的应用。

各种OS平台和软件形态的支持情况及路标如下表：

| 软件形态\OS | Windows | Linux | Android | Mac OS X | iOS |
| --- | --- | --- | --- | --- | --- |
| ActiveX控件 | √ | -- | -- | -- | -- |
| NPAPI插件 | √ | √ | -- | -- | -- |
| Java (JNI)插件 | √ | √ | √ | -- | -- |
| 静态库 | √ | √ | √ | √ | √ |