A tool to auto-compile & install KCPTUN for SS/SSR on Linux
##一键安装KCPTUN for SS/SSR on Linux。
脚本是业余爱好，英文属于文盲，写的不好，欢迎您批评指正。

##目录

致谢
已测试平台
安装前的准备工作
安装
安装命令
安装教程
Shadowsocks-libev + KCPTUN
ShadowsocksR + KCPTUN
防火墙设置示例
更新
卸载
##致谢

感谢秋水逸冰，一键安装脚本中很多代码都是从秋水的脚本中借鉴过来的，在此感谢大神们的付出。

##已测试平台

序号	测试系统	系统版本
1	debian	7
2	debian	8
3	centos	6
4	centos	7
5	ubuntu	16.04
6	ubuntu	14.04
7	ubuntu	12.04
##安装前的准备工作

命令都是在你的服务器上运行的，
首先你要知道如何通过SSH远程登录到你的服务器上 SSH教程
其次安装时间较长，建议使用screen进行安装 screen教程
最后要会一点点的VI(VIM)编辑器使用方法 VI/VIM教程

##安装
###安装命令

    wget --no-check-certificate -O ./kcptun_for_ss_ssr-install.sh https://raw.githubusercontent.com/onekeyshell/kcptun_for_ss_ssr/master/kcptun_for_ss_ssr-install.sh
    chmod 700 ./kcptun_for_ss_ssr-install.sh
    ./kcptun_for_ss_ssr-install.sh install
###安装教程
####Shadowsocks-libev + KCPTUN

本教程以Debian 8为例，运行脚本时会自动检测脚本是否有更新，如有更新会自动更新，然后需要再次运行脚本继续。
通过SSH登录到你的服务器上后，将安装命令一行一行的复制到你的服务器上：

运行脚本时会自动检测脚本是否有更新，如有更新会自动更新，然后需要再次运行脚本继续。

如果脚本是最新的，那么就会然你选择安装的内容：

输入SS的基本信息


输入KCP的基本信息


安装是一个漫长的过程，如果一切顺利，最后会提示你所有的配置信息，按照信息配置你的客户端就可以了
最后要说明的是如果你有防火墙设置，请将你用的端口都添加进去。

####ShadowsocksR + KCPTUN

本教程以Debian 8为例，运行脚本时会自动检测脚本是否有更新，如有更新会自动更新，然后需要再次运行脚本继续。
通过SSH登录到你的服务器上后，将安装命令一行一行的复制到你的服务器上：

运行脚本时会自动检测脚本是否有更新，如有更新会自动更新，然后需要再次运行脚本继续。

如果脚本是最新的，那么就会然你选择安装的内容：

输入SSR的基本信息


输入KCP的基本信息


安装是一个漫长的过程，如果一切顺利，最后会提示你所有的配置信息，按照信息配置你的客户端就可以了
最后要说明的是如果你有防火墙设置，请将你用的端口都添加进去。

####防火墙设置示例

centos7（请替换命令里的端口）：

firewall-cmd --permanent --zone=public --add-port=端口/tcp
firewall-cmd --permanent --zone=public --add-port=端口/udp
firewall-cmd --reload
centos6（请替换命令里的端口）：

iptables -I INPUT -m state --state NEW -m tcp -p tcp --dport 端口 -j ACCEPT
iptables -I INPUT -m state --state NEW -m udp -p udp --dport 端口 -j ACCEPT
/etc/init.d/iptables save
/etc/init.d/iptables restart
Debian/Ubuntu（请替换命令里的端口）：

iptables -I INPUT -m state --state NEW -m tcp -p tcp --dport 端口 -j ACCEPT
iptables -I INPUT -m state --state NEW -m udp -p udp --dport 端口 -j ACCEPT

#下面这些代码是让Debian/Ubuntu关机自动备份Iptables和启动自动加载Iptables
echo '#!/bin/bash' > /etc/network/if-post-down.d/iptables && \
echo 'iptables-save > /etc/iptables.rules' >> /etc/network/if-post-down.d/iptables && \
echo 'exit 0;' >> /etc/network/if-post-down.d/iptables && \
chmod +x /etc/network/if-post-down.d/iptables && \

echo '#!/bin/bash' > /etc/network/if-pre-up.d/iptables && \
echo 'iptables-restore < /etc/iptables.rules' >> /etc/network/if-pre-up.d/iptables && \
echo 'exit 0;' >> /etc/network/if-pre-up.d/iptables && \
chmod +x /etc/network/if-pre-up.d/iptables
##更新

    ./kcptun_for_ss_ssr-install.sh update
##卸载

    ./kcptun_for_ss_ssr-install.sh uninstall
© 2020 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About
