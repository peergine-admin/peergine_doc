## 4\. 使用消息传输类(PG_CLASS_Data) {#4-pg-class-data}

### 1) 多点消息传输 {#1}

节点类提供两点之间消息传输功能。消息传输类提供多点之间的消息传输功能。调用PG_METH_DATA_Message方法可以给所关联的通信组成员的发送单向的消息，消息的内容完全由应用程序决定，控件透明传输。参考“[PG_CLASS_Data类](#4-pg-class-data)”章节