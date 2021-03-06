## 6\. 使用音频传输类(PG_CLASS_Audio) {#6-pg-class-audio}

### 1) 两点模式 {#1}

音频传输类有两种模式：两点模式和会议模式，缺省为两点模式。两点模式允许经过呼叫协商之后才建立通话，一端发起请求之后，另一端可以选择接受或拒绝，只有对端选择接受后通话才建立。发起端调用PG_METH_AUDIO_Open方法发起呼叫请求，对端接收到呼叫请求后，通过返回应答的错误码来确认接受或拒绝，错误码等于0表示接受，错误码大于0表示拒绝及其原因。

两点模式时，如果音频传输对象关联的通信组对象有多个成员，则系统选择第1个成员作为对端节点。所以，为了使通信范围更加准确，建议音频传输对象关联节点对象作为对端节点，或者关联的通信组对象始终保持只有1个成员作为对端节点。

### 2) 会议模式及发言控制 {#2}

通过PG_ADD_AUDIO_Conference选项开启会议模式。会议模式下不需要呼叫过程，调用 PG_METH_AUDIO_Open方法打开对象之后就直接加入到会议中，可以跟通信组内的所有节点通话。会议模式下可以调用PG_METH_AUDIO_Speech方法来控制指定节点的发言状态。

### 3) 设置和获取音量 {#3}

调用PG_METH_AUDIO_CtrlVolume方法可设置和获取麦克风和扬声器的音量。

### 4) 实时显示音量的变化 {#4}

启用了PG_ADD_AUDIO_ShowVolume选项后，系统会调用PG_METH_AUDIO_ShowVolume方法上报在麦克风输入和扬声器输出的音频信号的音量。上报的频率为200毫秒1次，静音不会上报。应用程序可以依此在图像界面上显示输入/输出音量的变化。

### 5) 音频录制 {#5}

调用PG_METH_AUDIO_Record方法可将音频输出录制到由Path参数指定的AVI文件中。如果调用时指定Path参数为空，则停止当前正在进行的录制操作。

如果想将音频和视频录制到同一个AVI文件中，则在开始录制音频和视频时，都给Path参数指定同一个AVI文件。请参考“[视频录制](..\jie_dian_gong_neng_lei_de_bian_cheng_can_80033a\11_pgclasslive_7c7b3a.md#6)”章节。