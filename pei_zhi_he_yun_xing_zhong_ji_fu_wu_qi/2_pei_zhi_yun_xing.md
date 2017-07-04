## 2\. 配置运行 {#2}

Peergine中继服务器的可执行文件为pgRelay.exe，缺省的配置文件为pgRelay.cfg。缺省配置文件必须放在与pgRelay.exe相同的目录下。配置文件是一个OML格式的文本文件，可以使用文本编辑器打开编辑。如果使用其他配置文件，可以通过pgRelay.exe的命令行参数指定其他配置文件的路径。例如，在命令行提示符下执行：c:&gt;pgRelay.exe “c:\Peergine\bin\pgRelay1.cfg”。

中继服务器的配置文件的结构如下：

(MaxThread){16} //最大的转发线程数目（每个线程最多允许32条TCP连接）。

(ListenList){ //侦听端口列表，可以配置最多32个侦听端口。

(Name1){ //侦听端口1

(Type){0} //隧道类型：TCP隧道

(AddrListen){FE800000:0:01B05996:42CFB70D:7777:0} //TCP侦听地址/端口(这是个IPV6地址)

(AddrUDP4){0:0:0:127.0.0.1:0:0} //转换成UDP后的IPV4地址，端口自动分配。

(AddrUDP6){FE800000:0:01B05996:42CFB70D:0:0} //转换成UDP后的IPV6地址，端口自动分配。

}

(Name2){ //侦听端口2

(Type){1} //隧道类型：HTTP隧道

(AddrListen){0:0:0:127.0.0.1:8888:0} //TCP侦听地址/端口(这是个IPV4地址)

(AddrUDP4){0:0:0:127.0.0.1:0:0} //转换成UDP后的IPV4地址，端口自动分配。

(AddrUDP6){FE800000:0:01B05996:42CFB70D:0:0} //转换成UDP后的IPV6地址，端口自动分配。

}

}

(Node){ // 登录到集群服务器的参数，用来搭建中继服务器的集群功能（未实现）。

(SvrName){PGServer}

(SvrAddr){0:0:0:127.0.0.1:1112:0}

(CltAddr){0:0:0:127.0.0.1:1118:0}

(User){pgRelay1}

(Pass){}

(RefPeer){}

}

Peergine中继服务器应该部署在具有公网IP地址且所有节点都能到达的网络主机上。如果要使用IPV4和IPV6的转换功能，该网络主机必须具备IPV4和IPV6双栈，且IPV4和IPV6网络都能到达。