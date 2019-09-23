*[linux常用命令](#linux常用命令)


##### 基本命令

1.``切换目录``：cd

2.``查看当前目录下面的文件``：ls

3.``查看ip地址``：ip addr

4.``编辑文件开启网络``： vi /etc/sysconfig/network-scripts/ifcfg-ens33

5.``重启网络``：service network restart

6.``关机``：init 0

7.``重启``：init 6

8.``列出当前目录下的文件``：ls 、ls -l 、 ll

9.``查看当前路径``：pwd

10.``切换最近使用过的两个目录``：cd -

11.``中断当前程序``：ctrl+c

12.``清屏``：ctrl+l /(clear)

13.``检查网络是否通畅``：ping 127.0.0.1

##### 文件管理

1.``创建文件``：touch file1

2.``删除一个文件``：rm -rf file1    
  - -r:递归删除目录下面的文件以及子目录下面的文件。
  - -f: 强制删除，忽略不存在的文件，从不给出提示。

3.``修改文件名``：mv file1 file2

4.``查看文件内容``：cat file1

5.``复制文件``：cp file2 file22

6.``移动文件``：mv file1 file11

7.``编辑文件``：vi file1

8.``批量创建文件``：touch file{1..10}

9.``批量删除文件``：rm -rf file{1..10}

10.``查看文件前3行``：cat file1 | head -3
  - |：把前面的执行结构给后端

11.``查看文件后三行``：cat file1 | tail -3

##### linux服务器上面查找文件
 1.``find``：find /-name httpd.conf
  - find 目录 -name 文件名

2.``updatedb``：查找速度快
 - 建立一个小型数据库： updatedb
 - 在数据库里面搜索：locate httpd.conf
 - yum install mlocate -y

  mlocate是新型的locate比updatedb速度更快。

3.``查找文件里面的内容``：
  - vi搜索 vi httpd.conf
  - 输入 /listen 搜索listen  N下一个

##### linux目录操作

1.``创建目录``：mkdir dir1 dir2 dir3

2.``删除目录``：rm -rf dir1 dir2 dir3
  - r：递归删除目录下面的文件以及子目录的文件

  -f：强制删除，忽略不存在的文件，从不给出提示
  - rm -rf dir*  删除以dir开头的所有文件

3.``重命名目录或移动目录``：mv dir1 dir11

4.``查看目录``：ls

5.``递归创建目录``：mkdir -p a/b/c/d/e/f/g

6.``递归查看目录``：tree a

7.``复制目录``：cp -rf wwwroot/mywwwroot/

8.``tree命令不存在的话需要安装``：yum install tree -y


##### linux打包压缩命令
- 目前linux中打包和压缩的命令很多，最常用的方法有zip、gzip、bzip2、xz、tar

1.``zip压缩包``：
  -  制作：zip -r public.zip public  (ps：-r 递归 表示将指定目录下的所有子目录以及文件一起处理)
  - 解压：unzip publish.zip (unzip publish.zip -d dir)
  - 查看：unzip -l publish.zip

  -安装zip解压软件： yum install -y unzip zip

2.``gz压缩包（源代码压缩）`` ：
  - Linux 下最常用的打包程序就是 tar 了，使用 tar 程序打出来的包我们常称为 tar 包，tar
包文件的命令通常都是以.tar 结尾的。生成 tar 包后，就可以用其它的程序来进行压缩了， 所以首先就来讲讲 tar 命令的基本用法

  (1)``制作gz包``：tar czvf publish.tar.gz publish

  (2)``解压gz包``：tar xzvf public.tar.gz

  (3)``查看gz包``：tar tf public.tar.gz

  (4)``制作tar包``：tar cvf wwwroot.tar wwwroot
  
  (5)``解压tar包`` ：tar xvf wwwroot.tar

#### 参数
  · 特别注意，在参数的下达中，c/x/t仅能存在一个！不可同时存在，因为不可能同时压缩与解压缩。

  -c：建立一个压缩档案的参数指令(create的意思)

  -x： 解开一个压缩档案的参数指令！

  -t：查看tarfile里面的档案！

  -z： 是否同时具有 gzip的属性？亦即是否需要用gzip压缩。

  -j：是否同时具有 bzip2的属性？亦即是否需要用bzip2压缩。

  -v：压缩的过程中显示档案！ 这个常用，但不建议用在背景执行过程。

  -f：使用档名，请留意，在f之后要立即接档名，不要再加参数。


3.``xz压缩包``
 - 对于xz这个压缩相信很多人陌生，但xz是绝大数linux默认就带的一个压缩工具，xz格式比7z还小。

    (1)``制作``：tar cvf xxx.tar xxx  //创建xxx.tar文件

    (2)``压缩1``： xz xxx.tar //将xxx.tar压缩成xxx.tar.xz 并删除原来的tar包

    (3)``压缩2``：xz -k xxx.tar //将 xxx.tar压缩成为xxx.tar.xz 并保留原来的tar包

    (4)``查看``：xz -l ***.tar.xz //先解压xz
