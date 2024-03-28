#### 前言
在学习Linux系统过程中，除了掌握一些必要的操作命令，也必须要学会如何在Linux系统上安装和卸载软件。  
Linux系统为我们提供了多样的软件安装方式，大体上可以分为：源代码安装、软件包管理安装、二进制安装等三种安装方式。

#### 正文
- 源代码安装

无

- 软件包管理安装
  
目前在Linux系统中两种最常见的软件包管理安装方式，分别是rpm和Debian的dpkg，Centos主要是以rpm为主。

rpm是Linux的一种软件包名称，一般以.rpm结尾，安装时候的语法为：rpm -ivh。  
rpm方式安装软件,只能安装下载到本地机器上的rpm包，且安装的过程中，rpm包依赖性太强，安装包的安装位置是由软件包的开发者决定的，安装后的位置会非常凌乱。  
为了彻底解决rpm安装方式文件之间关联性太大的问题，Linux系统还提供了yum安装方式，其优点为将所有软件包都放到官方服务器上，当进行yum在线安装时，可以自动解决依赖性问题。

#### 常用yum命令
- 查询

```
yum list 列出yum服务器上面提供的所有软件名称

yum search “keyword” 搜索服务器上所有和关键字相关的包
```
- 安装

```
yum install "packageName" 安装

yum -y install "packageName" -y 表示安装过程自动回答 yes
```
- 升级和卸载

```
yum -y update "packageName" 升级

yum -y remove "packageName" 卸载
```
- 其他命令

```
yum info "packageName" 查看该软件的功能

yum install updates 列出目前服务器上可供本机进行升级的软件

yum repolist all 列出目前yum server所使用的软件库

yum clean all 删除已下载过的所有软件库的相关数据
```
- 二进制格式安装

类似于Windows下的exe文件，后缀一般为bin，二进制格式文件就是编译好的文件，安装就是先给它可执行权限，然后执行即可完成安装。一般而言，通过二进制格式进行软件安装的步骤如下：
```
1：chomd +x soft.bin
2:./soft.bin
```
- 软件安装路径

在Windows下安装软件时，通常软件都默认安装在C盘目录下，但这样即管理不方便，也会影响系统的性能，因此通常不建议将软件安装到C盘目录中。

- 总结：  
源码包安装的服务是不能使用【service】命令来启动服务，因为源码包的安装位置可以由用户指定，放在哪儿并不统一；  
但rpm包安装后，通常是放在【/etc/rc.d/init.d】 目录中的，而【service】命令执行时，会自动搜索该目录，所以rpm包安装的服务可以使用【service】命令来启动服务。

