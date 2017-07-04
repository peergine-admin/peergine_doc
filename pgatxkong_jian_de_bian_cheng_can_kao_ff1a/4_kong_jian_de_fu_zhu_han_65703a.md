## 4\. 控件的辅助函数: {#4}

### 1) String utilGetWndRect() {#1-string-utilgetwndrect}

**描述：**

获取控件窗口的尺寸和句柄。

**参数：**

无

**返回值：**

[字符串] 控件窗口的尺寸和句柄信息，OML格式。

格式样例：(PosX){0}(PosY){0}(SizeX){60}(SizeY){80}(Handle){9847387}

**示例(JavaScript)：**

// 打开一个本地视频预览，并在控件窗口上显示预览图像。

pgAtx.ObjectAdd(“VideoPreview”, “PG_CLASS_Video”, “”, 0x2);

var sWndEle = pgAtx.utilGetWndRect();

var sInEle = “(Code){0}(Mode){0}(Rate){200}(Wnd){” + sWndEle + “}”;

pgAtx.ObjectRequest(“VideoPreview”, 32, sInEle, “OpenPreview”);

### 2) String utilCmd(sCmd, sParam) {#2-string-utilcmd-scmd-sparam}

**描述：**

执行控件命令的函数。

**参数：**

sCmd：命令名，参考“

控件的命令列表

”章节。

sParam：命令参数

**返回值：**

[字符串] 返回命令执行的结果。

**示例(JavaScript)：**

// 弹出文件选择对话框

var sRes = pgAtx.utilCmd(“DlgFile”, “(Open){1}(Ext){}(File){}(Flag){0}(Filter){}”);