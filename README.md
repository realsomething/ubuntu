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

* lzma_decompress.img切换到保护模式需要做以下三件事:

  * 启用分段, 辅助进程管理

  * 启动分页, 辅助内存管理

  * 打开其他地址线

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

### ELF文件的分类

编译成 ELF 格式的二进制文件, 有三种格式(可重定位 .o 文件; 可执行文件; 共享对象文件 .so)

- 可重定位 .o 文件(ELF 第一种格式)
    - .h + .c 文件, 编译得到**可重定位** .o 文件 

    - .o 文件由: ELF 头, 多个节(section), 节头部表组成(每个节的元数据); 节表的位置和纪录数由 ELF 头给出

      ```
      section包括：
      .text：放编译好的二进制可执行代码
      .data：已经初始化好的全局变量
      .rodata：只读数据，例如字符串常量、const 的变量
      .bss：未初始化全局变量，运行时会置 0
      .symtab：符号表，记录的则是函数和变量
      .strtab：字符串表、字符串常量和变量名
      ```

    - .o 文件只是程序部分代码片段

    - .rel.text 和 .rel.data 标注了哪些函数/变量需要重定位

    - 要函数可被调用, 要以库文件的形式存在, 最简单是创建静态链接库 .a 文件(Archives)，通过 ar 创建静态链接库

      ```
      ar cr libstaticprocess.a process.o
      ```

       通过 gcc 提取库文件中的 .o 文件, 链接到程序中

      ```
      gcc -o staticcreateprocess createprocess.o -L. -lstaticprocess
      
      -L 表示在当前目录下找.a 文件，-lstaticprocess 会自动补全文件名，比如加前缀 lib，后缀.a，变成 libstaticprocess.a，找到这个.a 文件后，将里面的 process.o 取出来，和 createprocess.o 做一个链接，形成二进制执行文件 staticcreateprocess
      ```

    - 链接合并后, 就可以定位到函数/数据的位置, 形成可执行文件

- 可执行文件(ELF 第二种格式)
    - 链接合并后, 形成可执行文件，这个格式和.o 文件大致相似，还是分成一个个的 section，并且被节头表描述。只不过这些 section 是多个.o合并过的

    - 同样包含: ELF 头, 多个节, 节头部表; 另外还有段头表(包含段的描述, p_vaddr 段加载到内存的虚拟地址)

      ```
      section包括：
      代码段：
      .text：放编译好的二进制可执行代码
      .rodata：只读数据，例如字符串常量、const 的变量
      
      数据段：
      .data：已经初始化好的全局变量
      .bss：未初始化全局变量，运行时会置 0
      
      不加载到内存：
      .symtab：符号表，记录的则是函数和变量
      .strtab：字符串表、字符串常量和变量名
      ```

    - ELF 头中有 e_entry , 指向程序入口的虚拟地址

    - 静态链接库一旦链接进去，代码和变量的 section 都合并了，因而程序运行的时候，就不依赖于这个库是否存在。但是这样相同的代码段，如果被多个程序使用的话，在内存里面就有多份，而且一旦静态链接库更新了，如果二进制执行文件不重新编译，也不随着更新

- 共享对象 .so 文件(Shared Libraries，ELF 第三种格式)
    - 静态链接库合并进可执行文件, 但是多个进程不能共享

    - 动态链接库-链接了动态链接库的程序, 仅包含对该库的引用(且只保存名称),而不包含其代码

      ```
      gcc -o dynamiccreateprocess createprocess.o -L. -ldynamicprocess
      
      通过 gcc 创建和链接, 运行时, 先找到动态链接库(默认在 /lib 和 /usr/lib 找),找不到就会报错
      
      设定 LD_LIBRARY_PATH环境变量，程序运行时会在此环境变量指定的文件夹下寻找动态链接库
      
      export LD_LIBRARY_PATH=.
      ```

    - ELF的section增加了 .interp 段, 里面是 ld_linux.so (动态链接器)

    - 增加了两个节 .plt(Procedure Linkage Table：过程链接表)和 .got.plt(Global Offset Table：全局偏移表)

    - 一个动态链接函数对应 plt 中的一项 plt[x], plt[x] 中是代理代码, 调用 got 中的一项 got[y]

    - 起始, got 没有动态链接函数的地址, 都指向 plt[0], plt[0] 又调用 got[2], got[2]指向 ld_linux.so

    - ld_linux.so 找到加载到内存的动态链接函数的地址, 并将地址存入 got[y]

- 加载 ELF 文件到内存
    - 系统调用 exec 最终调用 load_elf_binary(do_execve->do_execveat_common->exec_binprm->search_binary_handler)
    - exec 是一组函数
        - 包含 p: 在 PATH 中找程序，如 execvp, execlp
        - 不包含 p: 需提供全路径
        - 包含 v: 以数字接收参数，如 execv, execvp, execve
        - 包含 l: 以列表接收参数，如 execl, execlp, execle
        - 包含 e: 以数字接收环境变量，如 execve, execle

- 进程树

    所有的进程都是从父进程 fork 过来的，祖宗进程就是系统启动的 init 进程，系统启动之后，init 进程会启动很多的 daemon 进程，为系统运行提供服务，然后启动 getty，让用户登录

    - ps -ef: 用户进程不带中括号, 内核进程带中括号
    - 用户进程祖先(1号进程, systemd); 内核进程祖先(2号进程, kthreadd)
    - tty ? 一般表示后台服务

* 分析工具

  * readelf 工具用于分析 ELF 的信息

  * objdump工具用来显示二进制文件的信息

  * hexdump 工具用来查看文件的十六进制编码

  * nm 工具用来显示关于指定文件中符号的信息

### 多线程并行

多进程缺点：创建进程占用资源多; 进程间通信需拷贝内存, 不能共享

- 线程相关操作
    - pthread_exit(A), A 是线程退出的返回值
    - pthread_attr_t 线程属性, 用辅助函数初始化并设置值; 用完需要销毁
    - pthread_create 创建线程, 四个参数(线程对象, 属性, 运行函数, 运行参数)
    - pthread_join 获取线程退出返回值, 多线程依赖 libpthread.so
    - 一个线程退出, 会发送信号给 其他所有同进程的线程
- 线程中有三类数据
    - 线程栈本地数据, 栈大小默认 8MB(通过命令 ulimit -a 查看， ulimit -s 修改); 线程栈之间有保护间隔, 若误入会引发段错误

      ```
      修改线程栈的大小：
      int pthread_attr_setstacksize(pthread_attr_t *attr, size_t stacksize);
      ```

    - 进程共享的全局数据，若多个线程一起修改，会有问题

    - 线程级别的全局变量(线程私有数据); key 所有线程都可以访问, 可填入各自的值(同名不同值的全局变量)，等到线程退出的时候，就会调用析构函数释放 value

    - ```
      创建：
      int pthread_key_create(pthread_key_t *key, void (*destructor)(void*))
      
      设置：
      int pthread_setspecific(pthread_key_t key, const void *value)
      
      获取：
      void *pthread_getspecific(pthread_key_t key
      ```
- 数据保护
    - Mutex(互斥)，lock(没抢到则阻塞)/trylock(没抢到则返回错误码)

      ```
      初始化：
      pthread_mutex_init(&g_task_lock, NULL);
      
      加锁：
      pthread_mutex_lock(&g_task_lock);
      
      解锁：
      pthread_mutex_unlock(&g_task_lock)
      
      销毁：
      pthread_mutex_destroy(&g_task_lock);
      ```

      

    - 条件变量(通知), 收到通知, 还是要抢锁(由 wait 函数执行); 因此条件变量与互斥锁配合使用

      ```
      初始化：
      pthread_cond_init(&g_task_cv, NULL);
      
      通知所有线程：
      pthread_cond_broadcast(&g_task_cv);
      
      等待，收到通知就退出
      pthread_cond_wait(&g_task_cv, &g_task_lock);
      
      销毁：
      pthread_cond_destroy(&g_task_cv);
      ```

#### 内核任务

内核中进程, 线程统一为任务, 由 taks_struct 表示，它是一个链表

- task_struct 中包含: 任务ID; 任务状态; 信号处理相关字段; 调度相关字段; 亲缘关系; 权限相关; 运行统计; 内存管理; 文件与文件系统; 内核栈

- 任务 ID; 包含 pid, tgid 和 \*group_leader
    - pid(process id, 线程的id); tgid(thread group id, 所属进程[主线程]的id); group_leader 指向 tgid 的结构体
    - 通过对比 pid 和 tgid 是否相同可判断是进程还是线程

- 信号处理, 包含阻塞暂不处理、等待处理、正在处理的信号
    - 信号处理函数默认使用用户态的函数栈, 也可以开辟新的栈专门用于信号处理, 由 sas_ss_xxx 指定
    - 通过 pending/shared_pending 区分进程和线程的信号

- 任务状态; 包含 state; exit_state; flags
    - 准备运行状态 TASK_RUNNING

    - 睡眠状态：可中断; 不可中断; 可杀
        - 可中断 TASK_INTERRUPTIBLE，浅睡眠，收到信号要被唤醒，只不过唤醒后，不是继续刚才的操作，而是进行信号处理

        - 不可中断 TASK_UNINTERRUPTIBLE，深睡眠，一旦等待的IO操作无法完成，则收到信号不会被唤醒, 自然不能被kill, 只能重启

        - 可杀 TASK_KILLABLE, 可以响应致命信号, 由不可中断与 TASK_WAKEKILL 组合

          ```
          #define TASK_KILLABLE           (TASK_WAKEKILL | TASK_UNINTERRUPTIBLE)
          ```

    - 停止状态 TASK_STOPPED, 由信号 SIGSTOP, SIGTTIN, SIGTSTP 与 SIGTTOU 触发进入

    - 调试跟踪 TASK_TRACED， 被 debugger 等进程监视时进入

    - 结束状态(包含 exit_state)
        - EXIT_ZOMBIE, 父进程还没有使用 wait()等系统调用获知它的终止信息，此时就是僵尸进程
        - EXIT_DEAD, 最终状态

    - 其他的标志则放到flags

        * PF_EXISTING 表示正在退出，在函数 find_alive_thread 中，找活着的线程时，遇到有这个 flag 的，就直接跳过
        * PF_VCPU 表示运行在虚拟 CPU 上
        * PF_FORKNOEXEC表示 fork 完了，还没有 exec，在 \_do_fork 函数里设置，exec 函数中清除

- 进程调度; 包含 是否在运行队列; 优先级; 调度策略; 可以使用那些 CPU 等信息

- 运行统计信息, 包含用户/内核态运行时间; 上/下文切换次数; 启动时间等

    ```
    u64				utime;// 用户态消耗的 CPU 时间
    u64				stime;// 内核态消耗的 CPU 时间
    unsigned long	nvcsw;//  自愿 (voluntary) 上下文切换计数
    unsigned long	nivcsw;// 非自愿 (involuntary) 上下文切换计数
    u64				start_time;		// 进程启动时间，不包含睡眠时间
    u64				real_start_time;// 进程启动时间，包含睡眠时间
    ```

- 进程亲缘关系

    ```
    struct task_struct __rcu *real_parent; 	/* real parent process */
    struct task_struct __rcu *parent; 		/* recipient of SIGCHLD, wait4() reports */
    struct list_head children;      /* list of my children */
    struct list_head sibling;       /* linkage in my parent's children list */
    ```

    - 拥有同一父进程的所有进程具有兄弟关系
    - children 表示链表的头部，链表中的所有元素都是它的子进程
    - sibling 用于把当前进程插入到兄弟链表中
    - parent 指向的父进程接收进程结束信号
    - real_parent 和 parent 通常一样; 但在 bash 中用 GDB 调试程序时, GDB 是 parent, bash 是 real_parent

- 进程权限, 包含 real_cred 指针(谁能操作我); cred 指针(我能操作谁)

    ```
    /* Objective and real subjective task credentials (COW): */
    const struct cred __rcu         *real_cred;	// 谁能操作我
    /* Effective (overridable) subjective task credentials (COW): */
    const struct cred __rcu         *cred;		// 我能操作谁
    ```

    ```
    struct cred {
    ......
            kuid_t          uid;            /* real UID of the task */
            kgid_t          gid;            /* real GID of the task */
            kuid_t          suid;           /* saved UID of the task */
            kgid_t          sgid;           /* saved GID of the task */
            kuid_t          euid;           /* effective UID of the task */
            kgid_t          egid;           /* effective GID of the task */
            kuid_t          fsuid;          /* UID for VFS ops */
            kgid_t          fsgid;          /* GID for VFS ops */
    ......
            kernel_cap_t    cap_inheritable; /* caps our children can inherit */
            kernel_cap_t    cap_permitted;  /* caps we're permitted */
            kernel_cap_t    cap_effective;  /* caps we can actually use */
            kernel_cap_t    cap_bset;       /* capability bounding set */
            kernel_cap_t    cap_ambient;    /* Ambient capability set */
    ......
    } __randomize_layout;
    ```

    - cred 结构体中标明多组用户和用户组 id

    - uid/gid(哪个用户的进程启动我，权限审核不比较这两个)

    - euid/egid(按照哪个用户审核权限, 操作消息队列, 共享内存等，真正起作用的用户和组)

    - fsuid/fsgid(文件操作时审核)

    - 一般说来，fsuid、euid，和 uid 是一样的，fsgid、egid，和 gid 也是一样的。因为谁启动的进程，就应该审核启动的用户到底有没有这个权限

    - 通过 chmod u+s program, 给程序设置 set-user-id 标识位, 运行时程序将进程 euid/fsuid 改为程序文件所有者 id，而program的实际所有者保存在suid/sgid中

    - suid/sgid 可以用来保存 id, 进程可以通过 setuid 更改 uid

    - capability 机制, 以细粒度赋予普通用户部分高权限 (capability.h 列出了权限)

        ```
        #define CAP_CHOWN            0
        #define CAP_KILL             5
        #define CAP_NET_BIND_SERVICE 10
        #define CAP_NET_RAW          13
        #define CAP_SYS_MODULE       16
        #define CAP_SYS_RAWIO        17
        #define CAP_SYS_BOOT         22
        #define CAP_SYS_TIME         25
        #define CAP_AUDIT_READ       37
        #define CAP_LAST_CAP         CAP_AUDIT_READ
        ```

        - cap_permitted 表示进程的权限
        - cap_effective 实际起作用的权限, cap_permitted 范围可大于 cap_effective，一个进程在必要的时候放弃某些权限，更加安全
        - cap_inheritable 若可执行文件的扩展属性设置了该权限，表示可被继承, 在 exec 执行时继承的权限集合, 并加入 cap_permitted 中(但非 root 用户不会保留 cap_inheritable 集合)
        - cap_bset(capability bounding set)所有进程保留的权限(限制只用一次的功能)，如系统启动以后，将加载内核模块的权限去掉，那所有进程都不能加载内核模块。即便这台机器被攻破，也做不了太多有害的事情
        - cap_ambient 比较新加入内核的，就是为了解决 cap_inheritabl鸡肋的问题 ，exec 时, 并入 cap_permitted 和 cap_effective 中

- 内存管理: mm_struct

    ```
    struct mm_struct                *mm;
    struct mm_struct                *active_mm;
    ```

- 文件与文件系统: 打开的文件, 文件系统相关数据结构

    ```
    /* Filesystem information: */
    struct fs_struct                *fs;
    /* Open file information: */
    struct files_struct             *files;
    ```

### 用户态函数栈

- 用户态/内核态切换如何关联：

```
struct thread_info		thread_info;
void  *stack;
```

- 用户态函数栈

  * 通过 JMP + 参数 + 返回地址 调用函数

  - 栈内存空间从高到低增长
  - 32位栈结构: 栈帧包含 前一个帧的 EBP + 局部变量 + N个参数 + 返回地址
    - ESP: 栈顶指针，push和pop操作后会自动调整
    - EBP: 栈基指针(栈帧最底部, 局部变量起始)
    - EAX: 保存返回结果
  - 64位栈结构: 结构类似
    - rsp: 栈顶指针
    - rbp: 栈基指针
    - rax: 保存返回结果
    - 参数传递时, 前 6个放寄存器中(再由被调用函数 push 进自己的栈, 用以寻址), 参数超过 6个压入栈中

  ### 内核栈

- 内核栈结构

  - Linux 为每个 task 分配了内核栈, 32位(8K), 64位(16K)
  - 栈结构: [预留8字节 +] pt_regs + 内核栈 + 头部 thread_info
  - thread_info 是 task_struct 的补充, 存储于体系结构有关的内容
  - pt_regs 用以保存用户运行上下文, 通过 push 寄存器到栈中保存

  ```
  #define task_pt_regs(task) \
  ({									\
  	unsigned long __ptr = (unsigned long)task_stack_page(task);	\
  	__ptr += THREAD_SIZE - TOP_OF_KERNEL_STACK_PADDING;		\
  	((struct pt_regs *)__ptr) - 1;					\
  })
  ```

- 通过 task_struct 找到内核栈

  ```
  static inline void *task_stack_page(const struct task_struct *task)
  {
  	return task->stack;
  }
  ```

  - 直接由 task_struct 内的 stack 直接得到指向 thread_info 的指针

- 通过内核栈找到 task_struct

  - 32位 直接由 thread_info 中的指针得到
  - 64位 每个 CPU 当前运行进程的 task_struct 的指针存放到 Per CPU 变量 current_task 中; 可调用 this_cpu_read_stable 进行读取

### 调度策略与调度类

进程包括两类: 实时进程(优先级高); 普通进程。 两种进程调度策略不同: task_struct->policy 指明采用哪种调度策略(有6种策略)

```
unsigned int policy;

#define SCHED_NORMAL		0
#define SCHED_FIFO		    1
#define SCHED_RR		    2
#define SCHED_BATCH		    3
#define SCHED_IDLE		    5
#define SCHED_DEADLINE		6

int prio, static_prio, normal_prio;
unsigned int rt_priority;
```

优先级配合调度策略, 实时进程(0-99); 普通进程(100-139)

#### 实时调度策略

高优先级可抢占低优先级进程

- SCHED_FIFO: 相同优先级进程先来先得
- SCHED_RR: 轮流调度策略, 采用时间片轮流调度相同优先级进程
- SCHED_DEADLINE: 在调度时, 选择 deadline 最近的进程

#### 普通调度策略

- SCHED_NORMAL: 普通进程
- SCHED_BATCH: 后台进程, 可以降低优先级
- SCHED_IDLE: 空闲时才运行

#### 调度策略的调度类

task_struct 中 * sched_class 指向封装了调度策略执行逻辑的类(有5种)

- stop_sched_class: 优先级最高. 将中断其他所有进程, 且不能被打断
- dl_sched_class: 实现 deadline 调度策略
- rt_sched_class: RR 或 FIFO, 具体策略由 task_struct->policy 指定
- fair_sched_class: 普通进程调度
- idle_sched_class: 空闲进程调度

#### 普通进程的 fair 完全公平调度算法 CFS

- 记录进程运行时间( vruntime 虚拟运行时间)
- 优先调度 vruntime 小的进程
- 按照比例累计 vruntime, 使之考虑进优先级关系

```
虚拟运行时间 vruntime += 实际运行时间 delta_exec * NICE_0_LOAD/ 权重
```

#### 调度队列和调度实体

- CFS 中需要对 vruntime 排序找最小, 不断查询更新, 因此利用红黑树实现调度队列
- task_struct 中有 实时调度实体sched_rt_entity, Deadline 调度实体sched_dl_entity 和 完全公平调度实体 sched_entity, cfs 调度实体即红黑树节点
- 所有可运行的进程通过不断地插入操作最终都存储在以时间为顺序的红黑树中，vruntime 最小的在树的左侧，vruntime 最多的在树的右侧。 CFS 调度策略会选择红黑树最左边的叶子节点作为下一个将获得 cpu 的任务
- 每个 CPU 都有 rq 结构体, 里面有 rt_rq 和 cfs_rq 调度队列以及其他信息; 队列描述该 CPU 所运行的所有进程
- 先在 rt_rq 中找进程运行, 若没有再到 cfs_rq 中找; cfs_rq 中 rb_root 指向红黑树根节点, rb_leftmost指向最左节点

#### 调度类如何工作

```
struct sched_class {
	const struct sched_class *next;
...
	void (*enqueue_task) (struct rq *rq, struct task_struct *p, int flags);
	void (*dequeue_task) (struct rq *rq, struct task_struct *p, int flags);
...
	struct task_struct * (*pick_next_task) (struct rq *rq,
						struct task_struct *prev,
						struct rq_flags *rf);

}
extern const struct sched_class stop_sched_class;
extern const struct sched_class dl_sched_class;
extern const struct sched_class rt_sched_class;
extern const struct sched_class fair_sched_class;
extern const struct sched_class idle_sched_class;
const struct sched_class fair_sched_class = {
	.next			= &idle_sched_class,
	...
}
```

- 调度类中有一个成员指向下一个调度类(按优先级顺序串起来)
- 找下一个运行任务时, 按 stop-dl-rt-fair-idle 依次调用调度类, 不同调度类操作不同调度队列
- 对于同样的 pick_next_task 选取下一个要运行的任务这个动作，不同的调度类有自己的实现。fair_sched_class 的实现是 pick_next_task_fair，rt_sched_class 的实现是 pick_next_task_rt。我们会发现这两个函数是操作不同的队列，pick_next_task_rt 操作的是 rt_rq，pick_next_task_fair 操作的是 cfs_rq
- 在每个 CPU 上都有一个队列 rq，这个队列里面包含多个子队列，例如 rt_rq 和 cfs_rq，不同的队列有不同的实现方式。某个 CPU 需要找下一个任务执行的时候，会按照优先级依次调度类，不同的调度类操作不同的队列。当然 rt_sched_class 先被调用，它会在 rt_rq 上找下一个任务，只有找不到的时候，才轮到 fair_sched_class 被调用，它会在 cfs_rq 上找下一个任务。这样保证了实时任务的优先级永远大于普通任务





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
