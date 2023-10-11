<!-- TOC -->

- [软件安装方式](#软件安装方式)
- [软件包管理](#软件包管理)
- [更新软件源](#更新软件源)
- [环境变量](#环境变量)
  - [路径](#路径)
  - [查看](#查看)
- [运行程序](#运行程序)
- [软件安装](#软件安装)
  - [安装adb](#安装adb)
  - [安装vim](#安装vim)
  - [安装搜狗输入法](#安装搜狗输入法)
  - [安装QQ 解压wine-qqintl-www.linuxidc.com.tar.xz](#安装qq-解压wine-qqintl-wwwlinuxidccomtarxz)
  - [安装虚拟机](#安装虚拟机)
  - [安装source insight](#安装source-insight)
  - [安装SSH](#安装ssh)
  - [安装Node&NPM](#安装nodenpm)
  - [安装XAMPP](#安装xampp)
  - [安装sqlitebrowser](#安装sqlitebrowser)
  - [安装jdk](#安装jdk)
    - [1.6](#16)
    - [1.7](#17)
    - [1.8](#18)
    - [更新默认jdk](#更新默认jdk)
    - [展讯版本](#展讯版本)
    - [阿里版本](#阿里版本)
  - [安装wine](#安装wine)
  - [安装beyond copare](#安装beyond-copare)
- [创建快捷方式](#创建快捷方式)
- [帮助命令](#帮助命令)
- [VIM相关](#vim相关)
- [Terminal](#terminal)
- [用户和权限](#用户和权限)
  - [创建新用户](#创建新用户)
  - [修改主机名](#修改主机名)
  - [修改用户名](#修改用户名)
- [登录](#登录)
  - [提示普通用户密码错误无法开机](#提示普通用户密码错误无法开机)
  - [windows 虚拟机无法识别usb 问题，添加VID相关，安装展讯驱动](#windows-虚拟机无法识别usb-问题添加vid相关安装展讯驱动)
  - [ubuntu usb 调试权限配置 以及adb 版本使用，添加VID相关](#ubuntu-usb-调试权限配置-以及adb-版本使用添加vid相关)
  - [smb 登录windows 共享文件夹问题](#smb-登录windows-共享文件夹问题)
  - [sftp 远程登录下载](#sftp-远程登录下载)
  - [ssh 远程登录](#ssh-远程登录)
  - [ssh sftp git 远程常用主机需要输入密码的问题](#ssh-sftp-git-远程常用主机需要输入密码的问题)
- [网络](#网络)
  - [状态查看](#状态查看)
  - [故障排查](#故障排查)
  - [服务管理](#服务管理)
- [内核升级](#内核升级)
- [grub配置文件](#grub配置文件)
- [进程管理](#进程管理)
- [作业控制](#作业控制)
- [信号](#信号)
  - [查看](#查看-1)
  - [发送](#发送)
  - [处理](#处理)
- [守护进程](#守护进程)
- [系统日志](#系统日志)
- [服务管理工具systemctl](#服务管理工具systemctl)
- [SeLinux](#selinux)
- [系统状态查看](#系统状态查看)
- [查看内存](#查看内存)
- [文件系统](#文件系统)
- [磁盘](#磁盘)
  - [查看](#查看-2)
  - [安装gparted 分区工具](#安装gparted-分区工具)
  - [查看硬盘分区UUID](#查看硬盘分区uuid)
  - [通过sudo vim /etc/fstab 来挂载新分区到指定目录](#通过sudo-vim-etcfstab-来挂载新分区到指定目录)
  - [分区与挂载](#分区与挂载)
  - [磁盘配额](#磁盘配额)
  - [交换分区swap](#交换分区swap)
  - [RAID](#raid)
  - [逻辑卷管理](#逻辑卷管理)
- [Linux启动过程](#linux启动过程)
- [shell](#shell)
  - [shell脚本的启动方式](#shell脚本的启动方式)
- [重定向](#重定向)
- [变量](#变量)
  - [分类定义](#分类定义)
  - [自定义变量](#自定义变量)
  - [环境变量](#环境变量-1)
  - [basename和dirname](#basename和dirname)
  - [预定义变量](#预定义变量)
  - [位置参数变量](#位置参数变量)
- [read命令](#read命令)
- [数组](#数组)
- [特殊字符](#特殊字符)
- [运算符](#运算符)
- [算术运算](#算术运算)
- [test命令](#test命令)
- [数字常量](#数字常量)
- [括号](#括号)
- [字符串操作](#字符串操作)
    - [读取](#读取)
    - [连接](#连接)
    - [替换](#替换)
    - [截取](#截取)
- [条件](#条件)
- [分支](#分支)
- [循环](#循环)
- [命令行参数](#命令行参数)
- [函数](#函数)
- [周期性任务](#周期性任务)
- [正则表达式中的元字符](#正则表达式中的元字符)
- [扩展元字符](#扩展元字符)
- [tr命令](#tr命令)
- [cut命令](#cut命令)
- [sed命令](#sed命令)
- [awk命令](#awk命令)

<!-- /TOC -->

### 软件安装方式

1. 安装包：

```
install:
CentOS: rpm -i *.rmp
Ubuntu: dpkg -i *.deb

uninstall:
CentOS: rpm -e *.rmp
Ubuntu: dpkg -r *.deb

search: 
CentOS: rpm -qa | grep keyword
Ubuntu: dpkg -I | grep keyword

dpkg -S softwarename: 显示包含此软件包的所有位置
dpkg -L softwarename: 显示安装路径
```

2. 软件管家：

```
install:
CentOS: yum install java-11-openjdk.x86
Ubuntu: apt-get install openjdk-9-jdk

uninstall: 
CentOS: yum erase java-11-openjdk.x86
Ubuntu: apt-get purge openjdk-9-jdk
```

软件源路径：

```
/etc/apt/sources.list
```

3. 下载解压：

```
wget wget http://www.baidu.com
```

将安装好路径的软件包下载后的tar.gz或者zip解压即可，无需安装，但是需要配置环境变量

### 软件包管理
软件包全名=软件名称+软件版本+系统版本+平台架构
```
Redhat、CentOS，使用yum包管理器，软件包格式为rpm，参数含义：q（查询），i（安装，需要全名），e（卸载），yum可以自动解决依赖问题，参数含义：install（安装），remove（卸载），list|grouplist（查看），update（升级），makecache（更新缓存）
Ubuntu、Debian，使用apt包管理器，软件包格式为deb
```

### 更新软件源
```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo_bak
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
yum makecache
```

###  环境变量
#### 路径
1. vim ~/.bashrc // 仅对当前用户有效
2. vim ~/.profile // 仅对当前用户有效
3. vim /etc/profile // 对所有用用有效
4. vim /etc/environment // 对所有用用有效

#### 查看
- 查看单个环境变量: echo $PATH
- 查看所有环境变量: env
- 查看所有本地定义的环境变量: set
- 删除指定的环境变量: unset
- 只对当前shell(BASH)有效: export CLASS_PATH=./JAVA_HOME/lib:$JAVA_HOME/jre/lib,可以通过执行 source ~/.bashrc使当前用户有效或source vim /etc/profile对所有用户有效
- 常用的环境变量
```
PATH        决定了shell将到哪些目录中寻找命令或程序
HOME        当前用户主目录
HISTSIZE　  历史记录数
LOGNAME     当前用户的登录名
HOSTNAME　  主机的名称
SHELL 　　  当前用户Shell类型
```

### 运行程序
1. 命令行运行

```
 ./filename  
 如果在path设置了环境变量，无需./  如果关闭了命令行，则程序关闭
```

2. 后台运行

```
   nohup filename > output.txt 2>&1 &  
   表示在后台运行程序，标准输出和错误输出保存到文件
   要关闭程序，可通过命令 ps -ef |grep filename |awk '{print $2}'|xargs kill -9
```

3. 以服务方式运行

```
   /lib/systemd/system 目录下会创建一个XXX.service 的配置文件，里面定义了如何启动、如何关闭X86体系
```

### Ubuntu20.04 Android环境配置
```
----------------------------------
sudo apt-get install libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-dev g++-multilib
sudo apt-get install -y git flex bison gperf build-essential libncurses5-dev:i386
sudo apt-get install tofrodos python-markdown libxml2-utils xsltproc zlib1g-dev:i386
sudo apt-get install dpkg-dev libsdl1.2-dev
sudo apt-get install git-core gnupg flex bison gperf build-essential
sudo apt-get install zip curl zlib1g-dev gcc-multilib g++-multilib
sudo apt-get install libc6-dev-i386
sudo apt-get install lib32ncurses5-dev x11proto-core-dev libx11-dev
sudo apt-get install libgl1-mesa-dev libxml2-utils xsltproc unzip m4
sudo apt-get install lib32z-dev ccache
sudo apt-get install libssl-dev vim gitk

sudo apt-get install libesd0-dev 如果执行报错就执行下面操作再执行 
sudo vim /etc/apt/sources.list   中添加
    deb http://us.archive.ubuntu.com/ubuntu/ xenial main universe
 deb-src http://us.archive.ubuntu.com/ubuntu/ xenial main universe
     
sudo apt-get update
sudo apt-get install libncurses5
     
sudo add-apt-repository ppa:linuxuprising/libpng12
sudo apt update
sudo apt install libpng12-0 

sudo apt-get -o Dpkg::Options::="--force-overwrite" install openjdk-9-jdk
 
sudo add-apt-repository ppa:openjdk-r/ppa  
sudo apt-get update  
sudo apt-get install openjdk-8-jdk 

sudo apt-get install libswitch-perl  
sudo apt-get install libxml-simple-perl
sudo apt-get install libxml2-dev zlib1g-dev
sudo cpan install XML::LibXML

sudo cpan install Archive::Zip

kaios ---------------------------
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt update
sudo apt install yarn


modify python version ----------------------
cd /usr/bin/
sudo ln -s python2.7  python

sudo apt install python2.7-dev
python2.7 安装签名问题pycrypto-2.6.1.tar.gz
tar -xvf pycrypto-2.6.1.tar.gz
cd pycrypto-2.6.1
sudo python setup.py install

sudo apt-get install tightvncserver xrdp 

samba --------------------------------------
sudo apt-get install samba
sudo vim /etc/samba/smb.conf 
添加以下 用户名 访问路径
[hj]
path=/mnt/w2
public = no
browseable = yes
valid users = hj
writable = yes

[whq]
path=/mnt/w1
public = no
browseable = yes
valid users = whq
writable = yes

sudo touch /etc/samba/smbpasswd
sudo smbpasswd -a userName  添加samba用户名以及配置密码
```

### 软件安装

#### 源码安装

```
// 脚本文件，最终生成Makefile
./configure
// 编译为可执行文件
make
// 将可执行文件放到指定目录并配置环境变量
make install  
```

#### 安装adb
直接用android sdk自带的

```
sudo vim /etc/environment 
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/home/hefeng/Android/Sdk/platform-tools
sudo source /etc/environment 
```

#### 安装vim
```  
sudo apt-get install vim
```

#### 安装搜狗输入法
```  
sudo dpkg -i sogoupinyin_2.1.0.0086_amd64.deb
```
安装报错执行：  
```  
sudo apt-get install -f
sudo dpkg -i sogoupinyin_2.1.0.0086_amd64.deb
```
ubuntu 下搜狗输入法无法输入中文的问题, 进入.config文件夹，在里面可以看到`SogouPY，SogouPY.users，Sougou-qimpanel`，把这三个删除   

#### 安装QQ 解压wine-qqintl-www.linuxidc.com.tar.xz 
```  
sudo dpkg -i fonts-wqy-microhei_0.2.0-beta-2_all.deb
sudo dpkg -i ttf-wqy-microhei_0.2.0-beta-2_all.deb 
sudo dpkg -i wine-qqintl_0.1.3-2_i386.deb
```
报错执行：   
```  
sudo apt-get install -f
sudo dpkg -i wine-qqintl_0.1.3-2_i386.deb
```

#### 安装虚拟机 
先VirtualBox VMs.tar 用户目录 ，然后解压，再软件中心安装virtualbox ，然后进入VirtualBox VMs.tar 解压目录点击WinXp.vbox,进入winxp虚拟机会提示报错，然后在用户目录新建SharedFloader ，并将VBoxGuestAdditions_4.3.36.iso copy 到用户目录下的.config/VirtualBox 目录中（/home/user/.config/VirtualBox/） 目录中SharedFloader为共享目录，也在vbox中设置为其它目录
然后命令行执行 `sudo adduser xxx vboxusers`，其中xxx指的是当前的用户名 ，否则虚拟机无法访问usb 设备，以及共享文件夹

#### 安装source insight  
直接解压SourceInsighten.zip 然后邮件exe文件以wine xxx 打开 既可 ，直接下一步 就可以   

#### 安装SSH
```
ssh localhost   提示 ssh: connect to host localhost port 22: Connection refused 则未安装
sudo apt-get install openssh-server
sudo /etc/init.d/ssh start 
ps -e|grep ssh  显示 14669 ?        00:00:00 sshd  则已安装
```
默认端口是22，修改`vi /etc/ssh/sshd_config` 搜索Port  

#### 安装Node&NPM
1. 用uname -a或lscpu查看CPU架构，选择Linux Binaries (x86/x64)下载
```
2. xz -d node-v8.5.0-linux-x64.tar.xz
3. tar -vxf node-v8.5.0-linux-x64.tar
```
4. 设置软连接（用绝对路径，删除已经存在的软连接 `sudo rm /usr/bin/node  sudo rm /usr/bin/npm`）  
```
sudo ln -s /home/hefeng/software/node/node-v8.5.0-linux-x64/bin/node /usr/bin/node
sudo ln -s /home/hefeng/software/node/node-v8.5.0-linux-x64/bin/npm /usr/bin/npm
```
5. 查看版本号是否正常 `node -v`    v8.5.0  `npm -v`    5.3.0  

#### 安装XAMPP
1. 下载文件https://www.apachefriends.org/download.html
2. `chmod 777  xampp-linux-x64-5.6.31-0-installer.run`
3. 切换到root用户
4. `./xampp-linux-x64-5.6.31-0-installer.run`
5. 在浏览器输入localhost若能打开网址http://localhost/dashboard/ ，则安装成功，xampp默认安装在/opt/lampp下，切目录下的lampp和xampp作用相同
6. 在lampp/htdocs下新建文件hefeng，在其目录下新建appache，php，MySql，并在appache中新建test.json填入数据从http://guolin.tech/api/china 拷贝，phh中新建test.php填入
```
<?php
phpinfo();
?>
```
7. 在浏览器访问http://localhost/hefeng/ 可以看到三个目录，访问http://localhost/hefeng/appache/test.json 能够看到json数据，访问http://localhost/hefeng/php/test.php 能够显示php服务器的配置信息
8. `/opt/lampp/lampp security` 最新版本只能设置FTP密码（xampp控制面板的默认用户名是xampp，phpmyadmin的默认用户名是pma，mysql的默认用户名是root密码为空，ftp的默认用户名是daemon，默认端口21）
9. 退出root，启动：`sudo /opt/lampp/lampp start`  停止：`sudo /opt/lampp/lampp stop`

#### 安装sqlitebrowser
```
sudo add-apt-repository -y ppa:linuxgndu/sqlitebrowser
sudo apt-get update
sudo apt-get install sqlitebrowser
```


#### 安装jdk
##### 1.6
```
sudo apt-get install openjdk-6-jdk
```

下载之后如果是bin 文件添加可执行权限直接执行，如果是压缩包 直接解压 ，直接mv 到`/usr/lib/jvm/` 目录下面

##### 1.7
```
sudo apt-get install openjdk-7-jdk
```
##### 1.8
```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update 
sudo apt-get install openjdk-8-jdk
```
##### 更新默认jdk 
```
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

`注意：千万不要在系统环境中配置JAVA_HOME变量，配置这个变量之后会导致无法各个Android 系统版本无法自动兼容问题`

##### 展讯版本
* 4.4  需要`sunjdk1.6 : cd /usr/lib/jvm/   	    sudo ln -s jdk1.6.0_38  java-6-sun`  
* 4.4  默认导入java 环境的时候会寻找`/usr/lib/jvm/java-6-sun` 这个路径 ，所以需要做一个链接到jdk1.6.0上	 
* 6.0  需要jdk1.7	： 通过安装openjdk-7-jdk 会自动建立链接 ：`/usr/lib/jvm/java-7-openjdk-amd64`	 
* 7.0  需要jdk1.8	： 通过安装openjdk-8-jdk 会自动建立链接 ：`/usr/lib/jvm/java-8-openjdk-amd64`   
具体版本需求可以查看源码中的：`build/envsetup.sh` 中的`set_java_home`函数  
	
##### 阿里版本
具体可查看：`/build/core/find-jdk-tools-jar.sh`	脚本	  
`注意：千万不要像网上所有的在系统环境中配置JAVA_HOME 变量，配置这个变量之后会导致无法各个Android 系统版本无法自动兼容问题`

#### 安装wine 
```
sudo apt-get install wine
```

#### 安装beyond copare 
解压Beyond_linux.zip命令行切换到解压目录，`sudo dpkg -i bcompare-4.0.7.19761_i386.deb `，执行报错会报错再执行   
```
sudo apt-get install -f 
sudo dpkg -i bcompare-4.0.7.19761_i386.deb
```
安装成功之后 
```
sudo cp -rf Crack/BCompare /usr/lib/beyondcompare/  
sudo cp -rf Crack/trial.key /usr/lib/beyondcompare/
```
执行成功之后执行bcompare 命令 Tools->Options->Startup  勾中 include beyond Compare in file manager context menus， Tools->Options->Tweaks 去掉Check every勾

过期之后重置

```
ubuntu: rm ~/.config/bcompare/registry.dat
window: C:\Users\sky\AppData\Roaming\Scooter Software\Beyond Compare
```

#### python

```
更新源：
sudo apt-get update
安装：
sudo apt-get install python3.8

配置：
sudo update-alternatives --config python
优先级：
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.5  7

卸载：
sudo apt-get remove python3.8
包括依赖：
sudo apt-get remove --auto-remove python3.8
包括配置文件：
sudo apt-get purge python3.8
or
sudo apt-get purge --auto-remove python3.8

卸载源码安装：
sudo mv /usr/local/bin/python3.9 .
sudo mv /usr/local/bin/python3.9-config .

sudo unlink /etc/alternatives/python
sudo ln -s /usr/bin/python3.5 /etc/alternatives/python

sudo update-alternatives --remove  python /usr/local/bin/python3.9
```

### 创建快捷方式

```
~/.local/share/applications
或
/usr/share/application
路径下：
~/.local/share/applications/jetbrains-studio.desktop
添加：
[Desktop Entry]
Encoding=UTF-8
Version=1.0
Type=Application
Name=Android Studio 3.0
Icon=/home/hefeng/software/android-studio/bin/studio.png
Exec="/home/hefeng/software/android-studio/bin/studio.sh" %f
Categories=Development;IDE;
StartupNotify=false
StartupWMClass=jetbrains-studio
OnlyShowIn=Unity;
X-UnityGenerated=true
```

### 帮助命令
```
man
查看具体部分
man 1 passwd 
man 5 passwd
查看全部部分
man -a passwd

help:
内部命令（shell自带命令）：help cd 
外部命令：ls --help
type cd
cd is a shell builtin
type ls
ls is hashed (/bin/ls)

info:
比man/help更详细
```

### VIM相关
```
ctrl-e 下移一行
ctrl-f 上翻一页
ctrl-b 下翻一页
ctrl-u 上翻半页
ctrl-d 下翻半页

gg 跳至文首
G 调至文尾

0 跳至行首，不论有无缩进
^ 跳至行首的第一个字符
$ 跳至行尾

w 跳到下一个字首，
W 跳到下一个字首，长跳
e 跳到下一个字尾
E 跳到下一个字尾，长跳
b 跳到上一个字
B 跳到上一个字，长跳

vim 的可视化：
字符文本操作（v）：逐个字符选择文本
行文本操作（V）：逐行选择文本
块文本操作（ctrl+v）：按照块的方式选择文本
```
### Terminal
```
Ctrl+a	光标移动到开始
Ctrl+e	光标移动到最末
Ctrl+k	删除此处至末尾的所有内容
Ctrl+u	删除此处至开始的所有内容
Ctrl+h	删除当前字符前一个字符
Ctrl+w	删除此处到左边的单词
Ctrl+Left	光标移动到上一个单词的词首
Ctrl+Right	光标移动到下一个单词的词尾

Ctrl+l	相当于clear，即清屏
Ctrl+r	查找历史命令

Ctrl+S	暂停屏幕输出
Ctrl+Q	继续屏幕输出
```

### 用户和权限
```
useradd
userdel
chmod
chown
passwd
查看用户信息：id sky

特殊权限
suid：二进制文件执行时设置为文件属主的权限，如passwd，用s表示
sgid：文件共享时用，目录下新创建的文件或目录自动改为目录所属的组，用g表示
sbit：临时文件时用，目录下新创建的文件或目录仅root或自己可以删除，如tmp，用t表示
```
#### 创建新用户
1. 使用useradd时，会添加用户名，并创建和用户名相同的组名，但它并不在/home目录下创建基于用户名的目录，也不提示创建新的密码；如果后面不添加任何参数选项，例如：#sudo useradd test创建出来的用户将是默认“三无”用户：一无Home Directory，二无密码，三无系统Shell
2. 使用adduser时，创建用户的过程更像是一种人机对话，系统会提示你输入各种信息，然后会根据这些信息帮你创建新用户，建议用此命令创建用户

#### 修改主机名
1. ubuntu主机名位于/etc/hostname里，将其修改为自己需要的名称
2. 修改/etc/hosts文件，将其中127.0.1.1对应的主机名更改为新的主机名，与/etc/hostname里的主机名一致

#### 修改用户名
1. `sudo vim /etc/sudoers`
2. `sudo vim /etc/shadow`
3. `mv temp hefeng`
4. `sudo vim /etc/passwd` (修改的地方比较多，但是主目录一定要改`hefeng:x:1000:1000:hefeng:/home/hefeng:/bin/bash`，否则开机会提示密码错误，实则无法加载主目录)
5. 很多之前安装的应用的桌面依赖路径发生变化，可能导致无法启动，需要重新修改启动路径

### 登录
#### 提示普通用户密码错误无法开机
1. 重启Ubuntu，随即长按esc进入grub菜单
2. 在Recovery Menu中，选择`Root Drop to root shell prompt`
3. `cat /etc/shadow` 查看用户名
4. passwd "用户名" 之后再敲两次密码 如果提示`authentication token manipulation error`. 先执行`mount -o rw,remount /` 再修改密码

#### windows 虚拟机无法识别usb 问题，添加VID相关，安装展讯驱动
```
sudo adduser xxx vboxusers
reboot
```
配置虚拟机-设置  

#### ubuntu usb 调试权限配置 以及adb 版本使用，添加VID相关
```  
/etc/udev/rules.d/70-android.rules(本地实际路径：/etc/udev/rules.d/70-persistent-net.rules)
```

#### smb 登录windows 共享文件夹问题
```  
smb://192.168.0.7 ,组为：(XUNRUI)xunrui.com.cn, 用户名为：邮件用户名, 密码为：邮件密码
```

#### sftp 远程登录下载
```  
sftp user@192.168.100.27
```

#### ssh 远程登录
```  
ssh user@192.168.100.27
```
#### ssh sftp git 远程常用主机需要输入密码的问题
1. 在本地执行ssh-keygen 一路enter 下去
2. 执行完上面的命令会在.ssh 目录下面生成`id_rsa  id_rsa.pub` 这两个文件
3. 然后copy `id_rsa.pub` 文件中的全部内容到远程服务器或者远程主机的 根目录下面的`.ssh/authorized_keys` 中，然后再次`ssh sftp git`登录 就不需要密码  

### 网络   
#### 状态查看
1. nettools 
```
ifconfig
eth0表示第一个网卡，也可能叫其他名字：eno0（板载网卡）、ens33（PCI-E网卡）、enp0s3（无法获取物理信息的PCI-E网卡），名称受到/etc/default/grub文件里面两个参数影响：biosdevname和net.ifnames，都设置为0，再执行grub2-mkconfig  -o /boot/grub2/grub.cfg，再reboot即可生效，会将名字设置为eth0
设置ip地址：ifconfig eth0 10.0.2.16 netmask 255.255.255.0

查看网线连接状态：mii-tool eth0
route：查看网关（路由），-n表示不解析主机名
设置默认网关：route del default gw 10.211.50.1  route add default gw 10.211.50.1 
设置其他网关：route add -host 10.0.0.1 gw 10.211.50.2
设置网段网关：route add -net 192.168.0.0 netmask 255.255.255.0 gw  10.211.50.3
netstat
```
2. iproutes
```
ip
ip addr ls 等同于 ifconfig
ip link set dev eth0 up 等同于 ifup eth0
ip addr add 10.0.0.1/24 dev eth0 等同于 ifconfig eth0 10.0.0.1 netmask 255.255.255.0
ip route add 10.0.0.1/24 via 192.168.0.1 等同于 route add -net 10.0.0.1 netmask 255.255.255.0 gw  192.168.0.1 
ss
```

#### 故障排查
```
ping：与目标主机是否连接
traceroute：与目标主机已经连接，但是无法访问网络，追踪路由，如traceroute -w 1 www.baidu.com
mtr：与目标主机已经连接，网络拥堵状态，比traceroute更详细
nslookup：域名解析，如nslookup www.baidu.com 或nslookup 后输入service可查看当前默认DNS服务器
telnet：检查端口，如telnet www.baidu.com 80
tcpdump：tcp相关协议抓包
netstat：查看协议服务，如netstat -ntpl
ss：如ss -ntpl
```

#### 服务管理
1. 管理工具：network和NetworkManager
```
network和NetworkManager不能同时启用

service network status：查看
service network start|stop|restart：启动、停止、重启
chkconfig --list network：查看network启用情况
chkconfig --level 2345 network off：将2、3、4、5级别关闭，如果全部关闭，则表示禁用network，由NetworkManager接管

systemctl list-unit-files NetworkManager.service：查看
systemctl start|stop|restart NetworkManager.service：启动、停止、重启
systemctl enable|disable NetworkManager.service：启用、禁用
```
2. 网络配置文件
```
网卡相关：/etc/sysconfig/network-scripts/ifcfg-eth0，BOOTPROTO默认是dhcp表示动态分配IP，可以改为静态IP，需要将BOOTPROTO配置为none，增加IPADDR、NETMASK、GATEWAY、DNS1|DNS2|DNS3，设置完后可以通过service network restart或者systemctl restart NetworkManager.service生效
主机相关：/etc/hosts
hostname：查看主机名
hostname sky.xr：临时修改主机名
hostnamectl set-hostname sky.xr：永久修改主机名，需要在/etc/hosts添加127.0.0.1 sky.xr，否则开机某些网络服务会超时
```

### 内核升级
```
1. rpm格式内核
查看内核版本：uname -a
升级内核版本：yum install linux-3.10.0
升级已安装软件和补丁：yum update

2. 配置内核
cd /usr/src/kernels/linux-5.10.0
make  menuconfig|allnoconfig|allyesconfig
使用当前内核配置进行配置
cp /boot/config-kernelversion.platform  /usr/src/kernels/linux-5.10.0/.config

3. 编译
查看CPU：lscpu
编译内核：make -j2 all

4. 安装内核
make modules_install
make install
```

### grub配置文件
```
/etc/default/grub：grub默认路径
/etc/grub.d/：grub具体各个部分
/boot/grub2/grub.cfg：grub实际路径
grub2-mkconfig  -o /boot/grub2/grub.cfg：更新grub配置

grep ^menu /etc/grub2/grub.cfg：列出已经安装的内核列表
grub2-editenv list：查看默认引导的内核
grub2-set-default 0：将第一个menuentry指向的内核设置为默认

忘记密码操作步骤
1. mount -o remount, rw /sysroot
2. chroot /sysroot
3. echo 123456 | passwd --stdin root
4. vim /etc/selinux/config
5. exit, reboot
```

### 进程管理
```
ps -ef/aux：打印所有进程
ps -eLf/axms：打印所有线程
ps -eo/axZ：标记进程是否Selinux
ps -U root -u root u：以root用户运行的进程
ps axo stat,euid,ruid,tty,tpgid,sess,pgrp,ppid,pid,pcpu,comm：以用户定义方式显示
ps -eo pid,tid,class,rtprio,ni,pri,psr,pcpu,stat,wchan:14,comm：以用户定义方式显示
ps -T -p pid：pid所属所有线程
top -H -p pid
pstree -p pid
```

### 作业控制
```
nice -n：设置进程nice值
renice -n：设置正在运行进程nice值
jobs：查看所有后台进程
promess &：在后台运行
ctrl+z：正在运行进程按此键将其放入后台且停止
bg idx：将进程放入后台且运行
fg idx：将进程放入前台且运行
```

### 信号
#### 查看
```
kill -l：查看所有信号
trap -l：查看所有信号
info signal：查看信号相关信息
```
#### 发送
```
kill SID PID
1 pid>0：将信号发送给进程ID为pid的进程
2 pid==0：将信号发送给与发送进程属于同一进程组的所有进程，且发送进程具有权限向这些进程发送信号
3 pid<-1：将信号发送给进程组ID等于pid绝对值，且发送进程具有权限向这些进程发送信号
4 pid==-1：将信号发送给发送进程具有权限向它们发送信号的所有进程，除去init和调用进程自身
```
#### 处理
```
trap 'cmd1; cmd2...' signal-list: 收到信号后执行cmd1, cmd2等命令
1 默认动作：trap signal-list
2 忽略信号：trap "" signal-list
3 执行命令：trap "commands" signal-list
4 查看已经注册的信号处理：trap -p

查看当前终端设置与信息：stty -a

处理信号：trap 'echo hello' SIGINT
^Chello
取消注册：trap SIGINT
```

### 守护进程
```
nohup：不响应SIGHUP信号，即终端关闭也可以继续运行(如sleep 60 & 关闭终端，此进程即结束，而nohup sleep 60 & 关闭终端，此进程依然在运行，且输出会保存在当前目录下的nohup.out)
screen：进入到screen环境
ctrl+a d：退出screen环境
screen -ls：查看所有screen会话
screen -r sid：恢复screen会话
```

### 系统日志
```
/var/log下
message：常规日志
dmesg：内核日志
secure：安全日志
cron：周期性服务日志
```

### 服务管理工具systemctl
```
network：/etc/init.d/
/usr/lib/systemd/system：*.service表示服务，runlevel*.target表示级别，其中service里面的netconsole和network可以通过init控制
ckconfig --list：

systemctl get-default：查看当前级别
systemctl set-default：设置当前级别
systemctl start|stop|reload|restart|enable|disable service：控制服务
systemctl status service：查看服务状态
```

### SeLinux
```
MAC：强制访问控制，相对于DAC自主访问控制而言，影响性能，一般关闭
查看状态：getenforce|/usr/sbin/sestatus|ps -Z and ls -Z and id -Z
临时修改：setenforce 0
永久修改：/etc/selinux/config
ps -Z, ls -Z, id -Z可以查看标签
```

### 系统状态查看
```
sar
ifstop
```

### 查看内存
```
top
free
```

### 文件系统
```
vim file：用vim编辑文件保存后会发现文件的inode值会发生变化
cp afile bfile：会创建一个新的文件
mv afile bfile：如果只是改名，inode值不变
ln afile bfile：硬链接，只对应一个inode，与源文件几乎没有区别, 只能通过ls -li看出link关系，删除源文件后，硬链接文件仍然存在保留了源文件的内容，无法跨文件系统
ln -s afile bfile：软连接，对应两个inode，不是同一文件，软连接文件的内容是实际指向文件的地址，可以跨文件系统
getfacl file：查看文件的访问控制权限
setfacl -m u:user1:rw file：为user1设置文件的读写权限
setfacl -x g:group1:r file：为group1收回文件的读权限
```

### 磁盘
#### 查看
```
df -h
fdisk -l
parted -l
ls -al /dev/sd?：sda表示一个磁盘，sda1表示一个分区
du：与ls相比，会去除空洞，表示实际大小
dd if=/dev/zero bs=4m count=10 of=afile：创建40M大小的文件
dd if=/dev/zero bs=4m count=10 seek=20 of=bfile：创建开始80M空洞后面40M大小的文件
```

#### 安装gparted 分区工具
```  
sudo apt-get install gparted
sudo gparted 
```
执行该工具 给硬盘分区  

#### 查看硬盘分区UUID
```  
sudo blkid 
```

#### 通过sudo vim /etc/fstab 来挂载新分区到指定目录
```  
UUID=0a707d59-eb03-4cdf-905b-0cdc2d9bd103	/home/workspace	ext4	defaults	0	2
UUID=d55abf57-335b-4c96-9f36-3c4bf6e1b919	/home/workspace1	ext4	defaults	0	2
```

#### 分区与挂载
```
fdisk /dev/sdc：对磁盘sdc进行分区，比如创建一个一个sdc1，如果磁盘大于2G，需要使用命令parted /dev/sdc进行操作
mkfs.ext4 /dev/sdc1：对分区用ext4文件系统进行格式化
mkdir /mnt/sdc1
mount -o uquota,gquota /dev/sdc1 /mnt/sdc1：把sdc1分区挂载到/mnt/sdc1目录下，-o表示用户和组支持磁盘配额
/dev/sdc1 /mnt/sdc1 ext4 defaults uquota,gquota  0 0：添加到/etc/fstab中，重启生效开机自动挂载
```

#### 磁盘配额
```
xfs_quota -c -x 'report -ugibh' /mnt/disk1：查看disk1的磁盘配额，u表示用户，g表示组，i表示inode，b表示block，h表示按M表示容量
xfs_quota -c -x 'limit -u isoft=5 ihard=10 user1' /mnt/disk1：对user1限制inode的数目，超过5个会有时间限制，但是不能超过10个
xfs_quota -c -x 'limit -u bsoft=5m bhard=10m user1' /mnt/disk1：对user1限制磁盘容量为不超过10M
```

#### 交换分区swap
```
1. 用分区来扩展swap空间
mkswap /dev/sdd1：对sdd1进行swap格式化
swapon /dev/sdd1：将sdd1的swap功能打开
swapoff /dev/sdd1：关闭
2. 用文件来扩展swap空间
dd if=/dev/zero bs=4m count=1024 of=/swapfile：创建一个4G的根目录文件swapfile，权限改为600
mkswap /swapfile：对文件swapfile进行swap格式化
swapon /swapfile：将文件swapfile的swap功能打开
swapoff /swapfile：关闭
/swapfile swap defaults 0 0：写入/etc/fstab永久生效
```

#### RAID
```
四种常见级别：
RAID 0 stripping 条带：至少两块硬盘，每个硬盘存储一半数据，提高单盘吞吐率
RAID 1 mirror 镜像：至少两块硬盘，另一个硬件做备份
RAID 5 奇偶校验：至少三块硬盘，两块放数据，一块放另外两块硬盘数据差异的校验
RAID 10：至少四块硬盘，RAID 0和RAID 1的结合

软件组成RAID阵列：
安装mdadm
mdadm -C /dev/md0 -a yes -l1 -n2 /dev/sd[bc]1：用raid 1的方式，用2个分区/dev/sdb1和/dev/sdc1进行创建raid阵列md0
mdadm -D /dev/md0：查看raid信息
echo DEVICE /dev/sd[b,c]1 >> /etc/mdadm.conf：重启才会自动加载raid
mdadm -Evs >> /etc/mdadm.conf：对raid的配置信息进行加载
mkfs.xfs /dev/md0：对raid用文件系统xfs进行格式化

mdadm --stop /dev/md0：停止raid
dd if=/dev/zero of=/dev/sdb1 bs=1m count=1：无法停止raid可破坏其超级块
```

#### 逻辑卷管理
```
pvs：查看物理卷信息
pvcreate /dev/sd[b,c,d]1：创建一个逻辑卷，包含三个物理磁盘
vgcreate vg1 /dev/sdb1 /dev/sdc1：为sdb1和sdc1建立卷组vg1，一个pv只能属于一个卷组
vgs：查看卷组信息
lvcreate -L 100m -n lv1 vg1：为vg1卷组创建一个名字为lv1大小为100M的逻辑卷
lvs：查看逻辑卷信息

mkdir /mnt/lvroot
mkfs.xfs /dev/vg1/lv1：用xfs格式化逻辑卷lv1
mount /dev/vg1/lv1 /mnt/lvroot：将逻辑卷挂载到指定目录

vgextend vg1 /dev/sdd1：扩充卷组vg1下的分区sdd1
lvextend -L +50G /dev/vg1/lv1：为逻辑卷lv1增加50G空间，不能超过卷组的空间 
xfs_grows /dev/vg1/lv1：通知文件系统已经扩充，此时通过df -h查看才会有变化
```

### Linux启动过程
```
1. bios：主板
2. mbr：dd if=/dev/sda of=/mbr.bin bs=512 count=1：将sda的mbr信息保存到mbr.bin，然后可通过hexdump -C mbr.bin查看
3. grub(bootloader)：grub2-editenv list：查看默认引导的内核
4. kernel：内核驱动硬件
5. systemd：加载/etc/systemd/system服务级别和/usr/lib/systemd/system下的各种服务
6. shell：
```

### shell
```
当前使用的shell：echo $SHELL
当前支持的shell：cat /etc/shells
```

#### shell脚本的启动方式
```
脚本检查：bash -n file.sh

1. bash ./file.sh：会创建子进程（内置命令不会创建子进程，仅对当前shell有效）
2. ./file.sh：会创建子进程，需要有x权限
3. source ./file.sh：不会创建子进程，脚本文件可以读取到shell的变量
4. . ./file.sh：不会创建子进程，脚本文件可以读取到shell的变量
```

### 重定向
```
输入重定向：read var < /tmp/a.txt
输出重定向：echo 123 > /tmp/b.txt，>>表示追加，2>表示仅标准输出，&>表示标准输出和错误输出
输入输出重定向：cat < /tmp/c.txt >> EOF; I am $USER; EOF
```

### 变量
#### 分类定义
```
在bash中，变量的默认类型都是字符串型，如果要进行数值运算，则必须指定变量类型为数值型，变量分为用户自定义变量, 环境变量，位置参数变量和预定义变量。可以通过set命令查看系统中存在的所有变量  

系统变量：保存和系统操作环境相关的数据。$HOME、$PWD、$SHELL、$USER等等
预定义变量：是Bash中已经定义好的变量，变量名不能自定义，变量作用也是固定的
位置参数变量：主要用来向脚本中传递参数或数据，变量名不能自定义，变量作用固定
```

#### 自定义变量
```
1. 变量调用：要在变量名前加上前缀“$”，如echo $A2. 使用let：let a=123+456，性能很差，不建议用
2. 变量赋值
　　a 定义时赋值：变量＝值　等号两侧不能有空格，如 A=9 
　　b 将一个命令的执行结果赋给变量，使用$()或``：如 A=$(ls -al)，如 A=`ls -al` 
　　c 将一个变量赋给另一个变量: 如 A=$STR
3. 变量叠加
　　aa=123
　　cc="$aa"456
　　dd=${aa}789
    变量值中有空格或特殊字符可用""或''，单引号和双引号的区别：
　　NUM=10    
　　SUM="$NUM hehe"     echo $SUM     输出10 hehe
　　SUM2='$NUM hehe'     echo $SUM2    输出$NUM hehe
4. 列出所有变量：set
5. 删除变量：unset  NAME，readonly B=2 声明静态的变量不能 unset
6. 作用域：用户自定义的变量作用域为当前的shell环境，子进程读取父进程的变量：export a
```

#### 环境变量
```
环境变量会在当前shell和其所有子shell中生效。如果把环境变量写入相应的配置文件，那么这个环境变量就会在所有的shell中生效
1. 申明变量：export 变量名=变量值   
2. 作用域：当前shell以及所有的子shell

环境变量的配置文件
su -加减号即继承环境变量的是4个路径都生效（执行顺序依次是：/etc/profile，~/.bash_profile，~/.bashrc，/etc/bashrc），不加减号只有bashrc生效（执行顺序依次是：~/.bashrc，/etc/bashrc），家目录一般放用户特有的，否则放公共的
/etc/profile：系统和终端启动时的信息
/etc/bashrc：
~/.bashrc：
~/.bash_profile：
/etc/profile.d/：不同的shell加载不同的文件

source /etc/bashrc：使得修改后的配置文件生效
```
#### basename和dirname
```
basename：去除目录剩下的名字，若指定后缀，则basename去掉后缀
dirname：目录名字，若指定后缀，则dirname去掉后缀

pwd
/home/workspace1

basename /home/workspace1/test 
test

dirname /home/workspace1/test 
/home/workspace1
```

#### 预定义变量
```
$?：执行上一个命令的返回值   执行成功，返回0，执行失败，返回非0（具体数字由命令决定）
$$：当前进程的进程号（PID），即当前脚本执行时生成的进程号
$!：后台运行的最后一个进程的进程号（PID），最近一个被放入后台执行的进程   &
```

#### 位置参数变量
```
特殊变量
$n：n为数字，$0代表命令本身，即程序名，$1-$9代表第一到第9个参数,十以上的参数需要用大括号包含，如${10}
$*：代表命令行中所有的参数，把所有的参数看成一个整体。以"$1 $2 … $n"的形式输出所有参数
$@：代表命令行中的所有参数，把每个参数区分对待，以"$1" "$2" … "$n" 的形式输出所有参数
$#：代表命令行中所有参数的个数

shift指令：参数左移，每执行一次，参数序列顺次左移一个位置，$# 的值减1，用于分别处理每个参数，移出去的参数不再可用
```

### read命令
```
read -p(提示语句) -n(字符个数) -t(等待时间，单位为秒) –s(隐藏输入)  
如 read –t 30 –p “please input your name: ” NAME
```

### 数组
```
a=(1 2 3)：定义数组
echo ${a[@]}：显示所有元素
echo ${#a[@]}：显示数组个数
echo ${a[0]}：显示第一个元素
```

### 特殊字符
```
#：注释
;：分割命令
\：转义字符
""和''：双引号变量会被其值替换
```

### 运算符
```
=：赋值运算符
+-/ *%：算术运算符

-eq：等于
-ne：不等于
-le：小于等于
-ge：大于等于
-lt：小于
-gt：大于

[]和test是一样的，在命令行里test expr和[ expr ]的效果相同，[[ ]]
是内置在shell中的一个命令，比test强大的多。支持字符串的模式匹配（使用=~操作符时甚至支持shell的正则表达 式）
[[ 3 -gt 2 && 5 -gt 4 ]] 
echo $?     # 0
[[ 3 -gt 2 && 5 -gt 6 ]]
echo $?     # 1
[[ 3 -gt 2 && 5 -gt 4 ]]  # [[]]中，不能使用a或o
echo $?     # 0
[ 3 -gt 2 ] || [ 5 -gt 6 ] # []中，||，必须包含在[]外
echo $?     # 0
[ 3 -gt 2 -a 5 -gt 4 ]  # [] 中，and，必须包含在[]中
echo $?     # 0
[ 3 -gt 2 -o 5 -gt 4 ]  # or
echo $?     # 0

字符串：
[ -z "$var" ]     # 长度为零，为真
[ -n "$var" ]     # 长度非零，为真
[ "$var" = "one two three" ]	# string1 与 string2 相同，为真	
[ "$var" != "one two three" ]   # string1 与 string2 不同，为真	
数字：
[ 3 -eq $mynum ]    # 等于	
[ 3 -ne $mynum ]	# 不等于	
[ 3 -lt $mynum ]	# 小于	
[ 3 -le $mynum ]	# 小于或等于
[ 3 -gt $mynum ]	# 大于	
[ 3 -ge $mynum ]	# 大于或等于	
文件：
[ -e /var/log/syslog ]  # filename 存在，则为真	
[ -d /tmp/mydir ]	    # filename 为目录，则为真	
[ -f /usr/bin/grep ]    # filename 为常规文件，则为真	
[ -L /usr/bin/grep ]    # filename 为符号链接，则为真	
[ -r /var/log/syslog ]  # filename 可读，则为真	
[ -w /var/mytmp.txt ]   # filename 可写，则为真	
[ -L /usr/bin/grep ]    # filename 可执行，则为真	
[ /tmp/install/etc/services -nt /etc/services ] # filename1 比 filename2 新，则为真	
[ /boot/bzImage -ot arch/i386/boot/bzImage ]    # filename1 比 filename2 旧，则为真	

```

### 算术运算
```
expr：只支持整数，运算符要用空格分开如 a=`expr 4 + 5`
expr可嵌套如 a=`expr \`expr 4 + 5\` \* 2`，同echo $(( (4 + 5) * 2 ))

$( )：用途和反引号``一样，用来表示优先执行的命令
${ }：取变量
```

### test命令
```
test expression 同 [ expression ] ，expression首尾都有个空格
测试范围：整数、字符串、文件
返回值：表达式的结果为真，则test的返回值为0，否则为非0

test中比较运算符只有==和!=，都是用于字符串比较，不可用于整数比较，整数比较只能使用-eq, -gt

test -n ""  # n表示是否为非空nonzero
echo $?     # 0
test -n " "  
echo $?     # 1
test -n "1"  
echo $?     # 1
test -z "1" # z表示是否为空zero
echo $?     # 0

```

### 数字常量
```
let var_name=var_value：let定义，可用双圆括号简化，变量值以0开头为8进制，以0x开头为16进制
a=4+5
echo $a
4+5
let a=4+5或((a=4+5))
echo $a
9
```

### 括号
```
1 圆括号(),(()),$()
    a：单独使用会产生一个子shell，如(x=123)，在父shell中echo $x应为空
    b：数组初始化，如x=(1 2 3)
    c：两个是let的简写，可以进行算术运算，如echo $((10+22))
    d：变量定义，如x=$(ls)，echo $x
2 方括号[],[[]]
    a：单独使用做test或数组元素，如[ 5 -gt 4 ]
    b：两个表示测试表达式，如[[ 5 > 4 ]]
3 尖括号<>表示重定向
4 花括号
    a：输出范围如echo {0..9}
    b：文件复制如cp /etc/passwd{,.bak}表示把passwd复制一份为passwd.bak
```

### 字符串操作
##### 读取
```
echo ${a-'hello'} 	# 如果a没有被声明, 就以hello作为其值，等同于echo ${a='hello'} 
hello
a=world
echo ${a-'hello'}   # 如果a被声明了，其值就是设置的值
world

a=''
echo ${a-'hello'}  
                    # 输出为空
echo ${a:-'hello'}  # 如果a没有被声明, 或者其值为空, 就以hello作为其值，等同于echo ${a:='hello'} 
hello

b=wonder
echo $b
wonder
echo ${b+'world'}   # 如果b声明了, 那么其值就是world, 否则就为null字符串
world
echo ${b:+'beauty'} # 如果b被设置了, 那么其值就是beauty, 否则就为null字符串
beauty

echo ${c?'hello'}   # 如果c没被声明, 那么就打印hello
bash: c: hello
echo ${c:?'world'}  # 如果c没被设置, 那么就打印world
bash: c: world

c=''
echo ${c?'hello'}
                    # 如果c没被声明了，就是声明后的值，输出为空
echo ${c:?'world'} 
world
c='hi'
echo ${c:?'world'}  # 如果c被设置了，就是设置后的值
hi
```
```
a=hello
echo ${#a}          # 字符串长度
5

echo ${a:2}         # 从第2个字符取字串
llo

echo ${a:2:2}       # 从第2个字符取长度为2的字串
ll

echo ${a: -4}       # 取后4位，同echo ${a:(-3)}
ello

echo ${a:(-2):2}    # （从0从尾部数）从-2位置开始取长度为2的子串
lo

echo ${a:0-4}       # 0-表示从尾部数，从第4位开始到结束
ello

echo ${a:0-4:2}     # 从尾部开始数，从第4位开始长度为2
el
```

##### 连接
```
a='hello '
b='world!'
echo $a$b
hello world!
echo ${a}${b}       # 最好加上大括号
hello world!
```

##### 替换
```
a='hellohelloworld'
echo ${a/hello/beautiful}    # 替换第一个匹配的字串
beautifulhelloworld
echo ${a//hello/beautiful}   # 替换所有匹配的字串
beautifulbeautifulworld

a='hello, hello, world'
echo ${a/#hello/beautiful}   # 如果以hello开头，则替换为beautiful，否则不处理
beautiful, hello, world
echo ${a/?world/beautiful}   # 如果以world开头，则替换为beautiful，否则不处理
hello, hello,beautiful
```

##### 截取 
```
var=http://www.google.com/test.htm
```
```
1. # 号截取，从左开始，删除匹配到的第一个
echo ${var#*//}
其中 var 是变量名，# 号是运算符，*// 表示从左边开始删除第一个 // 号及左边的所有字符
即删除 http://
结果是 ：www.google.com/test.htm
 
2. ## 号截取，从左开始，删除配到的所有
echo ${var##*/}
##*/ 表示从左边开始删除最后（最右边）一个 / 号及左边的所有字符
即删除 http://www.google.com/         
结果是 test.htm
 
3. %号截取，从右开始，删除匹配到的第一个
echo ${var%/*}
%/* 表示从右边开始，删除第一个 / 号及右边的字符
结果是：http://www.google.com
 
4. %% 号截取，从右开始，删除配到的所有
echo ${var%%/*}
%%/* 表示从右边开始，删除最后（最左边）一个 / 号及右边的字符
结果是：http:
```

### 条件
```
if   [测试条件成立] 或命令返回为0
then 执行相应命令
elif [测试条件成立] 或命令返回为0
then 执行相应命令
else 执行其他命令
fi 结束
```

### 分支
```
case "$变量" in
    "值1")
    命令1
    ;;
    "值2")
    命令2
    ;;
    *)
    命令
esac
```
### 循环
```
for 参数 in 列表
do 执行的命令
done 封闭一个循环

C风格的for循环
for(变量初始化；条件判断；变量变化)
do 
done

while test测试是否成立
do 
done

until循环：条件为假时执行，否则退出

break：结束整个循环
continue：结束本次循环
```

### 命令行参数
```
$0：脚本名称
$1到$n：命令行参数
$*和$@：所有位置参数
$#：位置参数个数
```

### 函数
```
# function可省略
function func()
{
...
    return 0
}
系统自建函数库：/etc/init.d/functions，可通过source /etc/init.d/functions导入到当前shell
```

### 周期性任务
```
1.一次性任务：at 18:30，按ctrl+d退出，没有终端，故而没有标准输出，可保存到文件，按atp查看所有任务
2.周期性任务：crontab -e：配置（分钟 小时 日期 月份 星期 命令），crontab -l：查看，tail -f /val/log/cron：通过日志查看任务有无执行，/var/spool/cron：每个用户同名的文件
3.延迟计划任务：anacrontab，如/etc/cron.d/0hourly，/etc/anacrontab
4.flock 文件：加文件锁，保证任务单例执行，如flock -xn "/tmp/f.lock" -c "/data/a.sh"
```

### 正则表达式中的元字符
```
.：换行符外的任意单个字符
*：匹配任意数目的前面字符，在通配符中它表示任意个任意字符，正则表达式中可用.*表示
[]：匹配其中的任意单个字符
^：行首
$：行尾
\：转义后面的单个字符
```

### 扩展元字符
```
+：匹配前面的正则表达式至少出现一次
?：匹配前面的正则表达式出现零次或一次
|：匹配前面或后面的正则表达式

find /etc -type f -regex .*wd：搜索/etc目录下以wd结尾的普通文件
find *.txt -exec rm -v {} /;：搜索当前目录下的txt文件并删除，{} /;用来指定删除的文件
cut -d ":" -f7 /etc/passward | sort |uniq -c | sort -r -r：以:分割取第七列先排序再统计行数，再反向排序，-n表示按数值排序
```

### tr命令
```
对来自标准输入的字符进行替换、压缩和删除
echo "HELLO WORLD" | tr 'A-Z' 'a-z'：所有字符大写转小写
echo "hello 123 world 456" | tr -d '0-9'：删除所有数字
echo "hello 123 world 456" | tr -d -c '0-9 \n'：仅保留数字
echo "thissss is    a text linnnnnnne." | tr -s ' sn'：连续重复的空格、s、n三个字符压缩为一个显示
cat file | tr -d "\n\t"：删除制表符、换行符
cat file | tr -s "\n" > new_file：删除空行
```

### cut命令
```
cut -c1-3：取每行第1到3个字符，b是字节，
cut -f 1,3 -d" " file：以空格分割，取每行的第1和3个字段
cut -f 1-3 -d" " file：以空格分割，取每行的第1到3个字段
cut -f1 --complement -d" "：以空格分割，取除了第一行之外的行，-d默认分隔符是tab,只能和"-f"选项一起使用
cat file | tr -s ' ' | cut -d ' ' -f1,3 -s：-s表示避免打印不包含分隔符的
```

### sed命令
```
sed 's/old/new/' file：替换一个文本，如果文本有转义字符，可将分割字符替换为!或其他字符如：sed 's!old!new!' file
sed -e 's/old/new/' -e 's/old/new/' file：依次替换文本，替换动作执行两次，也可写为：sed 's/old/new/';'s/old/new/' file
sed -i 's/old/new/' 's/old/new/' file：替换之后的结果直接写入文件，默认不会修改源文件
sed 's/正则表达式/new/' file：支持正则表达式，替换一个文本
sed -r 's/扩展正则表达式/new/' file：支持扩展正则表达式

sed '/s/ab*/!/' file：将文件中以a开头后面有0或多个b的文本替换为!
sed -r '/s/ab+/!/' file：将文件中以a开头后面一个或多个b的文本替换为!
sed -r '/s/ab?/!/' file：将文件中以a开头后面一个或零个b的文本替换为!
sed -r '/s/a|b/!/' file：将文件中存在a或b的文本替换为!
sed -r '/s/(aa)|(bb)/!/' file：将文件中存在aa或bb的文本替换为!
sed -r '/s/(a.*b)/\1:\1/' file：将文件中以a开头以b结尾的文本作为第一组，后面加:，再复制一次匹配的文本

sed 's/old/new/g' file：替换所有文本
sed 's/old/new/2' file：替换第二次匹配文本
sed 's/old/new/p' file：替换一个文本，并将匹配的行打印
sed -n 's/old/new/p' file：替换一个文本，并只将替换的行打印
head -5 /etc/passwd | sed -n 's/old/new/w /tmp/a.txt'：替换一个文本，并只将替换的行写到文件
head -5 /etc/passwd | sed '2,$s/old/new'：对第2到最后一行进行匹配
head -5 /etc/passwd | sed '/^skys,$s/old/new/g'：对以sky开头的行到最后一行进行匹配

sed '/sky/d' file：将匹配到的行删除
sed '/sky/d; s/old/new/' file：先将匹配到的行删除，再进行替换操作

sed '/sky/i hello' file：在匹配到的行前面插入一行hello
sed '/sky/a hello' file：在匹配到的行后面插入一行hello
sed '/sky/c hello' file：匹配到的行用hello进行替换
sed '/sky/r file' file：匹配到的行用文件内容进行替换

sed -n '/sky/p' file：仅将匹配到的行打印

seq 1 10000 > text.txt：生成10000个连续整数写入文件
time sed -n '1,10p' text.txt：统计时间
time sed -n '10q' text.txt：统计时间，只读取前面10行，所以更快

模式空间：数据处理
保持空间：数据暂存
```

### awk命令
```
awk -F":" '/^root/{print $1, $2}' /etc/passwd：匹配以root开头的行，打印以：分割的第1和第2个字段
awk 'BEGIN{FS=":";OFS="-"}{print $1, $2}' /etc/passwd：以：分割，打印第1和第2个字段，两个字段再以-分割，FS为字段分隔符，OFS为输出的字段分隔符
awk 'BEGIN{RS="/"}{print $0}' /etc/passwd：以/作为每行输入结束，默认是/n符，打印整行，RS为记录分隔符
awk '{print NR, $0}' /etc/passwd：对每行输出前添加NR行号，NR和FNR表示行数，如果是多文件，FNR将重新从1开始计数
awk 'BEGIN{FS=":"}{print NF}' /etc/passwd：对每行的字段个数进行输出，NF表示字段数量
awk 'BEGIN{FS=":"}{print $NF}' /etc/passwd：对每行的租后一个字段进行输出，$NF表示获取最后一个字段内容

awk '{if($2>70) {print $1;print $2}}' kpi.txt：如果第二个字段的值大于70，则打印第一和第二个字段
awk '{sum=0;for(c=2;c<=NF;c++) sum+=$c;print sum;print sum/(NF-1)}' kpi.txt：对每行求和和平均
awk '{sum=0;for(c=2;c<=NF;c++) sum+=$c;average[$1]=sum/(NF-1)}END{for(user in average) print user, average[user]}' kpi.txt：打印每行第一个字段和平均

ARGC和ARGV和C里面含义一样

awk 'BEGIN{pi=3.14;print int(pi)}'：取整
awk 'BEGIN{srand();print rand()*10}'：生成小于10的随机数
awk 'function a() { return 1024 } BEGIN{print a()}'：自定义函数
awk 'function b(s) { print "len is: " length(s)} BEGIN{print b("hello world")}'：打印字符串长度
```
