v2ray tcp类应用直连，v2ray ws类应用分流一次；naiveproxy直连，v2ray h2类应用分流（反代）一次。

注意：

1、naiveproxy(caddy2) 使用本github文件，可同时支持naiveproxy及v2ray h2反向代理。

2、v2ray v4.31.0 版本及以后才支持 trojan 及完整回落。

3、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程；而v2ray的trojan不支持端口或进程分离h2回落，故回落nginx只能全部采用h1回落。

4、全部配置没有启用 PROXY protocol，仅端口回落。

5、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加stream_ssl_preread_module模块构建自定义模板，再进行源代码编译和安装。

6、配置1：v2ray、naiveproxy(caddy2))各自公开一个监听端口，各自分别或配合提供服务。配置2：nginx为v2ray vless+tcp、v2ray trojan、naiveproxy(caddy2)进行SNI分流（四层转发），实现共用443端口。
