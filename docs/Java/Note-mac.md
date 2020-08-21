#### 前言

- 查看本机的Ip地址
```
ifconfig | grep "inet " | grep -v 127.0.0.1
```
- 使用homebrew安装MySQL
1. 安装命令
```
brew install mysql
```
2. 启动命令
```
mysql.server start
```
3. 停止命令
```
mysql.server stop
```

