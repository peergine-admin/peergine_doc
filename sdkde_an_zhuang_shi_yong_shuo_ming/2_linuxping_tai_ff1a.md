## 2\. Linux平台： {#2-linux}

NPAPI插件：可执行文件为libpgnpp-plugin.so，复制到/usr/lib/mozilla/plugins目录后就可以在浏览器中调用Peergine的API。

JNI插件：可执行文件为libpgJNI.so，将其路径添加到PATH环境变量中。

JNI类库：pgJNILib.jar包文件，包含了pgJNI、pgJNINode和pgJNINodeProc共3个java类。将其路径添加到CLASSPATH环境变量中，就可以在Java应用程序中调用Peergine的API。