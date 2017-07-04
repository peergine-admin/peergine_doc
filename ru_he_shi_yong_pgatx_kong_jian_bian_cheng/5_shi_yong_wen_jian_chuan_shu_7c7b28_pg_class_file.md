## 5\. 使用文件传输类(PG_CLASS_File) {#5-pg-class-file}

### 1) 两点文件传输 {#1}

文件传输类提供了两点之间传输文件的功能。方法PG_METH_FILE_Put和PG_METH_FILE_Get分别为上传和下传文件。方法PG_METH_FILE_Cancel中断一个正在进行的文件传输。方法PG_METH_FILE_Status上报文件传输的状态。开始传输时，可以通过Offset和Size参数指定只传输文件的一个片段。进行多次传输不同的片段可以组成一个断点续传的过程。参考“

PG_CLASS_File类

”章节。