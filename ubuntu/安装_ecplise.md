# 安装ecplise

## 下载软件包

## 解压 
解压软件到你创建的文件夹中
## 创建启动图标

要给软件添加启动图标，可到/usr/share/applications目录下创建相应的配置文件，以下为给eclipse配置启动图标示例：
命令行进入/usr/share/applications目录

`cd /usr/share/applications`

添加文件eclipse.desktop

`sudo vim eclipse.desktop`

添加内容

~~~
[Desktop Entry]
Name=eclipse
Name[zh_CN]=eclipse
Comment=eclipse Client
Exec=/home/yanghao/eclipse/eclipse
Icon=/home/yanghao/eclipse/icon.xpm
Terminal=false
Type=Application
Categories=Application;
Encoding=UTF-8
StartupNotify=true
~~~

Exec 和 Icon 后面的代码需要根据你 eclipse 的实际安装的位置替换（Exec就是启动软件的可执行文件位置，Icon就是要显示的启动图标位置，icon可以是jpg、png、svg等格式）。

