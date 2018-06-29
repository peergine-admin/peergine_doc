## 11\. PG_CLASS_Live类: {#11-pg-class-live}

### 1) 描述： {#1}

媒体流直播类。

### 2) 选项： {#2}

#### PG_ADD_LIVE_NoOutput {#pg-add-live-nooutput}

掩码：0x1

说明：收到媒体流后只进行转发，不进行输出、播放。

#### PG_ADD_LIVE_LoadFirst {#pg-add-live-loadfirst}

掩码：0x2

说明：优先从剩余转发负荷最大的节点获取媒体流。

#### PG_ADD_LIVE_DrawThread {#pg-add-live-drawthread}

掩码：0x4

说明：创建一个单独的线程来显示视频帧到视频窗口（不在UI线程里显示视频，Windows、android系统有效）。

#### PG_ADD_LIVE_FrameStat {#pg-add-live-framestat}

掩码：0x8

说明：启用视频帧统计信息的上报，参考“PG_METH_LIVE_FrameStat”。

#### PG_ADD_LIVE_FilterDecode {#pg-add-live-filterdecode}

掩码：0x10

说明：启动视频解压之后加上模糊滤镜效果。

### 3) 方法： {#3}

#### PG_METH_LIVE_Open {#pg-meth-live-open}

ID：32

说明：打开一个媒体流直播对象。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(Source){1}(Media){1}(Delay){3000}(CacheSize){256}(MaxPart){1} (TimerVal){3}(Param){}

Source：指定本节点是否为源节点。1为源(播放)节点，0为收看节点。

Media：指定媒体流的类型。参考“[常量：媒体流的类型](#4)”章节

Delay：接收媒体流的缓冲延时时间（毫秒）。只有作为源节点时，才需要指定此参数。

CacheSize：缓冲区的长度（帧数）。只有作为源节点时，才需要指定此参数。

MaxPart：最大的子流数目。控件支持获取媒体流时，分裂成多个子流分别从不同的源节点获取。此参数指定最大的子流数目。此参数的值必须为以2为底数、正整数为指数的幂，例如：1、2、4、8等。

TimerVal：周期自动上报传输状态的时间间隔。如果此参数为0，则不自动上报状态。

Param：初始化媒体流的参数。此参数中不能包含OML的标记字符，请用omlEncode()进行编码。参考“[说明：媒体流的初始化](#6)”章节。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_LIVE_Close {#pg-meth-live-close}

ID：33

说明：关闭一个媒体流直播对象

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：空

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_LIVE_Ctrl {#pg-meth-live-ctrl}

ID：34

说明：控制媒体流的播放和收看。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(Action){1}(Param){0}

Action：控制动作。参考“[常量：媒体流的控制动作](#5)”章节

Param：控制参数（未使用）。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_LIVE_Status {#pg-meth-live-status}

ID：35

说明：获取或上报媒体流传输的状态。

交互方式：[方式6](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#7-6)或[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：空

接收请求参数：样例：(BitRate){84950}(FrmRate){9}(FrmPlay){456}(FrmCache){568}(FrmTotal){0}

BitRate：媒体流的比特率（bits/秒）

FrmRate：媒体流的帧率（帧/秒）

FrmPlay：已经播放的帧号

FrmCache：已经缓冲的帧号

FrmTotal：总的帧数

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_LIVE_Record {#pg-meth-live-record}

ID：36

说明：录制媒体流到avi、mov或mp4文件中。只有作为收看节点时，才能录制。

交互方式：[方式5](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：样例：(Path){c:\temp\xxxx.avi}(HasVideo){0}(HasAudio){0}

Path：avi、mov或mp4文件的路径（受沙盒控制），文件名后缀可以为“avi”、“mov”或“mp4”。

HasVideo：需要录制视频。0为不需要录制视频，1为需要录制视频。

HasAudio：需要录制音频。0为不需要录制音频，1为需要录制音频。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Path){c:\temp\xxxx.avi}

Path：avi、mov或mp4文件的路径。

#### PG_METH_LIVE_Camera {#pg-meth-live-camera}

ID：37

说明：拍摄视频快照。

交互方式：[方式5](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：样例：(Path){c:\temp\xxxx.jpg}

Path：jpg文件的路径（受沙盒控制），文件名后缀必须为“jpg”(大小写不敏感)。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Path){c:\temp\xxxx.jpg}

Path：jpg文件的路径。

#### PG_METH_LIVE_RelayPeer {#pg-meth-live-relaypeer}

ID：38

说明：强制从指定的节点获取媒体流。

交互方式：[方式5](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：样例：(Flag){0}(Action){1}(Peer){abc}

Flag：标志。1为返回当前的节点列表，0为不返回节点列表。

Action：操作。1为增加，0为删除。

Peer：指定获取媒体流的节点名称

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(PeerSize){2}(PeerList){(abc){}(xyx){}}

PeerSize：节点个数。

PeerList：节点列表。

#### PG_METH_LIVE_FrameStat {#pg-meth-live-framestat}

ID：39

说明：上报视频发送状态的统计信息。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：无此操作

接收请求参数：样例：(Peer){NodeA}(Total){2365}(Drop){0}

Peer：指定上报视频统计的节点。

Total：总发送的视频帧数

Drop：丢弃的视频帧数

发送应答参数：无此操作

接收应答参数：无此操作。

### 4) 常量：媒体流的类型 {#4}

#### PG_LIVE_MEDIA_Audio {#pg-live-media-audio}

ID：0

说明：实时捕捉的音频流。

#### PG_LIVE_MEDIA_Video {#pg-live-media-video}

ID：1

说明：实时捕捉的视频流。

#### PG_LIVE_MEDIA_AVI {#pg-live-media-avi}

ID：2

说明：播放AVI文件。控件目前支持的AVI视频/音频格式为：

_音频：PCM或G.711A编码、16bit采样、采样速率11 KHz、单通道。_

_视频：MJPEG(A)、VP8视频压缩格式。_

如果你的AVI文件格式不符合，请先用工具转换成以上的格式后再播放。

### 5) 常量：媒体流的控制动作 {#5}

#### PG_LIVE_CTRL_Stop {#pg-live-ctrl-stop}

ID：0

说明：停止播放或收看

#### PG_LIVE_CTRL_Play {#pg-live-ctrl-play}

ID：1

说明：开始播放或收看

#### PG_LIVE_CTRL_Pause {#pg-live-ctrl-pause}

ID：2

说明：暂停播放或收看（未实现）

#### PG_LIVE_CTRL_Position {#pg-live-ctrl-position}

ID：3

说明：跳到指定位置进行播放或收看（未实现）。

#### PG_LIVE_CTRL_JpegPull {#pg-live-ctrl-jpegpull}

ID：4

说明：直播使用MJPEG的视频编码格式时，如果帧率设置得很低，但又想立即看到最新的图像，则可以调用此操作，让中间件立即发送一帧图像。

### 6) 说明：媒体流的初始化 {#6}

#### 实时音频流的初始化

源节点的Param参数：样例：(Code){0}(Mode){0}

Code：音频压缩编码：0为PCM编码，1为G.711A编码。

Mode：音频格式：0为单声道/16Bits/11K采样

收听节点的Param参数：空（不需要参数）

#### 实时视频流的初始化 {#-0}

源节点的Param参数：样例：(Code){1}(Mode){1}(Rate){100}

Code：视频压缩编码。0为BMP，1为MJPEG，2为VP8。

Mode：视频捕捉的尺寸模式。参考“[常量：视频捕捉的尺寸模式](#4)”章节。

Rate：视频帧率，每帧的时间间隔（毫秒）。

收看节点的Param参数：样例：(Wnd){(PosX){0}(PosY){0}(SizeX){80}(SizeY){60}(Handle){2376}}

Wnd：显示视频的窗口的尺寸和句柄。

#### 播放AVI文件的初始化 {#avi}

源节点的Param参数：样例：(Path){d:\temp\xxxx.avi}

Path：AVI文件的路径（受沙盒控制）。

收看节点的Param参数：样例：(Wnd){(PosX){0}(PosY){0}(SizeX){80}(SizeY){60}(Handle){7654}}

Wnd：显示视频的窗口的尺寸和句柄。

### 7）扩展选项 {#7}

#### PG_OPTION_LIVE_RelayNum {#pg-option-live-relaynum}

Item：0

说明：允许把媒体流同时转发给下一级节点的个数。

格式：(Item){0}(Value){2}

范围：影响当前的直播类对象。

#### PG_OPTION_LIVE_NearSize {#pg-option-live-nearsize}

Item：1

说明：设置邻近节点的个数。直播对象只与邻近节点交换状态信息，只从邻近节点获取媒体流。

格式：(Item){1}(Value){8}

范围：影响当前的直播类对象。

#### PG_OPTION_LIVE_AttachCameraNo {#pg-option-live-attachcamerano}

Item：2

说明：给直播对象绑定一个摄像头编号，该直播对象使用该摄像头采集的视频源。

格式：(Item){2}(Value){0}，Value的值： 摄像头编号0、1、2、3、……

范围：影响当前的直播类对象。