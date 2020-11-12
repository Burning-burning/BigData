### Hadoop 运行环境搭建

#### 1. 虚拟机环境配置

1. 关闭防火墙

   systemctl stop firewalld.service   关闭防火墙

   systemctl disable firewalld.service    关闭开机自启动

   systemctl status firewalld.service   查看防火墙是否已关闭

2. 创建一个一般用户atguigu

   useradd atguigu

   ll /home   查看是否已添加用户

   passwd atguigu

3. 在/opt目录下创建software module文件夹，并更改所有权

   mkdir /opt/software /opt/module

   ll /opt

   chown atguigu:atguigu /opt/software /opt/module

4. 把这个用户加到sudoers

   vim /etc/sudoers

   atguigu   ALL=（ALL）     ALL

   su atguigu

   sudo ls

   exit;

5. 改hosts

   vim /etc/hosts

   192.168.80.5   hadoop100

   192.168.80.6   hadoop101

   192.168.80.7  hadoop102

6. 改静态ip

   vim /etc/sysconfig.network-scripts/ifcfg-ens33

   DEVICE=ens33

   TYPE=Ethernet

   ONBOOT=yes

   BOOTPROTO=static

   IPADDR=192.168.80.5

   PREFIX=24

   GATEWAY=192.168.80.2

   DNS1=8.8.8.8

   DNS2=8.8.8.2

   NAME=ens33

   systemctl restart network

7. 改主机名字

   hostnamectl set-hostname hadoop100

   hostnamectl

   关机并拍快照

8. xxxx

#### 2. 安装JDK,hadoop

1. 拷贝jdk  hadoopjar包

2. 解压

   tar -zxvf jar包名  -C /opt/module

   tar -zxvf haddop  -C /opt/module

   ll

3. 配置环境变量(java  hadoop)

   sudo vim /etc/profile

   #JAVA_HOME
   export JAVA_HOME=/opt/module/jdk1.8.0_271
   export PATH=$PATH:$JAVA_HOME/bin

   保存后执行source /etc/profile

   echo $JAVA_HOME

   java -version

   sudo vi /etc/profile

   #HADOOP_HOME
   export HADOOP_HOME=/opt/module/hadoop-2.7.2
   export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

   

   保存后执行source /etc/profile

   hadoop version

   

4. 官网走一遍

   本地运行模式，单点设置（官方grep案例）

    vi`etc/hadoop/hadoop-env.sh` 

    export JAVA_HOME=/opt/module/jdk1.8.0_271

   保存后执行  bin/hadoop

   在hadoop2.7.2文件下面创建一个input文件夹

   mkdir input

   将hadoop的xml配置文件复制到input

   cp etc/hadoop/*.xml input

   执行share目录下的mapreduce程序

   bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.9.2.jar grep input output 'dfs[a-z.]+'

   查看输出结果

   cat output/*

   

   官方WordCount案例

   创建在hadoop2.7.2文件下面创建一个wcinput文件夹

   在wcinput文件下创建一个wc.input

   变价wc.input文件

   在文件中中输入如下内容

   

   

   保存并退出

   

5. xxx

6. x

7. xxx

8. xxxx

#### 3. 安装Hadoop

 