# ubuntu-sw
usual software installation and problems encountered.
  
  
  
  
### 安装jdk1.6
```
sudo apt-get install openjdk-6-jdk
```  

下载之后如果是bin 文件添加可执行权限直接执行，如果是压缩包 直接解压 ，直接mv 到`/usr/lib/jvm/` 目录下面

### 安装jdk1.7
```
sudo apt-get install openjdk-7-jdk
```
### 安装jdk1.8
```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update 
sudo apt-get install openjdk-8-jdk
```
### 更新默认jdk 默认jdk更新为1.8 
```
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

`注意：千万不要在系统环境中配置JAVA_HOME变量，配置这个变量之后会导致无法各个Android 系统版本无法自动兼容问题`

### Android 编译环境
```
sudo apt-get install git-core gnupg flex bison gperf build-essential	
sudo apt-get install zip curl libc6-dev libncurses5-dev:i386 x11proto-core-dev	
sudo apt-get install libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-dev:i386
sudo apt-get install g++-multilib mingw32 openjdk-6-jdk tofrodos python-markdown	
sudo apt-get install libxml2-utils xsltproc zlib1g-dev:i386 libxext-dev:i386
```

### 安装wine 
```
sudo apt-get install wine
```

### 安装beyond copare 
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

### 安装vim
```  
sudo apt-get install vim
```  

### 安装gparted 分区工具
```  
sudo apt-get install gparted
sudo gparted 
```  
执行该工具 给硬盘分区  

### 查看硬盘分区UUID
```  
sudo blkid 
```  

### 通过sudo vim /etc/fstab 来挂载新分区到指定目录
```  
UUID=0a707d59-eb03-4cdf-905b-0cdc2d9bd103	/home/workspace	ext4	defaults	0	2
UUID=d55abf57-335b-4c96-9f36-3c4bf6e1b919	/home/workspace1	ext4	defaults	0	2
```  

### 展讯版本
* 4.4  需要`sunjdk1.6 : cd /usr/lib/jvm/   	    sudo ln -s jdk1.6.0_38  java-6-sun`  
* 4.4  默认导入java 环境的时候会寻找`/usr/lib/jvm/java-6-sun` 这个路径 ，所以需要做一个链接到jdk1.6.0上	 
* 6.0  需要jdk1.7	： 通过安装openjdk-7-jdk 会自动建立链接 ：`/usr/lib/jvm/java-7-openjdk-amd64`	 
* 7.0  需要jdk1.8	： 通过安装openjdk-8-jdk 会自动建立链接 ：`/usr/lib/jvm/java-8-openjdk-amd64`   
具体版本需求可以查看源码中的：`build/envsetup.sh` 中的`set_java_home`函数  
	
###  阿里版本
具体可查看：`/build/core/find-jdk-tools-jar.sh`	脚本	  
`注意：千万不要像网上所有的在系统环境中配置JAVA_HOME 变量，配置这个变量之后会导致无法各个Android 系统版本无法自动兼容问题`

### windows 虚拟机无法识别usb 问题，添加VID相关，安装展讯驱动
```
sudo adduser xxx vboxusers
reboot
``` 
配置虚拟机-设置  

### ubuntu usb 调试权限配置 以及adb 版本使用，添加VID相关
```  
/etc/udev/rules.d/70-android.rules(本地实际路径：/etc/udev/rules.d/70-persistent-net.rules)
```  

### smb 登录windows 共享文件夹问题
```  
smb://192.168.0.7 ,组为：(XUNRUI)xunrui.com.cn, 用户名为：邮件用户名, 密码为：邮件密码
```  
### sftp 远程登录下载
```  
sftp user@192.168.100.27
```  
### ssh  远程登录
```  
ssh user@192.168.100.27
```  
### ssh sftp git 远程常用主机需要输入密码的问题
1. 在本地执行ssh-keygen 一路enter 下去
2. 执行完上面的命令会在.ssh 目录下面生成`id_rsa  id_rsa.pub` 这两个文件
3. 然后copy `id_rsa.pub` 文件中的全部内容到远程服务器或者远程主机的 根目录下面的`.ssh/authorized_keys` 中，然后再次`ssh sftp git`登录 就不需要密码  

### 安装搜狗输入法
```  
sudo dpkg -i sogoupinyin_2.1.0.0086_amd64.deb
```  
安装报错执行：  
```  
sudo apt-get install -f
sudo dpkg -i sogoupinyin_2.1.0.0086_amd64.deb
```  
ubuntu 下搜狗输入法无法输入中文的问题, 进入.config文件夹，在里面可以看到`SogouPY，SogouPY.users，Sougou-qimpanel`，把这三个删除   

### 安装QQ 解压wine-qqintl-www.linuxidc.com.tar.xz 
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

### 安装虚拟机 
先VirtualBox VMs.tar 用户目录 ，然后解压，再软件中心安装virtualbox ，然后进入VirtualBox VMs.tar 解压目录点击WinXp.vbox,进入winxp虚拟机会提示报错，然后在用户目录新建SharedFloader ，并将VBoxGuestAdditions_4.3.36.iso copy 到用户目录下的.config/VirtualBox 目录中（/home/user/.config/VirtualBox/） 目录中SharedFloader为共享目录，也在vbox中设置为其它目录
然后命令行执行 `sudo adduser xxx vboxusers`，其中xxx指的是当前的用户名 ，否则虚拟机无法访问usb 设备，以及共享文件夹

### 安装source insight  
直接解压SourceInsighten.zip 然后邮件exe文件以wine xxx 打开 既可 ，直接下一步 就可以   

### 安装SSH
```
ssh localhost   提示 ssh: connect to host localhost port 22: Connection refused 则未安装
sudo apt-get install openssh-server
sudo /etc/init.d/ssh start 
ps -e|grep ssh  显示 14669 ?        00:00:00 sshd  则已安装
```
默认端口是22，修改`vi /etc/ssh/sshd_config` 搜索Port  


### 安装Node&NPM
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

### 安装XAMPP
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

### 安装sqlitebrowser
```
sudo add-apt-repository -y ppa:linuxgndu/sqlitebrowser
sudo apt-get update
sudo apt-get install sqlitebrowser
```
