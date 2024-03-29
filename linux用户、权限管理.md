*[linux用户、权限管理](#linux用户、权限管理)

##### 一、用户管理
- Linux 系统同时可以支持多个用户，每个用户对自己的文件设备有特殊的权利，能够保证用户之间互不干扰。就像手机开了助手一样，同时登陆多个qq账号，当硬件配置非常高时，每个用户还可以同时执行多个任务，多个线程同时工作，提高效率。多用户是Linux优于其他操作系统的一大特点。
1.``添加用户``：useradd lisi

2.``设置密码``：passwd lisi

3.``删除用户``：userdel -r lisi
- -r:递归删除目录下面的文件以及子目录下的文件
- 删除用户的时候用户组被删除

4.``查看用户``：id user

5.``把用户加入组``： gpasswd -a testuser root

- 把用户testuser加入到root组，加入组后testuser获取到user组及root组所有权限

6.``移除组``：gpasswd -d testuser root

##### 二、用户权限  用户分类
- 网站发布到linux服务器下面一般要设置权限，不然的话可能没法上传图片，或者没法写入文件。windows中权限没有那么明显。linux里面对权限的管控非常严格。

1.``用户权限``：drwxr-x--- . 2 root root 6 4月 11 2019 mnt

  - d：表示目录
  - rwx：root对mnt目录具有读、写和执行的权限
  - r-x：root组内其他用户对 mnt目录具有读和执行权限
  - ---：other其他所有用户对mnt目录没有任何权限
  - .：表示acl的属性
  - 2：mnt里面的目录数量
  - root(第一个)：当前目录所属用户
  - root(第二个)： 当前目录所属组
  - 6：文件大小(以字节为单位) 这个字段表示文件大小,如果是一个文件夹,则表示该
文件夹的大小.请注意是文件夹本身的大小,而不是文件夹以及它下面的文件的总大小!很多人不能理解文件夹是一个特殊的文件的含义,这样的话理解文件夹大小的含义就比较困难了.
  - 4月：文件创建月份
  - 11 2019 ：文件创建时间
  - mnt：目录名称

2.``权限标志``
- r：读
- w： 写
- x：执行

3.``用户``
- 所有者：user u
- 所属组： group g
- 其他用户：other o
- 所有用户：all a

4.``目录的rwx``

- r： 查看目录里面的文件
- w： 在目录里创建或删除文件
- x： 切换进目录

5.``文件的rwx``

- r：查看文件内容
- w： 在文件里写内容
- x：执行该文件(文件不是普通文件，是程序或脚本)

##### 三、chmod权限分配
1.``增加权限--删除权限``
- chmod u+x my.sh &emsp;&emsp;&emsp;//给当前用户分配执行my.sh的权限
- chmod o+r,o+w file.txt &emsp;&emsp;&emsp;//给其他用户分配对 file.txt 的读写权限
- chmod o+r,o+w,o+x /mnt &emsp;&emsp;&emsp;//给所有其他用户分配对mnt目录的进入、读取、写入权限
- chmod -R o+r,o+w,o+x /mnt &emsp;&emsp;&emsp;//修改目录下的所有文件的权限为可读、可修改、可执行
- chmod 775 file &emsp;&emsp;&emsp;//775 表示-rwxr-xr-x
- chmod -R 777 wwwroot/  &emsp;&emsp;&emsp;//修改目录下的所有文件的权限为可读、可修改、可执行

--  **需求**--

(1)
 - 让其他人对 mnt目录没有任何权限

       chmod o-r,o-w,o-x /mnt

 - 所有人对test.sh文件具有x的权限

        chmod a+x test.sh
 - 让所有用户对test.sh都没有x权限

         chmod a-x test.sh

- 让所有用户对mnt以及mnt里面的所有文件和文件夹都有w权限

        chmod o-r,o-w,o-x /root
        chmod -R a+w /mnt/  //R表示递归

(2)**用户权限管理acl**
- 让zhangsan对opt目录具有rx权限，让 lisi对opt目录具有rwx的权限

  **ps：-m  修改**

      [root@localhost /]# setfacl -m u:zhangsan:rx opt/
      [root@localhost /]# setfacl -m u:lisi:rwx opt/

- 查看opt拥有的 acl权限

      getfacl opt

- 设置opt的acl权限

      setfacl -m u:zhangsan:rwx /opt
- 删除 opt的user1拥有的acl权限

      setfacl -x u:zhangsan /opt  //-x 删除      

- 删除opt上所设置过的所有acl权限

      setfacl -b opt/   

(3)**用户权限管理visudo**           
