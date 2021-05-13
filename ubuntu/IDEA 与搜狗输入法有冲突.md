# 方法 一

更换 jeritan runtime

## 下载编译好的 jetbrainruntime

下载 jetbrainruntime 解压到自建文件夹中

## 在 idea.sh 中导入 jdk 

```
cd /usr/local/bin/idea-IU-211.6693.111/bin

sudo vim idea.sh
```
在文件的开头添加
```
export IDEA_JDK=/home/yanghao/jdk11/java-11.0.7-jetbrain
```

## 重启软件