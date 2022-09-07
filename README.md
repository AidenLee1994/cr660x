# cr660x
SCUT-OPENWRT-CR660X
CR660x路由器破解
1.准备一台刷入openwrt的路由器（A）
1.1提交xqsystem.lua
1.用winscp把文件xqsystem.lua上传到/usr/lib/lua/luci/controller/admin/目录下

2.浏览器访问http://192.168.10.1/cgi-bin/luci/api/xqsystem/token，之后会出现code 0等字样就OK了

1.2修改路由器ip
1.在路由器 “网络->接口->LAN”中，设备IPV4为：169.254.31.1

2.忽略此端口的DHCP功能，从而关闭DHCP功能。

2.在需要刷入的cr660x的路由器（B）
2.1用电脑连接路由器，在浏览器中输入192.168.10.1，用管理密码登录路由器
管理密码在路由器背部贴纸上有写

然后记录此时路由器显示的stok

例如：stok=ab2186b95ae6335cc1326ba54e6db644

2.2 在路由器B中输入如下信息
A路由器的WIFI名称

A路由器的WIFI密码

B路由器的stok

输入格式如下：

http://192.168.10.1/cgi-bin/luci/;stok=**B路由器的stok**/api/misystem/extendwifi_connect?ssid=**A路由器的WIFI名称**&password=**A路由器的WIFI密码**

显示“code”：0的字样表示成功

2.3 在路由器B中输入如下信息
B路由器的stok

输入格式如下：

http://192.168.10.1/cgi-bin/luci/;stok=**B路由器的stok**/api/xqsystem/oneclick_get_remote_token?username=xxx&password=xxx&nonce=xxx

成功则显示 “code”:0 等字样

3.在路由器B中刷入pb-boot
3.1上传pb-boot.img到路由器B的/tmp路径
3.2 执行安装命令完成boot的安装
mtd write /tmp/pb-boot.img Bootloader

4.刷入系统
4.1进入刷机界面
按住路由器B的复位孔，然后接通电源，等待几秒，看到路由器的灯在缓慢闪烁时完成时松开复位孔

4.2提交刷机系统
openwrt: 点浏览，选openwrt-ramips-mt7621-xiaomi_mi-router-cr660x-squashfs-factory.bin，再点恢复固件，等待几分钟即可。
