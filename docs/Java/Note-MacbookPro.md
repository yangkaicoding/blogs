#### 前言

- IDEA for Mac常用快捷键
1. Refactoring（重构）
```
Shift+F6 重命名文件
Command+Option+V 提取变量
Command+Option+F 提取字段
Command+Option+M 将选中的代码提取为方法
```
2. Search/Replace (查询/替换)
```
Command+Shift+F	全局查找(根据路径)
Command+Shift+R	全局替换(根据路径)
```
3. Editing (编辑)
```
Command+N 声明代码
```
```
Shift+Enter 开始新的一行
```
```
Control+Option+I 自动缩进线
Command+Option+L 格式化代码
```
```
Control+O 覆盖方法(重写父类方法)
Control+I 实现方法(实现接口中的方法)
```
```
Option+向上箭头 连续选中代码块
Option+向下箭头 减少当前选中的代码块
```
1. Navigation (导航)
```
Control+H 显示当前类的层次结构
Command+F12 显示当前的文件结构层
Command+Option+向左箭头/向右箭头 退回/前进到上一个操作的位置
```
- 查看本机的Ip地址
```
ifconfig | grep "inet " | grep -v 127.0.0.1
```
- homebrew软件包管理工具
1. 安装包
```
brew install [package]
```
2. 卸载包
```
brew uninstall [package]
```
3. 列出过时的软件
```
brew outdated
```
4. 更新过时的软件（全部或指定）
```
brew upgrade
```
5. 升级homebrew
```
brew update
```
6. 列出所有安装的包
```
brew list
```
7. 清理旧版本缓存
```
brew clean up
```
8. 安装包信息检索
```
brew info
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

