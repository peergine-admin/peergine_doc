## 7\. PG_CLASS_Video类: {#7-pg-class-video}

### 1) 描述： {#1}

视频传输类。

### 2) 标志： {#2}

#### PG_ADD_VIDEO_Conference {#pg-add-video-conference}

掩码：0x1

说明：指定该Video对象为会议模式

#### PG_ADD_VIDEO_Preview {#pg-add-video-preview}

掩码：0x2

说明：指定该Video对象为预览模式

#### PG_ADD_VIDEO_OnlyInput {#pg-add-video-onlyinput}

掩码：0x4

说明：指定该Video对象单向输入的视频对象。

#### PG_ADD_VIDEO_OnlyOutput {#pg-add-video-onlyoutput}

掩码：0x8

说明：指定该Video对象单向输出的视频对象。用1个单向输入的视频对象与1个单向输出的视频对象，组成一条单向的视频通话会话。两条方向相反的单向视频通话会话，可以组成双向的视频通话，每个方向上的单向通话可以分别配置不同的视频参数。

#### PG_ADD_VIDEO_FrameStat {#pg-add-video-framestat}

掩码：0x10

说明：启用视频帧统计信息的上报，参考“PG_METH_VIDEO_FrameStat”。

#### PG_ADD_VIDEO_DrawThread {#pg-add-video-drawthread}

掩码：0x20

说明：创建一个单独的线程来显示视频帧到视频窗口（不在UI线程里显示视频，Windows、android系统有效）。

#### PG_ADD_VIDEO_OutputExternal {#pg-add-video-outputexternal}

掩码：0x40

说明：启用外部视频播放回调接口（视频解压之后）。

#### PG_ADD_VIDEO_OutputExtCmp {#pg-add-video-outputextcmp}

掩码：0x80

说明：启用外部视频播放回调接口（视频解压之前）。

#### PG_ADD_VIDEO_FilterDecode {#pg-add-video-filterdecode}

掩码：0x100

说明：启动视频解压之后加上模糊滤镜效果。

### 3) 方法： {#3}

#### PG_METH_VIDEO_Open {#pg-meth-video-open}

ID：32

说明：打开视频传输会话

交互方式：[方式1](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#2-1)

发送请求参数：样例：(Code){0}(Mode){1}(Rate){100}(Wnd){(PosX){0}(PosY){0}(SizeX){80} (SizeY){60}(Handle){237654}}

Code：压缩编码格式。0为BMP，1为MJPEG，2为VP8，3为h264

Mode：视频捕捉的尺寸模式，参考“[常量：视频捕捉的尺寸模式](#4)”章节

Rate：指定视频捕捉的帧率，每帧的时间间隔（毫秒）。

Wnd：视频的显示位置、尺寸和窗口句柄。格式为：(PosX){0}(PosY){0}(SizeX){80}(SizeY){60} (Handle){237654}

接收请求参数：空

发送应答参数：样例：(Code){0}(Mode){1}(Rate){100}(Wnd){(PosX){0}(PosY){0}(SizeX){80} (SizeY){60}(Handle){456723}}

Code：压缩编码格式。0为BMP，1为MJPEG，2为VP8，3为h264

Mode：视频捕捉的尺寸模式，参考“[常量：视频捕捉的尺寸模式](#4)”章节

Rate：指定视频捕捉的帧率，每帧的时间间隔（毫秒）。

Wnd：视频的显示位置、尺寸和窗口句柄。格式为：(PosX){0}(PosY){0}(SizeX){80}(SizeY){60} (Handle){237654}

接收应答参数：空

#### PG_METH_VIDEO_Close {#pg-meth-video-close}

ID：33

说明：关闭视频传输会话

交互方式：[方式4](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#5-4)

发送请求参数：空

接收请求参数：空

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_VIDEO_Move {#pg-meth-video-move}

ID：34

说明：调整当前输出视频的位置和尺寸或者把当前窗口中的视频移到另外一个窗口中显示。改变坐标参数时，调整视频的位置和尺寸。改变窗口的句柄时，转移视频到另外一个窗口中显示。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#8-7)

发送请求参数：样例：(Peer){NodeA}(Wnd){(PosX){0}(PosY){0}(SizeX){40}(SizeY){30} (Handle){ 237654}}

Peer：指定要进行视频调整或移动的节点。

Wnd：调整后的位置、尺寸和窗口句柄。格式为：(PosX){0}(PosY){0}(SizeX){60}(SizeY){80} (Handle){237654}

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_VIDEO_Join {#pg-meth-video-join}

ID：35

说明：加入指定节点的视频传输到会议中，此方法只能在会议模式中使用。

交互方式：[方式1](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#2-1)

发送请求参数：样例：(Peer){NodeA}(Wnd){(PosX){0}(PosY){0}(SizeX){40}(SizeY){30} (Handle){237654}}

Peer：指定要加入视频传输的节点。

Wnd：新窗口的尺寸和句柄。格式为：(PosX){0}(PosY){0}(SizeX){60}(SizeY){80} (Handle){237654}

接收请求参数：空

发送应答参数：样例：(Peer){NodeA}(Wnd){(PosX){0}(PosY){0}(SizeX){40}(SizeY){30} (Handle){237654}}

Peer：指定要加入视频传输的节点。

Wnd：新窗口的尺寸和句柄。格式为：(PosX){0}(PosY){0}(SizeX){60}(SizeY){80} (Handle){237654}

接收应答参数：空

#### PG_METH_VIDEO_Leave {#pg-meth-video-leave}

ID：36

说明：指定节点的视频传输从会议离开，此方法只能在会议模式中使用。

交互方式：[方式4](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#5-4)

发送请求参数：样例：(Peer){NodeA}

Peer：离开操作的节点。

接收请求参数：空

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_VIDEO_Camera {#pg-meth-video-camera}

ID：37

说明：抓拍指定节点视频的照片到指定的jpg文件

交互方式：[方式5](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：样例：(Peer){NodeA}(Path){d:\Pic1.jpg}

Peer：指定要对其进行拍照的节点。

Path：指定保存照片文件的路径，后缀必须为“jpg”。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Peer){NodeA}(Path){d:\Pic1.jpg}

Peer：指定要对其进行拍照的节点。

Path：指定保存照片文件的路径，后缀必须为“jpg”。

#### PG_METH_VIDEO_Record {#pg-meth-video-record}

ID：38

说明：录制指定节点的视频到指定的avi、mov或mp4文件。

交互方式：[方式5](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：样例：(Peer){NodeA}(Path){c:\temp\xxxx.avi}(HasAudio){0}

Peer：指定要对其进行录像的节点。

Path：指定保存avi、mov或mp4文件的路径，后缀可以为“avi”、“mov”或“mp4”。如果此参数为空，则停止正在进行的录像。

HasAudio：同时还需要录制音频。0为只录制视频，1为同时录制视频。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Peer){NodeA}(Path){c:\temp\xxxx.avi}

Peer：指定要对其进行录像的节点。

Path：指定保存avi、mov或mp4文件的路径，后缀必须为可以为“avi”、“mov”或“mp4”。

#### PG_METH_VIDEO_Transfer {#pg-meth-video-transfer}

ID：39

说明：暂停或者继续视频发送。

交互方式：[方式7](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：样例：(Peer){NodeA}(Local){1}(Remote){0}

Peer：指定要对其视频发送控制的节点。

Local：本端视频的控制。1为允许发送，0为暂停发送

Remote：对端视频的控制。1为允许发送，0为暂停发送

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_VIDEO_FrameStat {#pg-meth-video-framestat}

ID：40

说明：上报视频发送状态的统计信息。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：无此操作

接收请求参数：样例：(Peer){NodeA}(Total){2365}(Drop){0}

Peer：指定上报视频统计的节点。

Total：总发送的视频帧数

Drop：丢弃的视频帧数

发送应答参数：无此操作

接收应答参数：无此操作。

### 4) 常量：视频捕捉的尺寸模式 {#4}

#### PG_VIDEO_MODE_80x60 {#pg-video-mode-80x60}

ID：0

说明：80 x 60像素

#### PG_VIDEO_MODE_160x120 {#pg-video-mode-160x120}

ID：1

说明：160 x 120像素

#### PG_VIDEO_MODE_320x240 {#pg-video-mode-320x240}

ID：2

说明：320 x 240像素

#### PG_VIDEO_MODE_640x480 {#pg-video-mode-640x480}

ID：3

说明：640 x 480像素

#### PG_VIDEO_MODE_800x600 {#pg-video-mode-800x600}

ID：4

说明：800 x 600像素

#### PG_VIDEO_MODE_1024x768 {#pg-video-mode-1024x768}

ID：5

说明：1024 x 768像素

#### PG_VIDEO_MODE_176x144 {#pg-video-mode-176x144}

ID：6

说明：176x144像素

#### PG_VIDEO_MODE_352x288 {#pg-video-mode-352x288}

ID：7

说明：352x288像素

#### PG_VIDEO_MODE_704x576 {#pg-video-mode-704x576}

ID：8

说明：704x576像素

#### PG_VIDEO_MODE_854x480 {#pg-video-mode-854x480}

ID：9

说明：854x480像素

#### PG_VIDEO_MODE_1280x720 {#pg-video-mode-1280x720}

ID：10

说明：1280x720像素

#### PG_VIDEO_MODE_1920x1080 {#pg-video-mode-1920x1080}

ID：11

说明：1920x1080像素

### 5）扩展选项 {#5}

#### PG_OPTION_VIDEO_CameraNo {#pg-option-video-camerano}

Item：0

说明：设置当前使用的摄像头编号，指定使用哪个摄像头（前置、后置，或者摄像头编号）。

格式：(Item){0}(Value){1}

范围：可在任何一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_CameraFormat {#pg-option-video-cameraformat}

Item：1

说明：有些Android设备上，调用Android API查询到的视频格式与实际采集到的视频格式是不一样的。这将导致中间件不能正确处理视频。这个选项告诉中间件实际采集到的视频的格式，替代用Android API查询到的视频格式，使中间件能正确处理视频。（支持Android系统）

格式：(Item){1}(Value){1}，Value的值指定了视频格式的编号：1为YVYU、2为YUYV、3为YUV420SP、4为YUV422SP、5为I420、6为YV12。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_CameraRotate {#pg-option-video-camerarotate}

Item：2

说明：在Android设备上纵向采集视频时，图像确实是纵向采集的。但图像却是横向保存在内存里的，需要在内存里做一次90度的图像旋转，图像显示时才是纵向的。（支持Android、IOS系统）

格式：(Item){2}(Value){90}，Value的值指定了旋转的角度。支持90、180和270。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_CameraConvert {#pg-option-video-cameraconvert}

Item：3

说明：由于中间件只规定了几种常见的视频图像尺寸，只有规定的尺寸中间件才能处理。但是Android上视频采集摄像头的规格多种多样，五花八门，有些Android平板上可以外接USB摄像头，情况就更复杂了。所以，当中间件所规定的尺寸摄像头都不支持时，视频采集将失败。通过这个扩展选项，告诉中间件一个摄像头能够支持的尺寸，让中间件使用这个尺寸去初始化摄像头，采集出视频后，再将图像转换成中间件规定的尺寸，问题就解决了。（支持Android系统）

格式：“(Item){3}(Value){” + Node.omlEncode(“(Mode){1}(Width){380}(Height) {260}”) + “}”，其中Mode为中间件规定的尺寸模式（参考“[常量：视频捕捉的尺寸模式](#4)” ）， Width和Height为摄像头实际支持的采集尺寸。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_CameraRate {#pg-option-video-camerarate}

Item：4

说明：设置摄像头的采集帧率。

格式：(Item){4}(Value){40}，Value的值为每帧的间隔（毫秒）。例如：1000 / 40 = 25帧/秒。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_ParamCommon {#pg-option-video-paramcommon}

Item：5

说明：设置通用的视频编码相关参数。（其中参数BitRate、KeyFrmRate和LossAllow只对VP8和H264视频编码有效）。

格式：“(Item){5}(Value){” + Node.omlEncode(“(BitRate){512}(FrmRate){40}(KeyFrmRate){3000} (LossAllow){0}”) + “}”。BitRate 为码率（Kbps，默认为512）。FrmRate 为帧率（帧间时间间隔，毫秒，默认为40）。KeyFrmRate 为I帧率（I帧间时间间隔，毫秒，默认为3000）。LossAllow为播放时允许连续丢帧数（缺省为0，允许丢帧会产生花屏）。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_ParamCodeMode {#pg-option-video-paramcodemode}

Item：6

说明：为每种视频编码和尺寸设置视频编码相关参数。当此参数不为0时，使用此参数，否则使用通用的视频编码相关参数。

格式：“(Item){5}(Value){” + Node.omlEncode(“(Code){3}(Mode){2}(BitRate){0}(FrmRate){0} (KeyFrmRate){0}(LossAllow){0}”) + “}”。 Code为编码类型（1为MJPEG，2为VP8，3为h264）。Mode为图像尺寸模式（参考“[常量：视频捕捉的尺寸模式](#4)”）。BitRate、FrmRate、KeyFrmRate和LossAllow的格式参考通用的视频编码相关参数。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_JitterDelay {#pg-option-video-jitterdelay}

Item：7

说明：设置消除网络传输抖动的延时时间。

格式：(Item){7}(Value){500}，Value的值为消抖延时的时间（毫秒）。缺省为300毫秒。

范围：在需要调整消抖时延的“PG_CLASS_Video”类对象上操作，只影响该对象。

#### PG_OPTION_VIDEO_InputExternal {#pg-option-video-inputexternal}

Item：8

说明：开启视频数据的外部输入接口。启用以后应用程序在中间件外部采集压缩视频数据，然后通过API输入到中间件中。

格式：(Item){8}(Value){1}，Value的值：0为禁用，1为启用。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_CameraEnable {#pg-option-video-cameraenable}

Item：9

说明：临时禁用和启用摄像头。

格式：(Item){9}(Value){1}，Value的值：0为禁用，1为启用。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_FillMode {#pg-option-video-fillmode}

Item：10

说明：设置视频输出匹配窗口的模式。

格式：(Item){10}(Value){0}，Value的值： 0为剪裁，1为整幅，2为拉伸。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_OutputExternal {#pg-option-video-outputexternal}

Item：11

说明：启用外部视频播放回调接口（视频解压之后）。

格式：(Item){11}(Value){0}，Value的值：0为禁用，1为启用。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_RedefModeSize {#pg-option-video-redefmodesize}

Item：12

说明：修改指定分辨率模式的宽度和高度。

格式：“(Item){12}(Value){” + Node.omlEncode(“(Mode){2}(Width){480}(Height){640}”) + “}”，Value的值：Mode：需要修改分辨率的模式，Width：新的宽度，Height：新的高度。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。重要：修改分辨率模式的宽度和高度，必须在打开第一个视频对象之前修改才有效。

#### PG_OPTION_VIDEO_OutputExtCmp {#pg-option-video-outputextcmp}

Item：13

说明：启用外部视频播放回调接口（视频解压之前）。

格式：(Item){10}(Value){0}，Value的值： 0为禁用，1为启用。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_FlashLight {#pg-option-video-flashlight}

Item：14

说明：打开或关闭摄像头闪光灯（对android系统后置摄像头有效）。

格式：(Item){14}(Value){0}，Value的值： 0为关闭闪光灯，1为打开闪光灯。

范围：可在任意一个“PG_CLASS_Video”类对象上操作，影响全局。

#### PG_OPTION_VIDEO_AttachCameraNo {#pg-option-video-attachcamerano}

Item：15

说明：给视频对象绑定一个摄像头编号，该视频对象使用该摄像头采集的视频源。

格式：(Item){15}(Value){0}，Value的值： 摄像头编号0、1、2、3、……。

范围：仅对操作的“PG_CLASS_Video”类对象有效。

### 6) Android视频采集扩展选项说明 {#6-android}

由于在Android上的视频采集场景比较多样，Peergine中间件提供扩展选项设置接口，通过PG_METH_COMMON_SetOption方法设置视频采集的参数，以适应多种视频采集的场景。

Android上设置视频采集选项的原因一般有以下两个方面：

*   正常使用需要：选择前置/后置摄像头，指定横屏/纵屏采集视频。
*   弥补设备的缺陷：有些小厂商开发的Android平板或手机的设备驱动程序适配不完整或者不正确，导致调用Android API无法正确访问设备。需要中间件做一个转换适配层后，才能正确使用。

使用扩站选项设置视频采集参数的时机是：PG_CLASS_Video类型的对象生命周期的任何时候。参考例程(Java)：

// P2P 节点Node添加一个PG_CLASS_Video类型的对象“Video1”

Node.ObjectAdd(“Video1”, “PG_CLASS_Video, “”, 0);

// 调用PG_METH_COMMON_SetOption方法，设置扩展选型，旋转图像90度

Node.ObjectRequest(“Video1”, 2, “(Item){2}(Value){90}”, “”);

// 删除对象

Node.ObjectDelete(“Video1”);