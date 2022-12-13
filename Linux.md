# 文件目录

## root

## home

## usr

## etc

# 常用命令

## 文件管理

### 切换目录

```
cd /		根目录
cd ~		上一层
cd ../		父目录
cd 绝对路径	 指定
```

### 查看目录下文件

```
list 
ll
```

# 环境变量配置



# 安装

## Java

1. 下载对应版本的JDK，放在对应的路径，并提取/解压

2. 打开终端（命令行），输入

   ```shell
   su root
   ```

   切换root用户，然后输入

   ```shell
   vim /etc/profile
   ```

   进入全局变量文件，按i进入编辑模式，在文末插入

   ```shell
   export JAVA_HOME=(JDK路径，精确到bin文件上一层，不要加上bin)
   export PATH=$JAVA_HOME/bin:$PATH 
   export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
   ```

   按Esc退出编辑模式，然后输入 :wq! 保存，然后输入

   ```shell
   source /etc/profile
   ```

   使变量生效，或者直接重启，然后输入

   ```shell
   java -version
   ```

   验证是否安装成功

## MySQL

1. 进入MySQL下载页，https://dev.mysql.com/downloads/mysql/

2. 选择自己版本对应的Operating System

3. 下载下列rpm，并放到对应文件夹内

   ```
   RPM Package, MySQL Server
   RPM Package, Client Utilities
   RPM Package, MySQL Configuration
   RPM Package, Shared Libraries
   ```

4. 打开命令行，进入下载的文件夹中

   ```shell
   cd (对应文件夹)
   ```

5. 安装rpm,一定要按顺序

   ```shell
   rpm -ivh common文件名
   rpm -ivh libs文件名
   rpm -ivh client文件名
   ```

   安装第三个的时候可能出错,输入

   ```shell
   ln -s libtinfo.so.5 /usr/lib/libncurses.so.5.9
   dnf install ncurses-compat-libs
   ncurses-compat-libs
   ```

   按顺序输入三条命令即可

6. 安装第四个rpm

   ```shell
   rpm -ivh mysql-community-server-5.7.26-1.el6.x86_64.rpm --force --nodeps
   ```

   检查一下情况

   ```shell
   rpm -qa | grep mysql
   ```

   显示

   ```shell
   mysql-community-libs-5.7.32-1.el7.x86_64
   mysql-community-release-el7-5.noarch
   mysql-community-client-5.7.32-1.el7.x86_64
   mysql-community-common-5.7.32-1.el7.x86_64
   mysql-community-server-5.7.32-1.el7.x86_64
   
   ```

   即安装完成

7. 启动MySQL

   ```shell
   service mysqld start
   ```

   若显示OK,则启动成功,如果显示

   ```shell
   Redirecting to /bin/systemctl start mysqld.service
   ```

   意思是命令已经废弃,使用新的命令Redirecting to后面的命令/bin/systemctl start mysqld.service,这步可能没有启动提示

8. 获取临时密码

   ```shell
   grep 'temporary password' /var/log/mysqld.log
   ```

   ```shell
   2020-12-02T11:39:49.929876Z 1 [Note] A temporary password is generated for root@localhost: w(DjaNdnj2IG
   ```

   保存最后面的字段 w(DjaNdnj2IG  这是临时密码

9. 登录mysql

   ```shell
   sudo mysql -u root -p 
   ```

   输入刚才保存的字段(此时的密码不可见,输就对了)注意大小写

   然后就看见

   ```shell
   mysql>
   ```

   登陆成功

10. 修改密码配置

    ```sql
     set global validate_password_policy=0;
    ```

    设置密码强度检测限制,0/LOW、1/MEDIUM、2/STRONG。

    ```sql
    set global validate_password_mixed_case_count=0;
    ```

    设置密码至少要包含的小写字母个数和大写字母个数。

    ```sql
    set global validate_password_number_count=0;
    ```

    命令设置至少要包含的数字个数。

    ```sql
    set global validate_password_special_char_count=0; 
    ```

    设置至少包含的特殊字符数。

    ```sql
    set global validate_password_length=0;
    ```

     设置密码最小长度。

11. 设置新密码

    ```shell
    alter user 'root'@'localhost' identified by 'swdz1234';
    ```

    后面的swdz1234是密码,根据自己的需要更改

12. 允许远程访问,可视化软件可建立链接

    ```sql
    grant all privileges on *.* to 'root'@'%' identified by 'swdz1234'; 
    ```

    完成授权

    ```sql
    flush privileges;
    ```

13. 设置开机启动  (使用quit退出mysql)

    ```shell
    vi /etc/rc.local
    ```

    打开文件

    ```shell
    mkdir -p /var/run/mysqld
    chown mysql.mysql /var/run/mysqld/
    ```

    输入上面的代码,退出保存(Java文中说过编辑保存)

    ```
    chmod 774 /etc/rc.d/rc.local
    ```

    设置权限

14. 用navicat链接数据库
    输入

    ```shell
    ifconfig -a
    ```

    查看ip

    ```shell
    ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.213.128  netmask 255.255.255.0  broadcast 192.168.213.255
            inet6 fe80::b1ee:a5f9:4ce5:8cde  prefixlen 64  scopeid 0x20<link>
            ether 00:0c:29:a3:bb:8b  txqueuelen 1000  (Ethernet)
            RX packets 448232  bytes 604501600 (576.4 MiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 76622  bytes 16040462 (15.2 MiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    
    lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            inet6 ::1  prefixlen 128  scopeid 0x10<host>
            loop  txqueuelen 1000  (Local Loopback)
            RX packets 48  bytes 4080 (3.9 KiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 48  bytes 4080 (3.9 KiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    
    virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
            inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
            ether 52:54:00:c2:91:d2  txqueuelen 1000  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    
    virbr0-nic: flags=4098<BROADCAST,MULTICAST>  mtu 1500
            ether 52:54:00:c2:91:d2  txqueuelen 1000  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    ```

    第二行的inet后面就是主机ip 192.168.213.128

15. 

16. 

17. 

18. 

19. 

1. 

   ```
   
   ```

   





## redis

