# 安装jdk安装 OpenJDK 8

## 安装过程
Java 8，前一个 Java LTS 版本，目前仍被广泛应用。如果你的应用运行在 Java 8 上，你可以通过输入下面的命令，安装它：sudo apt update
```
sudo apt install openjdk-8-jdk
```
运行时会发生错误，**如果使用的是国外的源没有这些乱七八糟的东西**

```
正在解压 openjdk-8-jdk:amd64 (8u282-b08-0ubuntu1~16.04) ...
在处理时有错误发生：
 /tmp/apt-dpkg-install-vkw8j0/0-libpng12-0_1.2.54-1ubuntu1.1_amd64.deb
E: Sub-process /usr/bin/dpkg returned an error code (1)
root@yanghao-X550VC:/# 
```

运行以下命令解决

```
sudo add-apt-repository ppa:linuxuprising/libpng12
sudo apt update
sudo apt install libpng12-0
```

```
root@yanghao-X550VC:/# sudo add-apt-repository ppa:linuxuprising/libpng12
 libpng12-0 for Ubuntu 20.10, 20.04, 19.10 or 19.04: https://www.linuxuprising.com/2018/05/fix-libpng12-0-missing-in-ubuntu-1804.html
 更多信息： https://launchpad.net/~linuxuprising/+archive/ubuntu/libpng12
按 [ENTER] 继续或 Ctrl-c 取消安装。

命中:1 http://mirrors.aliyun.com/ubuntu xenial InRelease
获取:2 http://mirrors.aliyun.com/ubuntu xenial-updates InRelease [109 kB]
获取:3 http://mirrors.aliyun.com/ubuntu xenial-backports InRelease [107 kB]
获取:4 http://mirrors.aliyun.com/ubuntu xenial-security InRelease [109 kB]
命中:5 http://dl.google.com/linux/chrome/deb stable InRelease              
获取:6 http://mirrors.aliyun.com/ubuntu xenial-updates/main amd64 DEP-11 Metadata [327 kB]
获取:7 http://mirrors.aliyun.com/ubuntu xenial-updates/universe amd64 DEP-11 Metadata [281 kB]
获取:8 http://mirrors.aliyun.com/ubuntu xenial-updates/multiverse amd64 DEP-11 Metadata [5,960 B]
获取:9 http://mirrors.aliyun.com/ubuntu xenial-backports/main amd64 DEP-11 Metadata [3,328 B]
获取:10 http://mirrors.aliyun.com/ubuntu xenial-backports/universe amd64 DEP-11 Metadata [6,616 B]
命中:11 http://packages.microsoft.com/repos/code stable InRelease              
获取:12 http://mirrors.aliyun.com/ubuntu xenial-security/main amd64 DEP-11 Metadata [93.8 kB]
获取:13 http://mirrors.aliyun.com/ubuntu xenial-security/universe amd64 DEP-11 Metadata [130 kB]
获取:14 http://mirrors.aliyun.com/ubuntu xenial-security/multiverse amd64 DEP-11 Metadata [2,468 B]
命中:15 http://archive.canonical.com/ubuntu xenial InRelease                   
命中:16 http://archive.ubuntu.com/ubuntu xenial InRelease                      
获取:17 http://ppa.launchpad.net/linuxuprising/libpng12/ubuntu focal InRelease [15.9 kB]
获取:18 http://ppa.launchpad.net/linuxuprising/libpng12/ubuntu focal/main amd64 Packages [996 B]
获取:19 http://ppa.launchpad.net/linuxuprising/libpng12/ubuntu focal/main Translation-en [532 B]
已下载 1,192 kB，耗时 3秒 (364 kB/s)     
Can not add an empty (zero-length) key to the cache
正在读取软件包列表... 完成
```

```
sudo apt install libpng12-0
```

运行过程
~~~
root@yanghao-X550VC:/# sudo apt install libpng12-0
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
下列软件包是自动安装的并且现在不需要了：
  chromium-codecs-ffmpeg-extra gstreamer1.0-vaapi ibus-data
  libgstreamer-plugins-bad1.0-0 libva-wayland2 python3-ibus-1.0
使用'sudo apt autoremove'来卸载它(它们)。
下列【新】软件包将被安装：
  libpng12-0
升级了 0 个软件包，新安装了 1 个软件包，要卸载 0 个软件包，有 0 个软件包未被升级。
有 7 个软件包没有被完全安装或卸载。
需要下载 173 kB 的归档。
解压缩后会消耗 290 kB 的额外空间。
获取:1 http://ppa.launchpad.net/linuxuprising/libpng12/ubuntu focal/main amd64 libpng12-0 amd64 1.2.54-1ubuntu1.1+1~ppa0~focal [173 kB]
已下载 173 kB，耗时 3秒 (59.2 kB/s)  
(正在读取数据库 ... 系统当前共安装有 221793 个文件和目录。)
准备解压 .../libpng12-0_1.2.54-1ubuntu1.1+1~ppa0~focal_amd64.deb  ...
正在解压 libpng12-0:amd64 (1.2.54-1ubuntu1.1+1~ppa0~focal) ...
正在设置 java-common (0.56ubuntu2) ...
正在设置 libpng12-0:amd64 (1.2.54-1ubuntu1.1+1~ppa0~focal) ...
正在设置 fonts-dejavu-extra (2.35-1) ...
正在设置 openjdk-8-jre-headless:amd64 (8u282-b08-0ubuntu1~16.04) ...
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/rmid 来在自
动模式中提供 /usr/bin/rmid (rmid)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java 来在自
动模式中提供 /usr/bin/java (java)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/keytool 来在
自动模式中提供 /usr/bin/keytool (keytool)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/jjs 来在自动
模式中提供 /usr/bin/jjs (jjs)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/pack200 来在
自动模式中提供 /usr/bin/pack200 (pack200)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/rmiregistry 
来在自动模式中提供 /usr/bin/rmiregistry (rmiregistry)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/unpack200 来
在自动模式中提供 /usr/bin/unpack200 (unpack200)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/orbd 来在自
动模式中提供 /usr/bin/orbd (orbd)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/servertool 
来在自动模式中提供 /usr/bin/servertool (servertool)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/tnameserv 来
在自动模式中提供 /usr/bin/tnameserv (tnameserv)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/jexec 来在自
动模式中提供 /usr/bin/jexec (jexec)
正在设置 ca-certificates-java (20160321ubuntu1) ...
Adding debian:DigiCert_High_Assurance_EV_Root_CA.pem
Adding debian:DigiCert_Trusted_Root_G4.pem
Adding debian:Hellenic_Academic_and_Research_Institutions_RootCA_2015.pem
Adding debian:GTS_Root_R2.pem
Adding debian:GlobalSign_ECC_Root_CA_-_R4.pem
Adding debian:Certigna.pem
Adding debian:TUBITAK_Kamu_SM_SSL_Kok_Sertifikasi_-_Surum_1.pem
Adding debian:Global_Chambersign_Root_-_2008.pem
Adding debian:ACCVRAIZ1.pem
Adding debian:TrustCor_RootCert_CA-1.pem
Adding debian:Security_Communication_RootCA2.pem
Adding debian:ePKI_Root_Certification_Authority.pem
Adding debian:QuoVadis_Root_CA.pem
Adding debian:Security_Communication_Root_CA.pem
Adding debian:Entrust_Root_Certification_Authority_-_G4.pem
Adding debian:GlobalSign_ECC_Root_CA_-_R5.pem
Adding debian:ssl-cert-snakeoil.pem
Adding debian:Amazon_Root_CA_2.pem
Adding debian:IdenTrust_Commercial_Root_CA_1.pem
Adding debian:IdenTrust_Public_Sector_Root_CA_1.pem
Adding debian:GlobalSign_Root_CA_-_R3.pem
Adding debian:QuoVadis_Root_CA_2.pem
Adding debian:SecureSign_RootCA11.pem
Adding debian:Starfield_Root_Certificate_Authority_-_G2.pem
Adding debian:DigiCert_Assured_ID_Root_G2.pem
Adding debian:DigiCert_Assured_ID_Root_G3.pem
Adding debian:Chambers_of_Commerce_Root_-_2008.pem
Adding debian:SwissSign_Silver_CA_-_G2.pem
Adding debian:GTS_Root_R1.pem
Adding debian:Certum_Trusted_Network_CA_2.pem
Adding debian:Certum_Trusted_Network_CA.pem
Adding debian:SwissSign_Gold_CA_-_G2.pem
Adding debian:NetLock_Arany_=Class_Gold=_Főtanúsítvány.pem
Adding debian:DigiCert_Global_Root_G2.pem
Adding debian:COMODO_ECC_Certification_Authority.pem
Adding debian:Go_Daddy_Root_Certificate_Authority_-_G2.pem
Adding debian:DigiCert_Assured_ID_Root_CA.pem
Adding debian:SSL.com_Root_Certification_Authority_ECC.pem
Adding debian:SSL.com_EV_Root_Certification_Authority_RSA_R2.pem
Adding debian:AffirmTrust_Networking.pem
Adding debian:GeoTrust_Primary_Certification_Authority_-_G2.pem
Adding debian:Amazon_Root_CA_3.pem
Adding debian:Certigna_Root_CA.pem
Adding debian:certSIGN_ROOT_CA.pem
Adding debian:Buypass_Class_2_Root_CA.pem
Adding debian:T-TeleSec_GlobalRoot_Class_3.pem
Adding debian:QuoVadis_Root_CA_3.pem
Adding debian:GlobalSign_Root_CA.pem
Adding debian:SSL.com_EV_Root_Certification_Authority_ECC.pem
Adding debian:Amazon_Root_CA_4.pem
Adding debian:Staat_der_Nederlanden_EV_Root_CA.pem
Adding debian:TrustCor_RootCert_CA-2.pem
Adding debian:DigiCert_Global_Root_CA.pem
Adding debian:OISTE_WISeKey_Global_Root_GB_CA.pem
Adding debian:EC-ACC.pem
Adding debian:Hellenic_Academic_and_Research_Institutions_ECC_RootCA_2015.pem
Adding debian:Microsoft_ECC_Root_Certificate_Authority_2017.pem
Adding debian:SSL.com_Root_Certification_Authority_RSA.pem
Adding debian:Trustis_FPS_Root_CA.pem
Adding debian:VeriSign_Universal_Root_Certification_Authority.pem
Adding debian:GlobalSign_Root_CA_-_R2.pem
Adding debian:TrustCor_ECA-1.pem
Adding debian:emSign_Root_CA_-_G1.pem
Adding debian:AffirmTrust_Premium_ECC.pem
Adding debian:QuoVadis_Root_CA_1_G3.pem
Adding debian:XRamp_Global_CA_Root.pem
Adding debian:AC_RAIZ_FNMT-RCM.pem
Adding debian:GDCA_TrustAUTH_R5_ROOT.pem
Adding debian:COMODO_Certification_Authority.pem
Adding debian:USERTrust_RSA_Certification_Authority.pem
Adding debian:Starfield_Class_2_CA.pem
Adding debian:Atos_TrustedRoot_2011.pem
Adding debian:SecureTrust_CA.pem
Adding debian:CA_Disig_Root_R2.pem
Adding debian:GTS_Root_R4.pem
Adding debian:e-Szigno_Root_CA_2017.pem
Adding debian:Trustwave_Global_ECC_P256_Certification_Authority.pem
Adding debian:Starfield_Services_Root_Certificate_Authority_-_G2.pem
Adding debian:TeliaSonera_Root_CA_v1.pem
Adding debian:QuoVadis_Root_CA_2_G3.pem
Adding debian:Cybertrust_Global_Root.pem
Adding debian:DigiCert_Global_Root_G3.pem
Adding debian:Actalis_Authentication_Root_CA.pem
Adding debian:Network_Solutions_Certificate_Authority.pem
Adding debian:Trustwave_Global_ECC_P384_Certification_Authority.pem
Adding debian:Go_Daddy_Class_2_CA.pem
Adding debian:emSign_ECC_Root_CA_-_C3.pem
Adding debian:Amazon_Root_CA_1.pem
Adding debian:GlobalSign_Root_CA_-_R6.pem
Adding debian:GTS_Root_R3.pem
Adding debian:D-TRUST_Root_Class_3_CA_2_EV_2009.pem
Adding debian:D-TRUST_Root_Class_3_CA_2_2009.pem
Adding debian:Staat_der_Nederlanden_Root_CA_-_G3.pem
Adding debian:Entrust_Root_Certification_Authority.pem
Adding debian:Entrust.net_Premium_2048_Secure_Server_CA.pem
Adding debian:Buypass_Class_3_Root_CA.pem
Adding debian:E-Tugra_Certification_Authority.pem
Adding debian:UCA_Extended_Validation_Root.pem
Adding debian:SZAFIR_ROOT_CA2.pem
Adding debian:UCA_Global_G2_Root.pem
Adding debian:CFCA_EV_ROOT.pem
Adding debian:Trustwave_Global_Certification_Authority.pem
Adding debian:Hellenic_Academic_and_Research_Institutions_RootCA_2011.pem
Adding debian:Hongkong_Post_Root_CA_1.pem
Adding debian:QuoVadis_Root_CA_3_G3.pem
Adding debian:Entrust_Root_Certification_Authority_-_EC1.pem
Adding debian:OISTE_WISeKey_Global_Root_GC_CA.pem
Adding debian:Baltimore_CyberTrust_Root.pem
Adding debian:DST_Root_CA_X3.pem
Adding debian:Autoridad_de_Certificacion_Firmaprofesional_CIF_A62634068.pem
Adding debian:Microsoft_RSA_Root_Certificate_Authority_2017.pem
Adding debian:AffirmTrust_Premium.pem
Adding debian:emSign_ECC_Root_CA_-_G3.pem
Adding debian:COMODO_RSA_Certification_Authority.pem
Adding debian:NAVER_Global_Root_Certification_Authority.pem
Adding debian:TWCA_Global_Root_CA.pem
Adding debian:Sonera_Class_2_Root_CA.pem
Adding debian:emSign_Root_CA_-_C1.pem
Adding debian:Entrust_Root_Certification_Authority_-_G2.pem
Adding debian:Comodo_AAA_Services_root.pem
Adding debian:Secure_Global_CA.pem
Adding debian:certSIGN_Root_CA_G2.pem
Adding debian:USERTrust_ECC_Certification_Authority.pem
Adding debian:AffirmTrust_Commercial.pem
Adding debian:Hongkong_Post_Root_CA_3.pem
Adding debian:Izenpe.com.pem
Adding debian:Microsec_e-Szigno_Root_CA_2009.pem
Adding debian:TWCA_Root_Certification_Authority.pem
Adding debian:ISRG_Root_X1.pem
done.
正在设置 openjdk-8-jre:amd64 (8u282-b08-0ubuntu1~16.04) ...
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/policytool 
来在自动模式中提供 /usr/bin/policytool (policytool)
正在设置 openjdk-8-jdk-headless:amd64 (8u282-b08-0ubuntu1~16.04) ...
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/idlj 来在自动模
式中提供 /usr/bin/idlj (idlj)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jdeps 来在自动模
式中提供 /usr/bin/jdeps (jdeps)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/wsimport 来在自
动模式中提供 /usr/bin/wsimport (wsimport)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jinfo 来在自动模
式中提供 /usr/bin/jinfo (jinfo)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jsadebugd 来在自
动模式中提供 /usr/bin/jsadebugd (jsadebugd)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/native2ascii 来
在自动模式中提供 /usr/bin/native2ascii (native2ascii)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jstat 来在自动模
式中提供 /usr/bin/jstat (jstat)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/javac 来在自动模
式中提供 /usr/bin/javac (javac)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/javah 来在自动模
式中提供 /usr/bin/javah (javah)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/hsdb 来在自动模
式中提供 /usr/bin/hsdb (hsdb)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/clhsdb 来在自动
模式中提供 /usr/bin/clhsdb (clhsdb)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jstack 来在自动
模式中提供 /usr/bin/jstack (jstack)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jrunscript 来在
自动模式中提供 /usr/bin/jrunscript (jrunscript)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/javadoc 来在自动
模式中提供 /usr/bin/javadoc (javadoc)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/javap 来在自动模
式中提供 /usr/bin/javap (javap)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jar 来在自动模式
中提供 /usr/bin/jar (jar)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/xjc 来在自动模式
中提供 /usr/bin/xjc (xjc)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/schemagen 来在自
动模式中提供 /usr/bin/schemagen (schemagen)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jps 来在自动模式
中提供 /usr/bin/jps (jps)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/extcheck 来在自
动模式中提供 /usr/bin/extcheck (extcheck)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jarsigner 来在自
动模式中提供 /usr/bin/jarsigner (jarsigner)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/rmic 来在自动模
式中提供 /usr/bin/rmic (rmic)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jstatd 来在自动
模式中提供 /usr/bin/jstatd (jstatd)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jmap 来在自动模
式中提供 /usr/bin/jmap (jmap)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jhat 来在自动模
式中提供 /usr/bin/jhat (jhat)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jdb 来在自动模式
中提供 /usr/bin/jdb (jdb)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/serialver 来在自
动模式中提供 /usr/bin/serialver (serialver)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jfr 来在自动模式
中提供 /usr/bin/jfr (jfr)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/wsgen 来在自动模
式中提供 /usr/bin/wsgen (wsgen)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jcmd 来在自动模
式中提供 /usr/bin/jcmd (jcmd)
正在设置 openjdk-8-jdk:amd64 (8u282-b08-0ubuntu1~16.04) ...
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/appletviewer 来
在自动模式中提供 /usr/bin/appletviewer (appletviewer)
update-alternatives: 使用 /usr/lib/jvm/java-8-openjdk-amd64/bin/jconsole 来在自
动模式中提供 /usr/bin/jconsole (jconsole)
正在处理用于 fontconfig (2.13.1-2ubuntu3) 的触发器 ...
正在处理用于 desktop-file-utils (0.24-1ubuntu3) 的触发器 ...
正在处理用于 mime-support (3.64ubuntu1) 的触发器 ...
正在处理用于 hicolor-icon-theme (0.17-2) 的触发器 ...
正在处理用于 gnome-menus (3.36.0-1ubuntu1) 的触发器 ...
正在处理用于 libc-bin (2.31-0ubuntu9.2) 的触发器 ...
正在处理用于 man-db (2.9.1-1) 的触发器 ...
正在处理用于 ca-certificates (20210119~20.04.1) 的触发器 ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...

```

到这里已经安装好了
下面运行命令，查看版本

```
java -version
```
运行过程

```
root@yanghao-X550VC:/# java -version
openjdk version "1.8.0_282"
OpenJDK Runtime Environment (build 1.8.0_282-8u282-b08-0ubuntu1~16.04-b08)
OpenJDK 64-Bit Server VM (build 25.282-b08, mixed mode)
```

## 设置默认版本

如果你在你的 Ubuntu 系统上安装了多个 Java 版本，你可以输入下面的命令，检测哪个版本被设置成了默认值：java -version想要修改默认的版本，使用update-alternatives命令：s

`sudo update-alternatives --config java`

输出像下面这样：
```
root@yanghao-X550VC:/# sudo update-alternatives --config java
链接组 java (提供 /usr/bin/java)中只有一个候选项：/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
无需配置。
```

## 配置环境变量

在一些 Java 应用中，环境变量JAVA_HOME被用来表示 Java 安装位置。想要设置 JAVA_HOME 变量，首先使用
update-alternatives找到 Java 安装路径
`sudo update-alternatives --config java`
~~~
root@yanghao-X550VC:/# sudo update-alternatives --config java
链接组 java (提供 /usr/bin/java)中只有一个候选项：/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
无需配置。
~~~
一旦你发现你偏好的 Java 安装路径，打开/etc/environment文件：

`sudo nano /etc/environment`

假设你想设置 JAVA_HOME 指定到 OpenJDK 8，在文件的末尾，添加下面的行：
JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"

运行下面的命令激活变量
`source /etc/environment`

验证 JAVA_HOME 环境变量被正确设置：

`echo $JAVA_HOME`

你应该可以看到 Java 安装路径：/usr/lib/jvm/java-11-openjdk-amd64

## 卸载 

Java你可以使用 apt 卸载 Java，就像卸载任何软件包一样。例如，想要卸载default-jdk软件包，输入：sudo apt remove openjdk-11-jdk
