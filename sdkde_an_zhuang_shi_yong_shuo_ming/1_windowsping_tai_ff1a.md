## 1\. Windows平台： {#1-windows}

ActiveX控件：可执行文件为pgATX.ocx，使用regsvr32命令注册后就可以在浏览器和WSH中调用Peergine的API。

NPAPI插件：可执行文件为nppgnpp.dll，复制到Chrome、Firefox和Safari的plugins目录后就可以在浏览器中调用Peergine的API。

JNI插件：可执行文件为pgJNI.dll，将其路径添加到PATH环境变量中。

JNI类库：pgJNILib.jar包文件，包含了pgJNI、pgJNINode和pgJNINodeProc共3个java类。将其路径添加到CLASSPATH环境变量中，就可以在Java应用程序中调用Peergine的API。