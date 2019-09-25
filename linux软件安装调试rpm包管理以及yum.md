*[linux软件安装调试rpm包管理以及yum](#linux软件安装调试rpm包管理以及yum)
##### 一、rpm安装和卸载软件
- 在 Linux 操作系统下，几乎所有的软件均通过 RPM 进行安装、卸载及管理等操作。RPM 的 全称为 Redhat Package Manager ，是由 Redhat 公司提出的，用于管理 Linux 下软件包的软件。 Linux 安装时，除了几个核心模块以外，其余几乎所有的模块均通过 RPM 完成安装。

1.``挂载光盘``
 - 必须把光盘放在光驱中
 - 光驱必须连上电脑
 - mount dev/cdrom/media &emsp;挂载
 - df &emsp;查看光盘是否挂载
 - 查找 ls | grep httpd

2.``安装``
- rpm -ivh httpd-2.4.6-80.el7.centos.x86_64.rpm
- rpm -ivh http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm
- rpm -i 需要安装的包文件名
- rpm -iv 安装过程中显示正在安装的文件信息;
- rpm -ivh 安装过程中显示正在安装的文件信息及安装进度;

3.``卸载软件``
- rpm -e httpd &emsp;&emsp;//httpd表示要卸载的软件包
- rpm -q httpd &emsp;&emsp;//查找httpd

4.``升级包``
- rpm -Uvh 软件

##### 二、yum安装软件

- Yum(全称为 Yellow dog Updater, Modified)是一个在 Fedora 和 RedHat 以及 CentOS 中的 Shell 前端软件包管理器。基于 RPM 包管理，能够从指定的服务器自动下载 RPM 包并且安装，可 以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。

1.``yum安装rpm包(常用软件安装)``
- yum install -y net-tools &emsp;&emsp;//包括 netstat ifconfig 等命令
- yum install -y unzip zip &emsp;&emsp;//zip 压缩减压
- yum install -y mlocate &emsp;&emsp;//updatedb
- yum install -y wget
- yum -y install psmisc &emsp;&emsp;//pstree | grep httpd 查看进程 pstree -p 显示进程以及子进程

2.``yum卸载rpm包``
- yum -y remove wget
3.``yum搜索 rpm包``
- yum search 名称
4.``yum查看rpm包``
- yum list
- yum list | grep httpd
- yum list updates &emsp;&emsp;//列出所有可更新的软件包
- yum list installed &emsp;&emsp;//列出所有已安装的软件包

5.``yum显示rpm包信息``
- yum info package1 &emsp;&emsp;//如:yum info httpd yum info zip yum info unzip

6.``yum远程安装Apache``
- yum -y install httpd
- service httpd start  &emsp;&emsp;//安装启动 apache

7.``yum本地安装apache RPM包``
- yum localinstall httpd-2.4.6-80.el7.centos.x86_64.rpm
8.``yum安装Nginx``

（1）、源安装
- sudo rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

(2)、查看nginx源是否配置成功
- yum search nginx
- yum info nginx
- yum install -y nginx

(3)、启动nginx并设置开机自动运行
- systemctl start nginx.service
- systemctl enable nginx.service
##### 三、yum仓库设置(了解)
