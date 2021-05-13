# 在服务器上安装 v2ray

## 下载 v2ray 

下载 v2ray 到本地电脑上

上传文件到国内的服务器上

v2ray-linux-64.zip

## 解压文件夹

解压文件 v2ray-linux-64.zip

你会得到以下文件
```
config.json  geosite.dat  v2ctl   vpoint_socks_vmess.json

geoip.dat    systemd      v2ray        vpoint_vmess_freedom.json
```
下面配置文件

- /usr/bin/v2ray/v2ray：V2Ray 程序；
- /usr/bin/v2ray/v2ctl：V2Ray 工具；
- /etc/v2ray/config.json：配置文件；
- /usr/bin/v2ray/geoip.dat：IP 数据文件
- /usr/bin/v2ray/geosite.dat：域名数据文件

mv /root/test/v2ray /usr/bin/v2ray
mv /root/test/v2ctl /usr/bin/v2ray
mv /root/test/geoip.dat /usr/bin/v2ray
mv /root/test/geosite.dat /usr/bin/v2ray

mv /root/test/ /etc/v2ray/


/etc/systemd/system/v2ray.service: Systemd
/etc/init.d/v2ray: SysV


chmod x 