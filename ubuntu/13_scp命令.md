# scp 命令

```
scp -P port 01.py user@remote:/desk/01.py
```

把当前目录下的文件 01.py 复制到远程主机的 /desk 中

```
scp -P port user@remote:/desk/o1.py
```

把远程主机中 /desk/01.py 复制到本地主机的当前目录下

```
scp -r demo user@remote:desk
```

把当前目录下的 demo 复制到远程主机的 desk 中

```
scp -r user@remote:desk demo
```

把远程的 desk 目录复制到本地目录 demo 中




