# Pre

## Linux网络环境搭建

`找到/etc/sysconfig/network-script/ifcfg-ens33`文件修改网卡配置

```shell
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
DEVICE=ens33
ONBOOT=yes
IPADDR=192.168.130.151
GATEWAY=192.168.130.2
NETMARK=255.255.255.0
```



##　安装JDK

将JDK压缩包上传到`/opt/`目录

`tar -zxvf`命令解压tar.gz压缩包

`/etc/profile`文件的最后添加系统环境变量，   `~/.bashrc`文件可以配置用户环境变量

```shell
JAVA_HOME=/opt/java
PATH=$JAVA_HOME/bin:$PATH
export JAVA_HOME PATH
```

让配置生效

```java
source /etc/profile
```



## 安装Perl

```shell
yum install -y build=essential

yum install -y gcc

wget http://www.cpan.org/src/5.0/perl-5.16.1.tar.gz

tar -xzf perl-5.16.1.tar.gz

cd perl-5.16.1

./Configure -des -Dprefix=/usr/local/perl

make && make test && make install

perl -v
```



## Linux集群间的免密通信

`ssh-keygen -t rsa` 命令生成公钥和密钥

```shell
cd /root/.ssh

cp id_rsa.pub  authorized_keys
```

使用`ssh-copy-id -i hostname`命令将本机的公钥拷贝到指定机器的authorized_keys文件中



## Redis安装

```shell
# 先安装tcl
$ tar -zxvf tcl-xxx
$ cd tcl-xx
$ cd unix
$ ./configration
$ make && make install

# 再安装redis
$ wget http://download.redis.io/releases/redis-5.0.5.tar.gz
$ tar xzf redis-5.0.5.tar.gz
$ cd redis-5.0.5

让redis安装到指定目录

#$ vim  /opt/redis-4.0.2/src/MakeFiel         进入vim编辑器

#$ PREFIX?=/usr/local/redis                   修改的内容


$ make && make test && make install

```



###　生产环境部署配置

```shell
1 将utils/redis_init_script拷贝到 /etc/init.d目录中

2 将/etc/redis_init_script 重命名为redis_6379

3 修改redis_6379文件中14行REDISPORT，redis的监听端口


  mkdir /etc/redis               # 创建redis配置目录
  mkdir -p /var/redis/6379       # 创建redis工作目录
  
5 将解压后的redis-5.5.5/redis.conf文件复制到/etc/redis目录下

6  mv /etc/redis/redis.conf  /etc/reids/6379.conf 修改配置文件的名字
   vim /etc/redis/6379.conf 修改redis.conf的默认配置

    daemonize = yes                     让redis以daemon进行运行
    pidfile   /var/run/redis_6379.pid   设置redis的pid文件位置
    port 6379                           设置redis的监听端口号
    dir  /var/redis/6379                设置持久化文件的存储位置

8 让redis跟随系统启动自动启动 
   chmod 755 redis_6379
   chkconfig  --add redis_6379 on
   chkconfig  redis_6379 on
    
   
7 启动redis， 执行/etc/init.d/redis_6379脚本

9 使用redis-cli

     redis-cli -h 127.0.0.1 -p 6379 交互式命令行启动
     ping 测试
     quit 退出     
```



