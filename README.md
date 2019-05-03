# 
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

###  环境变量路径

1. vim ~/.bashrc // 仅对当前用户有效
2. vim ~/.profile // 仅对当前用户有效
3. vim /etc/profile // 对所有用用有效
4. vim /etc/environment // 对所有用用有效

### 查看环境变量

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

#### X86体系

CPU结构基于英特尔的 8086，因此称为 x86 架构

```
型号	总线位宽	地址位		寻址空间
8080	8		16			64K(2^16)
8086	16		20			1M
8088	8		20			1M
80386	32		32			4G
```

CPU与内存传数据，主要有两类数据，地址数据和真正的数据

地址总线：位数决定了能访问的地址范围

数据总线：位数决定了一次能保存多少位数据

### 16位寄存器

8个16位通用寄存器：AX、BX、CX、DX、SP、BP、SI、DI

AX、BX、CX、DX可以分为AH、AL、BH、BL、CH、CL、DH、DL

IP：指令指针寄存器（Instruction Pointer Register)，指向代码段中下一条指令的位置

为了切换进程，有四个16位段寄存器：

CS：代码段寄存器（Code Segment Register），通过它可以找到代码在内存中的位置

DS：数据段的寄存器（Data Register），通过它可以找到数据在内存中的位置

SS：栈寄存器（Stack Register），凡是与函数调用相关的操作，都与栈紧密相关

ES：附加段寄存器（Extra Register）

如果运算中需要加载内存中的数据，需要通过 DS 找到内存中的数据，起始地址+偏移量，加载到通用寄存器中

在 CS 和 DS 中都存放着一个段的起始地址。代码段的偏移量会放在通用寄存器中

起始地址CS和DS，偏移量IP和通用寄存器，都是16位，而地址总线是20位，需要把CS和DS左移4位，变成20位，加上16位的偏移量。8086CPU，最多只能访问 1M 的内存空间，还要分成多个段，每个段最多 64K

### 32位寄存器

8个16位通用寄存器，以及IP，依旧放在低16位，可以兼容32位，改动比较大的是段寄存器

CS、SS、DS、ES 仍然是 16 位的，但是不再是段的起始地址。段的起始地址放在内存的某个地方。这个地方是一个表格，里面是真正的段的起始地址。而段寄存器里面保存的是在这个表格中的哪一项，称为选择子（Selector）。将一个从段寄存器直接拿到的段起始地址，就变成了先间接地从段寄存器找到表格中的一项，再从表格中的一项中拿到段起始地址。

32 位的系统架构下，我们将前一种模式称为实模式（Real Pattern），后一种模式称为保护模式（Protected Pattern）。当系统刚刚启动的时候，CPU 是处于实模式的，这个时候和原来的模式是兼容的。也就是说，哪怕你买了 32 位的 CPU，也支持在原来的模式下运行，只不过快了一点而已

### BIOS

ROM会固化一些初始化的程序，如BIOS。实模式只有 1MB 内存寻址空间。加电, 重置 CS 为 0xFFFF , IP 为 0x0000, 第一条指令指向0xFFFF0，BIOS 做以下三件事:

- 检查硬件

- 提供基本输入(中断)输出(显存映射)服务

- 加载 MBR 到内存(0x7c00)

  

BIOS的界面会有一个启动盘，一般在第一个扇区，占512个字节，以0xAA55结束，启动盘是Grub2放置在这的

Grub2：Grand Unified Bootloaer Version 2：

```
grub2-mkconfig -o /boot/grub2/grub.cfg
```

MBR：启动盘第一个扇区(512字节, 由 Grub2 写入 boot.img 镜像)，BIOS 完成任务后，会将 boot.img 从硬盘加载到内存中的 0x7c00 来运行

### Bootloader

boot.img 加载 Grub2 的 core.img 镜像；core.img 包括 diskroot.img(diskboot.S)、 lzma_decompress.img(startup_raw.S)、kernel.img(startup.S) 以及其他模块；boot.img 先加载运行 diskroot.img, 再由 diskroot.img 加载 core.img 的其他内容；diskroot.img 解压运行 lzma_decompress.img、kernel.img(grub 的内核)，最后是各个模块对应的映像， 由lzma_decompress.img 切换到保护模式

------

- lzma_decompress.img切换到保护模式需要做以下三件事:
  - 启用分段, 辅助进程管理
  - 启动分页, 辅助内存管理
  - 打开其他地址线
- lzma_decompress.img解压运行kernel.img 做以下四件事:
  - 解析 grub.conf 文件
  - 选择操作系统
  - 例如选择 linux16, 会先读取内核头部数据进行检查, 检查通过后加载完整系统内核
  - 启动系统内核 grub_command_execute (“boot”, 0, 0)

### 内核初始化

`start_kernel()` 函数(位于 init/main.c), 初始化做三件事

- 创建样板进程, 及各个模块初始化
- 创建管理/创建用户态进程的进程
- 创建管理/创建内核态进程的进程

### 0号进程

样板进程, 即第一个进程. `set_task_stack_end_magic(&init_task)`，定义是 `struct task_struct init_task = INIT_TASK(init_task)`，这是唯一一个没有通过fork 或者 kernel_thread 产生的进程，是进程列表的第一个

各个其他模块初始化包括：

- 初始化中断, `trap_init()`. 系统调用也是通过发送中断进行, 由 `set_system_intr_gate()` 完成.
- 初始化内存管理模块, `mm_init()`
- 初始化进程调度模块, `sched_init()`
- 初始化基于内存的文件系统 rootfs, `vfs_caches_init()`
    - VFS(虚拟文件系统)将各种文件系统抽象成统一接口
- 调用 `rest_init()` 完成其他初始化工作

### 1号进程

创建管理/创建用户态进程的进程，是所有内核态进程的祖先，这是第一个用户态进程

* ` rest_init()` 通过 `kernel_thread(kernel_init, NULL, CLONE_FS)` 创建1号进程(工作在用户态)

- 权限管理
    - x86 提供 4个 Ring 分层权限，Ring0：内核，Ring1：设备驱动，Ring2：设备驱动，Ring3：应用
    - 操作系统利用: Ring0-内核态(访问核心资源); Ring3-用户态(普通程序)
- 用户态调用系统调用: 用户态-系统调用-保存寄存器-内核态执行系统调用-恢复寄存器-返回用户态
- 新进程执行 kernel_init 函数, 先运行 ramdisk 的 /init 程序(位于内存中)
    - 首先加载 ELF 文件（Executable and Linkable Format，可执行与可链接格式）
    - 极客时间版权所有: https://time.geekbang.org/column/article/90109
    - 设置用于保存用户态寄存器的结构体
    - 返回进入用户态
    - /init 加载存储设备的驱动，这时就切到用户态开始运行了
 - kernel_init 函数启动存储设备文件系统上的 init

ramdisk：基于内存的文件系统。内存访问不需要驱动。这个时候，ramdisk 是根文件系统。开始运行 ramdisk 上的 /init。等它运行完了就已经在用户态了。/init 这个程序会先根据存储系统的类型加载驱动，有了驱动就可以设置真正的根文件系统了。有了真正的根文件系统，ramdisk 上的 /init 会启动文件系统上的 init。接下来就是各种系统的初始化。启动系统的服务，启动控制台，用户就可以登录进来了。rest_init 的第一大事情才完成。仅仅形成了用户态所有进程的祖先。rest_init 第二大事情就是第三个进程，就是 2 号进程

###  2号进程

创建管理/创建内核态进程的进程，是所有内核态进程的祖先

- `rest_init()` 通过 `kernel_thread(kthreadd, NULL, CLONE_FS | CLONE_FILES)` 创建 2号进程(工作在内核态)

- `kthreadd` 负责所有内核态线程的调度和管理

  

### glibc 

将系统调用封装成更友好的接口，用户进程调用 open 函数的流程：

- glibc 的 syscal.list 列出 glibc 函数对应的系统调用

  ```
  # File name Caller  Syscall name    Args    	Strong name 	Weak names
  open		-		open			Ci:siv	__libc_open __open 	open
  ```

- glibc 的脚本 make_syscall.sh 根据 syscal.list 生成对应的宏定义(函数映射到系统调用)

  ```
  #define SYSCALL_NAME open
  ```

- glibc 的 syscal-template.S 使用这些宏, 定义了系统调用的调用方式(也是通过宏)

  ```
  T_PSEUDO (SYSCALL_SYMBOL, SYSCALL_NAME, SYSCALL_NARGS)
      ret
  T_PSEUDO_END (SYSCALL_SYMBOL)
  
  #define T_PSEUDO(SYMBOL, NAME, N)		PSEUDO (SYMBOL, NAME, N)
  ```

- 其中会调用 DO_CALL (也是一个宏), 32位与 64位实现不同

  

32位 DO_CALL (位于 i386 目录下 sysdep.h)：

- 将调用参数放入寄存器中, 由系统调用名得到系统调用号, 放入 eax

- 执行 ENTER_KERNEL(一个宏), 对应 int $0x80 触发软中断, 进入内核

- 调用软中断处理函数 entry_INT80_32(内核启动时, 由 trap_init() 配置)

  ```
  set_system_intr_gate(IA32_SYSCALL_VECTOR, entry_INT80_32);
  ```

- entry_INT80_32 将用户态寄存器存入 pt_regs 中(保存现场以及系统调用参数), 调用 do_syscall_32_iraq_on 

- do_syscall_32_iraq_on 从 pt_regs 中取系统调用号(eax), 从系统调用表得到对应实现函数, 取 pt_regs 中存储的参数, 调用系统调用

- entry_INT80_32 调用 INTERRUPT_RUTURN(一个宏)对应 iret 指令, 系统调用结果存在 pt_regs 的 eax 位置, 根据 pt_regs 恢复用户态进程

  ```
  #define INTERRUPT_RETURN                iret
  ```

  

64位 DO_CALL (位于 x86_64 目录下 sysdep.h)：

- 通过系统调用名得到系统调用号, 存入 rax; 不同于中断, 执行的是 syscall 指令，而且传递参数的寄存器也变了

- syscall 使用了MSR(特殊模块寄存器), 辅助完成某些功能(包括系统调用)

- trap_init() 会调用 cpu_init->syscall_init 设置该寄存器

  ```
  wrmsrl(MSR_LSTAR, (unsigned long)entry_SYSCALL_64);
  ```

- syscall 从 MSR 寄存器中拿出函数地址进行调用, 即调用 entry_SYSCALL_64

- entry_SYSCALL_64 先保存用户态寄存器到 pt_regs 中

- 调用 entry_SYSCALL64_slow_pat->do_syscall_64

- do_syscall_64 从 rax 取系统调用号, 从系统调用表得到对应实现函数, 取 pt_regs 中存储的参数, 调用系统调用

- 返回执行 USERGS_SYSRET64(一个宏), 对应执行 swapgs 和 sysretq 指令; 系统调用结果存在 pt_regs 的 ax 位置, 根据 pt_regs 恢复用户态进程

  ```
  #define USERGS_SYSRET64				\
  	swapgs;					\
  	sysretq;
  ```



无论是 32 位，还是 64 位，都会回到系统调用表 sys_call_table：

- 32位 定义在 arch/x86/entry/syscalls/syscall_32.tbl 

    ```
    5	i386	open			sys_open  compat_sys_open
    ```

- 64位 定义在 arch/x86/entry/syscalls/syscall_64.tbl

    ```
    2	common	open			sys_open
    ```

- syscall_*.tbl 内容包括: 系统调用号, 系统调用名, 内核实现函数名(以 sys 开头)

- 内核实现函数的声明: include/linux/syscall.h

- 内核实现函数的实现: 某个 .c 文件, 例如 sys_open 的实现在 fs/open.c

    - .c 文件中, 以宏的方式替代函数名, 用多层宏构建函数头

- 编译过程中, 通过 syscall_32.tbl和syscall_64.tbl  生成 unistd_32.h 和 unistd_64.h文件

    - unistd_32.h 和 unistd_64.h包含系统调用与实现函数的对应关系

- syscall_*.h include 了 unistd_*.h 头文件, 并定义了系统调用表(数组)



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

### 创建新用户

1. 使用useradd时，会添加用户名，并创建和用户名相同的组名，但它并不在/home目录下创建基于用户名的目录，也不提示创建新的密码；如果后面不添加任何参数选项，例如：#sudo useradd test创建出来的用户将是默认“三无”用户：一无Home Directory，二无密码，三无系统Shell
2. 使用adduser时，创建用户的过程更像是一种人机对话，系统会提示你输入各种信息，然后会根据这些信息帮你创建新用户，建议用此命令创建用户

### 修改主机名

1. ubuntu主机名位于/etc/hostname里，将其修改为自己需要的名称
2. 修改/etc/hosts文件，将其中127.0.1.1对应的主机名更改为新的主机名，与/etc/hostname里的主机名一致

### 修改用户名

1. `sudo vim /etc/sudoers`
2. `sudo vim /etc/shadow`
3. `mv temp hefeng`
4. `sudo vim /etc/passwd` (修改的地方比较多，但是主目录一定要改`hefeng:x:1000:1000:hefeng:/home/hefeng:/bin/bash`，否则开机会提示密码错误，实则无法加载主目录)
5. 很多之前安装的应用的桌面依赖路径发生变化，可能导致无法启动，需要重新修改启动路径

### 提示普通用户密码错误无法开机

1. 重启Ubuntu，随即长按esc进入grub菜单
2. 在Recovery Menu中，选择`Root Drop to root shell prompt`
3. `cat /etc/shadow` 查看用户名
4. passwd "用户名" 之后再敲两次密码 如果提示`authentication token manipulation error`. 先执行`mount -o rw,remount /` 再修改密码

### 安装adb

直接用android sdk自带的

```
sudo vim /etc/environment 
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/home/hefeng/Android/Sdk/platform-tools
sudo source /etc/environment 
```




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
