# 忽略文件

一些文件使我们不想上传到版本库的，忽略它们可以屏蔽不同 IDE 之间的差异

## 如何忽略

以下是 Ubuntu 上的操作 

在终端打开仓库目录

1.创建忽略规则文件

```
touch .gitignore
```

2.写入模板

```
vim .gitignore

# Complied class file
*.class

# Log file
*.log

# Moblie Tools for java (J2ME)
.mtj.tmp/

# Package File #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar

# virtual machine crash logs, see http://www.java.com/en/download/help/error_hostpot.xml

hs_err_pid*

.classpath
.project
.settings
target
.idea
*.iml
```
Windows 上是 

1.创建忽略文件 xx.ignore

2.引用忽略文件，打开 ./gitconfig
添加
```
[core]
     excluesfile=address
```