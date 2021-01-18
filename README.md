**这里是搭建主流科学上网的优化配置及最优组合示例。如是不太了解科学上网，建议先依次从简单到复杂参考及部署。**  
1. 示例实现了端口转发到进程转发及PROXY protocol的从低到高（效率）应用支持。
2. 示例实现了端口回落\分流到进程回落\分流及PROXY protocol的从低到高（效率）应用支持。
3. 示例实现了nginx SNI/caddy2 SNI/haproxy SNI及v2ray SNI的端口分流到进程分流及PROXY protocol的从低到高（效率）应用支持。
4. nginx SNI分流实现了tcp/udp分流，为fullcone应用提供了基础。
5. naiveproxy除进程监听（server进程）外，实现了支持h3代理应用，即quic协议传输。
6. 除v2ray(vless\vmess+kcp+seed)示例外，所有示例实现了回落或反代网站都支持http自动跳转到https，且SSL/TLS安全评估报告为A+。
7. caddy2实现了Caddyfile配置开启h2c server、PROXY protocol、naiveproxy等应用支持，让caddy2配置简单化。
8. caddy2实现了json配置SNI分流应用，且同时支持端口或进程分别PROXY protocol发送，灵活性等同haproxy SNI分流。
* **注：** 端口转发、端口回落\分流、SNI的端口分流指基于local loopback应用，不同应用实现的方式；进程转发、进程回落\分流、SNI的进程分流指基于Unix Domain Socket应用，不同应用实现的方式。

### 服务端单一应用配置示例
1. [v2ray(vless\vmess+kcp+seed)](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%5Cvmess%2Bkcp%2Bseed)) （vless或vmess的kcp应用。若网络极差，推荐部署。）  
2. [v2ray(vless\vmess+ws)+caddy2\nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%5Cvmess%2Bws)%2Bcaddy2%5Cnginx) （caddy2或nginx反向代理vless或vmess的ws应用。）  
3. [v2ray(socks\shadowsocks+ws)+caddy2\nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(socks%5Cshadowsocks%2Bws)%2Bcaddy2%5Cnginx) （caddy2或nginx反向代理socks或shadowsocks的ws应用。）  
4. [v2ray(vless\vmess+h2c)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%5Cvmess%2Bh2c)%2Bcaddy2) （caddy2反向代理vless或vmess的h2应用。）  
5. [v2ray(SS+v2ray-plugin)+caddy2\nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(SS%2Bv2ray-plugin)%2Bcaddy2%5Cnginx) （caddy2或nginx反向代理shadowsocks加v2ray-plugin的ws应用。）  
6. [v2ray(vless+tcp+tls)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%2Btcp%2Btls)%2Bcaddy2) （vless的tcp应用，web回落给caddy2。）  
7. [v2ray(vless+tcp+tls)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%2Btcp%2Btls)%2Bnginx) （vless的tcp应用，web回落给nginx。）  
8. [v2ray(trojan+tcp+tls)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(trojan%2Btcp%2Btls)%2Bcaddy2) （兼容trojan应用，web回落给caddy2。）  
9. [v2ray(trojan+tcp+tls)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(trojan%2Btcp%2Btls)%2Bnginx) （兼容trojan应用，web回落给nginx。）  
10. [v2ray(trojan+ws)+caddy2\nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(trojan%2Bws)%2Bcaddy2%5Cnginx) （caddy2或nginx反向代理兼容trojan-go的ws应用。） 
---
1. [trojan\trojan-go+caddy2\naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/trojan%5Ctrojan-go%2Bcaddy2%5Cnaiveproxy) （trojan或trojan-go应用，web回落给caddy2，或加naiveproxy应用。）  
2. [trojan\trojan-go+nginx](https://github.com/lxhao61/integrated-examples/tree/master/trojan%5Ctrojan-go%2Bnginx) （trojan或trojan-go应用，web回落给nginx。）  
---
1. [naiveproxy(caddy2+forwardproxy)](https://github.com/lxhao61/integrated-examples/tree/master/naiveproxy(caddy2%2Bforwardproxy)) （naiveproxy应用，基于h2或h3代理。）  

### 服务端综合应用配置示例
#### &emsp;v2ray或Xray为主、caddy2为辅及其它应用。
1. [v2ray(complete+h2c-tcp)+caddy2\naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c-tcp)%2Bcaddy2%5Cnaiveproxy) （caddy2反向代理ws与h2的综合应用，或加naiveproxy应用。）  
---
1. [v2ray(vless+tcp&ws+tls)+caddy2\naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%2Btcp%26ws%2Btls)%2Bcaddy2%5Cnaiveproxy)（vless的tcp与ws应用，web回落给caddy2，或加naiveproxy应用。）  
2. [v2ray(complete+h2c)+caddy2\naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c)%2Bcaddy2%5Cnaiveproxy) （v2ray或Xray综合应用加反向代理h2应用，或加naiveproxy应用。）  
3. [v2ray(complete+h2c)+naiveproxy+trojan](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c)%2Bnaiveproxy%2Btrojan) （上一项应用加trojan应用及caddy2 SNI共用端口。）  
---
1. [v2ray(vless&trojan+tcp&ws+tls)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%26trojan%2Btcp%26ws%2Btls)%2Bcaddy2) （回落终极部署/套娃方式，或caddy2 SNI共用端口。）  
2. [v2ray(complete+trojan+h2c)+naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Btrojan%2Bh2c)%2Bnaiveproxy) （v2ray或Xray全部应用加naiveproxy应用及caddy2 SNI共用端口。）  
#### &emsp;v2ray或Xray为主、nginx为辅及其它应用。  
1. [v2ray(complete-tcp)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete-tcp)%2Bnginx) （nginx反向代理ws的综合应用。）  
---
1. [v2ray(vless+tcp&ws+tls)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%2Btcp%26ws%2Btls)%2Bnginx) （vless的tcp与ws类应用，web回落给nginx。）  
2. [v2ray(complete)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete)%2Bnginx) （v2ray或Xray综合应用。）  
3. [v2ray(complete)+nginx+trojan](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete)%2Bnginx%2Btrojan) （上一项应用加trojan应用及nginx SNI共用端口。）  
---
1. [v2ray(vless&trojan+tcp&ws+tls)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%26trojan%2Btcp%26ws%2Btls)%2Bnginx) （回落终极部署/套娃方式，或nginx SNI共用端口。）  
2. [v2ray(complete+trojan)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Btrojan)%2Bnginx) （加trojan的v2ray或Xray综合应用及nginx SNI共用端口。）  
#### &emsp;平衡及兼顾优势的综合应用。
1. [v2ray(complete+h2c)+naiveproxy+trojan+haproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c)%2Bnaiveproxy%2Btrojan%2Bhaproxy) （用nginx或haproxy对各应用SNI分流，平衡及兼顾优势。）  
---
1. [v2ray(complete+trojan+h2c)+naiveproxy+haproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Btrojan%2Bh2c)%2Bnaiveproxy%2Bhaproxy) （用nginx或haproxy对各应用SNI分流，平衡及兼顾优势。）  
#### 以上所有实例注意:
1. 所有v2ray或Xray配置文件都配置了禁用BT。如不需要，可以删除相关配置（参考v2ray(other configuration)中BT_config.json文件）。  
2. v2ray从版本v4.33.0删除了xtls应用，故若还想用xtls应用，请选Xray。Xray是v2ray分支，也是因为这个应用分家。   
3. complete表示包含v2ray或Xray的vless+tcp+tls、vless+ws+tls、SS+v2ray-plugin+tls、vless+kcp+seed的综合应用。  
4. 所有ws（WebSocket）类应用支持CDN加速。  
5. naiveproxy=caddy2+forwardproxy（服务端）。此程序文件已编译好，本人github下载即可。  
6. 目前caddy2的http/https服务进程监听采用Unix Domain Socket应用不支持h3。若开启h3，caddy无法启动。  

### 服务端特殊应用配置示例
1. [v2ray(other configuration)](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(other%20configuration)) （v2ray或Xray其它多种特殊应用配置方法。）  
2. [caddy2\naiveproxy(other configuration)](https://github.com/lxhao61/integrated-examples/tree/master/caddy2%5Cnaiveproxy(other%20configuration)) （caddy2及naiveproxy的特殊应用配置方法。）  
3. [nginx(other configuration)](https://github.com/lxhao61/integrated-examples/tree/master/nginx(other%20configuration)) （nginx SNI分流v2ray或Xray应用与网站应用的配置方法。） 

### 官方客户端配置示例  
&emsp;[client configuration](https://github.com/lxhao61/integrated-examples/tree/master/client%20configuration)（若使用第三方客户端参考即可。）

### systemd服务文件  
&emsp;[service configuration](https://github.com/lxhao61/integrated-examples/tree/master/service%20configuration)（配置软件服务由systemd管理。）

### 使用/贡献指南  
1. 若科学上网相关软件增加新功能，开始在服务端单一应用配置示例中添加；过一段时间稳定后才会服务端综合应用配置示例中添加。如除trojan+tcp套娃外，vless+tcp及trojan+tcp的xtls已全部加上。  
2. 欢迎你提交 PR ,如对现行配置示例优化修订，或将自己使用的配置制作模板提交等。
