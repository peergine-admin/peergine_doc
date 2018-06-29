## 6\. PG_CLASS_Audio类: {#6-pg-class-audio}

### 1) 描述： {#1}

音频传输类。

### 2) 选项： {#2}

#### PG_ADD_AUDIO_Conference {#pg-add-audio-conference}

掩码：0x1

说明：指定Audio对象为会议模式

#### PG_ADD_AUDIO_ShowVolume {#pg-add-audio-showvolume}

掩码：0x2

说明：使能PG_METH_AUDIO_ShowVolume方法，实时上报输入/输出的音量变化给应用层。

#### PG_ADD_AUDIO_OnlyInput {#pg-add-audio-onlyinput}

掩码：0x4

说明：设置该Audio对象为只具有单向输入的音频对象。

#### PG_ADD_AUDIO_OnlyOutput {#pg-add-audio-onlyoutput}

掩码：0x8

说明：设置该Audio对象为只具有单向输出的音频对象。用1个单向输入的音频对象与1个单向输出的音频对象，组成一条单向的音频通话会话。

#### PG_ADD_AUDIO_SendReliable {#pg-add-audio-sendreliable}

掩码：0x10

说明：启用可靠传输方式发送音频数据。

#### PG_ADD_AUDIO_NoSpeechSelf {#pg-add-audio-nospeechself}

掩码：0x20

说明：禁用本端发言。

#### PG_ADD_AUDIO_NoSpeechPeer {#pg-add-audio-nospeechpeer}

掩码：0x40

说明：禁用对端发言。

#### PG_ADD_AUDIO_MuteInput {#pg-add-audio-muteinput}

掩码：0x80

说明：音频输入静音。

#### PG_ADD_AUDIO_MuteOutput {#pg-add-audio-muteoutput}

掩码：0x100

说明：音频输出静音。

### 3) 方法： {#3}

#### PG_METH_AUDIO_Open {#pg-meth-audio-open}

ID：32

说明：打开音频传输会话

交互方式：[方式1](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#2-1)

发送请求参数：样例：(Code){0}(Mode){0}

Code：音频压缩编码：0为PCM编码，1为G.711A编码，2为AAC编码。

Mode：音频格式：0为单声道/16Bits/11025Hz采样

接收请求参数：空

发送应答参数：样例：(Code){0}(Mode){0}

Code：音频压缩编码：0为PCM编码，1为G.711A编码，2为AAC编码。

Mode：音频格式：0为单声道/16Bits/11025Hz采样

接收应答参数：空

#### PG_METH_AUDIO_Close {#pg-meth-audio-close}

ID：33

交互方式：[方式4](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#5-4)

说明：关闭音频传输会话

发送请求参数：空

接收请求参数：空

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_AUDIO_CtrlVolume {#pg-meth-audio-ctrlvolume}

ID：34

说明：调节或查询扬声器和麦克风的音量。当Type参数为0(扬声器)时，此操作影响当前音频对象的Peer参数指定的对象的放音音量。当Type参数为1(麦克风)时，此操作影响全局的录音音量。

交互方式：[方式5](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：样例：(Peer){}(Action){0}(Type){1}(Volume){0}(Max){0}(Min){0}

Peer：节点名。在会议模式中，当Type为0（扬声器）时指定控制哪个节点的音量；当Type为1（麦克风）时为空。在两点模式中为空。

Action：动作。0为查询音量，1为设置音量

Type：设备类型。0为扬声器，1为麦克风。

Volume：音量的值。范围：0 ~ 100

Max：最大音量（忽略）

Min：最小音量（忽略）

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Peer){}(Action){0}(Type){1}(Volume){0}(Max){100}(Min){0}

Peer：节点名。在会议模式中，当Type为0（扬声器）时指定控制哪个节点的音量；当Type为1（麦克风）时为空。在两点模式中为空。

Action：动作。0为查询音量，1为设置音量

Type：设备类型。0为扬声器，1为麦克风。

Volume：音量的值。范围：0 ~ 100

Max：最大音量

Min：最小音量

#### PG_METH_AUDIO_ShowVolume {#pg-meth-audio-showvolume}

ID：35

说明：实时上报输入/输出的音量变化给应用层，应用程序可以依此在界面上显示音量变化的动画。

交互方式：[方式8](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#9-8)

发送请求参数：无此操作

接收请求参数：样例：(VolMic){0}(VolSpk){0}

VolMic：当前在麦克风上输入的音量，范围：0 ~ 100

VolSpk：当前在扬声器上输出的音量，范围：0 ~ 100

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_AUDIO_Speech {#pg-meth-audio-speech}

ID：36

说明：会议发言控制

交互方式：[方式4](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#5-4)

发送请求参数：样例：(Peer){NodeA}(ActSelf){1}(ActPeer){0}

Peer：指定要进行发言控制的节点

ActSelf：本端的发言状态。0为静音，1为发言

ActPeer：对端的发言状态。0为静音，1为发言

接收请求参数：样例：(Peer){NodeA}(ActSelf){0}(ActPeer){1}

Peer：指定要进行发言控制的节点

ActSelf：本端的发言状态。0为静音，1为发言

ActPeer：对端的发言状态。0为静音，1为发言

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_AUDIO_Record {#pg-meth-audio-record}

ID：37

说明：录音到指定的avi、mov或mp4文件

交互方式：[方式5](..\jie_shao\4_kong_jian_yu_ying_yong_cheng_xu_de_jiao_hu_fang_.md#6-5)

发送请求参数：样例：(Peer){NodeA}(Path){c:\temp\xxxx.avi}(HasVideo){0}

Peer：指定进行录音的节点

Path：存储录音的avi、mov或mp4文件路径。如果此参数为空，则停止正在进行的录音。

HasVideo：同时还需要录制视频。0为只录制音频，1为同时还录制视频。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Peer){NodeA}(Path){c:\temp\xxxx.avi}

Peer：指定进行录音的节点

Path：存储录音的avi、mov或mp4文件路径

### 4）扩展选项 {#4}

#### PG_OPTION_AUDIO_MicNo {#pg-option-audio-micno}

Item：1

说明：设置缺省使用的音频输入麦克风的编号，指定使用哪个麦克风。

格式：(Item){1}(Value){1}

范围：可在任何一个“PG_CLASS_Audio”类对象上操作，影响全局。

#### PG_OPTION_AUDIO_MicSampleRate {#pg-option-audio-micsamplerate}

Item：2

说明：设置当前使用的音频采样率。由于Peergine中间件使用的音频采样率为11K赫兹，但有些设备的音频输入不支持11K的采样率。所以，本选项给中间件指定一个设备可以支持的采样率。中间件以这个采样率采集音频数据，然后再重采样成11K。（支持Android系统）

格式：(Item){2}(Value){8000}，Value为指定的采样率（Hz赫兹）。

范围：可在任何一个“PG_CLASS_Audio”类对象上操作，影响全局。

#### PG_OPTION_AUDIO_Detect {#pg-option-audio-detect}

Item：3

说明：设置音频输入静音检测的门限。

格式：”(Item){3}(Value){“ + omlEncode(“(TailLen){20}(VolGate){50}”) + “}”， TailLen：检测的尾长(音频采集包个数)，VolGate：门限电平（0 ~ 32768）。

范围：可在任何一个“PG_CLASS_Audio”类对象上操作，影响全局。

#### PG_OPTION_AUDIO_InputExternal {#pg-option-audio-inputexternal}

Item：4

说明：启用外部音频采集回调接口。

格式：(Item){4}(Value){1}，Value的值：0为禁用，1为启用。

范围：可在任何一个“PG_CLASS_Audio”类对象上操作，影响全局。

#### PG_OPTION_AUDIO_OutputExternal {#pg-option-audio-outputexternal}

Item：5

说明：启用外部音频播放回调接口。

格式：(Item){5}(Value){1}，Value的值：0为禁用，1为启用。

范围：可在任何一个“PG_CLASS_Audio”类对象上操作，影响全局。

#### PG_OPTION_AUDIO_EnableAEC {#pg-option-audio-enableaec}

Item：6

说明：启用或禁用音频回音消除功能。

格式：(Item){6}(Value){1}，Value的值：0为禁用，1为启用。

范围：可在任何一个“PG_CLASS_Audio”类对象上操作，影响全局。

#### PG_OPTION_AUDIO_SpeakerNo {#pg-option-audio-speakerno}

Item：7

说明：设置缺省使用的音频播放的扬声器编号。

格式：(Item){7}(Value){0}，Value的值：扬声器编号，缺省为0。

范围：可在任何一个“PG_CLASS_Audio”类对象上操作，影响全局。

#### PG_OPTION_AUDIO_SendReliable {#pg-option-audio-sendreliable}

Item：8

说明：启用可靠传输方法发送音频数据。

格式：(Item){8}(Value){1}，Value的值：0为不可靠传输，1为可靠传输。缺省为不可靠传输。

范围：仅对当前操作的“PG_CLASS_Audio”类对象有效。

#### PG_OPTION_AUDIO_AttachMicNo {#pg-option-audio-attachmicno}

Item：9

说明：给音频对象绑定一个麦克风编号。音频对象将使用这个麦克风编号去打开这个麦克风设备。

格式：(Item){9}(Value){1}，Value的值：麦克风编号。

范围：仅对当前操作的“PG_CLASS_Audio”类对象有效。

#### PG_OPTION_AUDIO_AttachSpeakerNo {#pg-option-audio-attachspeakerno}

Item：10

说明：给音频对象绑定一个扬声器编号。音频对象将使用这个扬声器编号去打开这个扬声器设备。

格式：(Item){10}(Value){0}，Value的值：扬声器编号。

范围：仅对当前操作的“PG_CLASS_Audio”类对象有效。

#### PG_OPTION_AUDIO_AECMobile {#pg-option-audio-aecmobile}

Item：11

说明：启用适用于移动设备的简单回音消除。

格式：(Item){11}(Value){0}，Value的值：1为简单回音消除，0为正常的回音消除。

范围：可在任何一个“PG_CLASS_Audio”类对象上操作，影响全局。

#### PG_OPTION_AUDIO_MuteInput {#pg-option-audio-muteinput}

Item：12

说明：启用或禁用音频输入的静音。

格式：(Item){12}(Value){0}，Value的值：1为启用，0为禁用。

范围：仅对当前操作的“PG_CLASS_Audio”类对象有效。

#### PG_OPTION_AUDIO_MuteOutput {#pg-option-audio-muteoutput}

Item：13

说明：启用或禁用音频输出的静音。

格式：(Item){13}(Value){0}，Value的值：1为启用，0为禁用。

范围：仅对当前操作的“PG_CLASS_Audio”类对象有效。