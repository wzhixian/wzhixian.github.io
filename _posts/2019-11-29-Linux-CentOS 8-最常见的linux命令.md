---
layout: post
title: Linux-CentOS 8-最常见的linux命令
categories: Linux
description: Linux-CentOS 8-最常见的linux命令
keywords: Linux, linux命令
---

# Linux-CentOS 8-最常见的linux命令

**系统经典语录：**  
**1、命令操作完没有任何消息信息, 就是最好的消息**  
**2、系统一切从根开始**  
**3、系统中数据一切皆文件**  

## 一、linux关机命令：
1.shutdown命令安全地将系统关机（推荐）参数说明:

    [-r] 重启计算器。
	[-h] 关机后关闭电源〔halt〕。
	[-c] cancel current process取消目前正在执行的关机程序。
	[-time] 设定关机〔shutdown〕前的时间。
	
	shutdown -h  now   	=	立刻关机
	shutdown -h  时间  	= 	时间关机
	shutdown -r  now  	=	立即重启
	shutdown -h  10     =	十分钟后关机
2.halt 也可单独使用，也可达到关机的效果，但halt命令是其实halt就是调用shutdown -h。halt执行时，杀死应用进程，执行sync系统调用，内核停止，可能导致linux系统的死机，需要重启。  
3.poweroff 会发送一个 ACPI 信号来通知系统关机。  
4.init 进程一共分为7个级别, 0和6分别代表关闭和重启  

## 二、linux重启命令：

reboot 执行重启命令

## 三、linux查询所在位置路径：pwd

	[root@localhost network-scripts]# pwd
	/etc/sysconfig/network-scripts
	
## 四、linux切换目录：cd

    [root@localhost network-scripts]# cd -
	/root
	[root@localhost ~]# 

	[root@localhost network-scripts]# cd ..
	[root@localhost sysconfig]# 

	[root@localhost sysconfig]# cd
	[root@localhost ~]# 

## 五、linux创建目录文件：mkdir

参数：-p 递归创建

    [root@localhost /]# mkdir 123
	[root@localhost /]# mkdir -p 123/123

## 六、linux以树形结构展示目录结构：tree

参数：-L ：指定层数 -d：只显示目录

	[root@localhost /]# tree -d boot
	boot
	├── efi
	│   └── EFI
	│       └── centos
	├── grub2
	│   ├── fonts
	│   └── i386-pc
	├── loader
	│   └── entries
	└── lost+found

## 七、linux查看命令：ls
参数：-l ：长格式显示 -a ：显示所有文件 -d ：显示目录

    [root@localhost /]# ls -l abc
	total 0
	drwxr-xr-x. 2 root root 6 Oct 16 18:31 abc
	[root@localhost /]# ls -d abc
	abc
	[root@localhost /]# ls -a
	.   abc   backup  boot  dev  home  lib64  mnt  proc  run   server  sys  usr
	..  application  bin   data  etc  lib   media   opt  root  sbin  srv   tmp  var

## linux复制命令：cp
注释：111是目录文件，222是文本
参数：- r 递归 -i 是否覆盖确认 -a 相当于dpr -p保持文件或目录树形  

	命令格式：cp [-adfilprsu] 源文件(source) 目标文件(destination)
              cp [option] source1 source2 source3 ...  directory
    参数说明：
		-a:是指archive的意思，也说是指复制所有的目录
    	-d:若源文件为连接文件(link file)，则复制连接文件属性而非文件本身
    	-f:强制(force)，若有重复或其它疑问时，不会询问用户，而强制复制
    	-i:若目标文件(destination)已存在，在覆盖时会先询问是否真的操作
    	-l:建立硬连接(hard link)的连接文件，而非复制文件本身
    	-p:与文件的属性一起复制，而非使用默认属性
    	-r:递归复制，用于目录的复制操作
    	-s:复制成符号连接文件(symbolic link)，即“快捷方式”文件
		-u:若目标文件比源文件旧，更新目标文件
    如将/test1目录下的file1复制到/test3目录，并将文件名改为file2,可输入以下命令：
    cp /test1/file1 /test3/file2
	
	[root@localhost 123]# ls
	111  222
	[root@localhost 123]# cp 222 /456/999
	[root@localhost 123]# cd /456
	[root@localhost 456]# ls
	999
	[root@localhost 456]# cp -r /123/111 /456/888
	[root@localhost 456]# ls
	888  999

## 九、linux删除命令：rm
参数：- r 递归 - f 强制 两个一起用你可以删掉世界（很暴力很血腥，危险的命令）
    [root@localhost /]# rm -rf /123 /456
	[root@localhost wzx]# rm -rf c

## 十、linux更改命令别名：alias
删除别名：unalias  

    [root@localhost /]# alias ls='echo Hello,World!'
	[root@localhost /]# ls
	Hello,World!
	[root@localhost /]# unalias ls
	[root@localhost ~]# ls
	anaconda-ks.cfg

## 十一、linux移动命令：mv

参数：- t 把所用源参数移动到目录中
在相同路径目录中使用相当于改名，在不同路径中相当于移动

	[root@localhost 123]# ls
	888
	[root@localhost 123]# mv /123/888 777
	[root@localhost 123]# ls
	777
	[root@localhost 123]# mv /123/888 777
	[root@localhost 123]# ls
	777
	[root@localhost 123]# mv /123/777 /456/777
	[root@localhost 123]# ls
	[root@localhost 123]# cd /456
	[root@localhost 456]# ls
	777

## 十二、linux打印输出命令：echo

参数：-h 不换行 - e 支持转义 \t 代表top \n 代表回车

	[root@localhost /]# echo 8
	8

## 十三、linux创建文件或更新文件时间戳：touch

		[root@localhost wzx]# touch 123
		[root@localhost wzx]# ll
		total 0  
		-rw-r--r--. 1 root root 0 Oct 21 19:18 123
		[root@localhost wzx]# touch 123
		[root@localhost wzx]# ll
		total 0
		-rw-r--r--. 1 root root 0 Oct 21 19:19 123

## 十四、linux创建查看文件内容：cat

参数： -n 显示行号
	
	[root@localhost wzx]# cat 123
	123
	123
	123
	[root@localhost wzx]# cat -n 123
	     1	123
	     2	123
	     3	123

## 十五、linux输出头部 / 尾部部分文件：head / tail

参数：-n 行数

	[root@localhost wzx]# head -n 4 123
	1
	2
	3
	4
	[root@localhost wzx]# tail -n 4 123
	27
	28
	29
	30

## 十六、linux替换或删除字符：tr

注意：只是把文件内容输出出来，而不是改变文件内容

	[root@localhost wzx]# cat aa
	999999888888
	[root@localhost wzx]# tr '9' '1' <aa
	111111888888
	[root@localhost wzx]# cat aa
	999999888888

## 十七、linux查找文件里符合条件的字符串：grep

linux中常用的文本（awk，sed，grep）处理工具之一  
首先谈一下grep命令的常用格式为：grep [选项] ”模式“ [文件]  
grep家族总共有三个：grep，egrep，fgrep  

**参数：**  

    	参数					用途
		--color =auto		过滤的内容加颜色
		-v  				取反
		-i					不区分大小写
		-n					显示行号
		-w					按单词位单位过滤
		-o					只输出匹配的内容
		-E					相当于egrep(过滤多个参数）
		-A					显示过滤字符串和它之后多少行
		-B					显示过滤字符串和它之前多少行
		-C					显示过滤字符串和它之前之后多少行

**简单应用：**

	[root@localhost wzx]# grep -A 2 '15' 123
	15
	16
	17
	[root@localhost wzx]# grep -C 2 '15' 123
	13
	14
	15
	16
	17
	[root@localhost wzx]# grep -B 2 '15' 123
	13
	14
	15
	[root@localhost wzx]# grep -n '15' 123
	15:15
	[root@localhost wzx]# grep '15' 123
	15
	[root@localhost wzx]# grep '1' 123
	1
	10
	11
	[root@localhost wzx]# grep -o '1' 123
	1
	1
	1
	[root@localhost wzx]# grep -w '1' 123
	1
	[root@localhost wzx]# egrep -v "^[1-9]$|[1-2][0-9]" 123
	30

## 十八、linux查看文件类型：file

	[root@localhost wzx]# file usr/bin/cp
	usr/bin/cp: cannot open `usr/bin/cp' (No such file or directory)

## 十九、linux：创建创建软硬链接：ln

参数：- s 创建软连接

	[root@yu shangke]# ln -s /yuxi/shangke/123.txt /yuxi/xuexi/ruanlianjie.txt
	[root@yu xuexi]# ll -i
	     352 lrwxrwxrwx. 1 root root 21 Oct 21 21:12 ruanlianjie.txt -> /yuxi/shangke/123.txt
	[root@yu xuexi]# ln /yuxi/shangke/123.txt /yuxi/xuexi/lianjie.txt
	[root@yu xuexi]# ll -i
	16814069 -rw-r--r--. 2 root root 4 Oct 21 21:06 lianjie.txt
	16814069 -rw-r--r--. 2 root root 4 Oct 21 21:06 123.txt

## 二十、linux：查命令所在路径：which

	[root@localhost wzx]# which rm
	alias rm='rm -i'
		/usr/bin/rm

## 二十一、 查找目录下文件：find

**参数：**  

		参数 			用途  
		-name 		按文件名查找
		-type 		按文件类型查找(后面接文件类型参数,例如：目录 d 文件 f
		-exec 		对搜索结果在处理
		-mtime 	按修改时间查找
		
**简单应用：**

	[root@localhost wzx]# find / -name cp
	/usr/bin/cp
	[root@localhost wzx]# find /usr/wzx/ -type f
	/usr/wzx/nginx.conf
	/usr/wzx/aa

## 二十二、从标准输入执行命令：xargs

这只是最基础参考，命令的九牛一毛，详解百度搜索xargs命令

**参数：**

		参数 		用途
		-n 	数字，把几个数字一组
		-d 	指定分隔符，默认空格
		-i 	把{}当作前面查找的结果

		[root@localhost wzx]# cat aa.txt |xargs -n 3
		1 2 3
		4 5 6
		7 8 9

## 二十三、查看用户身份uid/gid：id

	[root@localhost wzx]# id
	uid=0(root) gid=0(root) 组=0(root) 环境=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

## 二十四、查看当前用户/添加普通用户：whoami / uesradd

	[root@localhost wzx]# whoami
	root

## 二十五、查看文件属性：stat

	[root@localhost wzx]# stat /a
	  文件：/a
	  大小：2656      	块：8          IO 块：4096   普通文件
	设备：fd00h/64768d	Inode：488652      硬链接：1
	权限：(0644/-rw-r--r--)  Uid：(    0/    root)   Gid：(    0/    root)
	环境：unconfined_u:object_r:etc_runtime_t:s0
	最近访问：2019-11-29 14:44:28.730408854 +0800
	最近更改：2019-11-29 14:33:50.662429982 +0800
	最近改动：2019-11-29 14:33:50.662429982 +0800
	创建时间：-

## 二十六、显示系统时间和日期：date

参数：- s 修改时间 - d 只能过去或未来格式

	[root@localhost wzx]# date
	2019年 11月 29日 星期五 15:36:18 CST

## 二十七、 查看运行等级：runlevel

	[root@localhost wzx]# runlevel
	N 5

## 二十八、切换运行级别：init

	[root@localhost ~]# init 5
	[root@localhost ~]# runlevel
	3 5
	[root@localhost shangke]# init 0
	[root@localhost shangke]# init 6

## 二十九、修改主机名：hostname

	[root@localhost ~]# hostname wangzhixian
	[root@localhost ~]# hostnamectl set-hostname wangzhixian

## 三十、压缩打包：tar
	
		参数 			用途
		- z 		压缩
		- c 		创建
		- v 		输出打包过程
		- f 		文件
		- t 		查看文件
		- C 		指定解压路径
		- x 		解压
		- h 		跟随软连接
		- exclude 	排除不打包文件
		- X 		从文件中排除不打包的文件

## 三十一、查看文件系统：df

参数：- i inode 信息 - h 查看block信息

	[root@localhost /]# df -h
	文件系统             容量  已用  可用 已用% 挂载点
	devtmpfs             889M     0  889M    0% /dev
	tmpfs                904M   28M  876M    4% /dev/shm
	tmpfs                904M  9.7M  894M    2% /run
	tmpfs                904M     0  904M    0% /sys/fs/cgroup
	/dev/mapper/cl-root   17G  4.4G   13G   26% /
	/dev/nvme0n1p1       976M  184M  726M   21% /boot
	tmpfs                181M   16K  181M    1% /run/user/42
	tmpfs                181M  3.5M  178M    2% /run/user/1000
	[root@localhost /]# df -i
	文件系统              Inode 已用(I) 可用(I) 已用(I)% 挂载点
	devtmpfs             227491     399  227092       1% /dev
	tmpfs                231178      81  231097       1% /dev/shm
	tmpfs                231178     853  230325       1% /run
	tmpfs                231178      17  231161       1% /sys/fs/cgroup
	/dev/mapper/cl-root 8910848  130399 8780449       2% /
	/dev/nvme0n1p1        65536     316   65220       1% /boot
	tmpfs                231178      19  231159       1% /run/user/42
	tmpfs                231178      38  231140       1% /run/user/1000

## 三十二、点：source

source命令是bash shell的内置命令，点命令，就是个点符号，是source的另一名称  
当前脚本中配置的变量也将作为脚本的环境，source（或点）命令通常用于重新执行刚修改的初始化文档，比如 . bash_profile 和 . profile 等等

## 三十三、查看磁盘文件UUID信息：blkid

	[root@localhost /]# blkid
	/dev/nvme0n1: PTUUID="8ea9bc38" PTTYPE="dos"
	/dev/nvme0n1p1: UUID="1e7db250-e91c-4682-9772-9cea6fac5636" TYPE="ext4" PARTUUID="8ea9bc38-01"
	/dev/nvme0n1p2: UUID="RTswFQ-wTKP-L34Z-wLFN-yN6J-2Ls2-5axFbe" TYPE="LVM2_member" PARTUUID="8ea9bc38-02"
	/dev/mapper/cl-root: UUID="fda2e07a-82ed-4449-98d0-5d324631915f" TYPE="xfs"
	/dev/mapper/cl-swap: UUID="b7f97e16-0252-4582-9974-cbd2d4311b26" TYPE="swap"

## 三十四、指定某个网卡激活启动/关闭：ifdown/ifup

	[root@localhost ~]# ifdown ens33 && ifup ens33
	Device 'ens33' successfully disconnected.
	Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/2)

## 三十五、查看服务是否开启：telnet

telnet命令通常用来远程登录，但也可以确定远程服务的状态，比如确定远程服务器的某个端口是否能访问。

	[root@localhost /]# telnet 10.0.0.200 22
	Trying 10.0.0.200...
	telnet: connect to address 10.0.0.200: Connection refused

## 三十六、检查及删除文本文件中重复出现的行列 / 文本文件内容加以排序：uniq / sort

sort几个常用参数：
注意uniq命令只能筛选两行在一起的数据，分开无法筛选，筛选前先排序

		参数 			用途
		uniq 	
		-c 			在每列旁边显示该行重复出现的次数
		-d 			仅显示重复出现的行列
		-u 			仅显示出一次的行列
		sort 	
		-b 			忽略每行前面开始出的空格字符
		-r 			以相反的顺序来排序
		-n 			依照数值的大小排序


		[root@localhost wzx]# cat 1
		1
		haha
		2
		haha
		3
		haha
		4
		haha
		[root@localhost wzx]# sort -n 1 |uniq -c
		      4 haha
		      1 1
		      1 2
		      1 3
		      1 4

## 三十七、外国人在厕所学统计：wc（统计，用于计算数字）

参数： - l 只显示行数

	[root@localhost wzx]# wc -l aa
	1 aa

## 三十八、查看硬件信息大礼包

		命令 			用途
		lscpu 		查看cpu使用情况
		free 		查看内存使用情况
		w 			查看负载使用情况
		top 		查看负载使用情况
		uptime 		查看负载使用情况

## 三十九、删除执行中的程序：kill

强行杀死进程（很暴力很血腥，危险的命令）

	[[root@localhost wzx]# kill -KILL pts/1

## 四十、显示目录或文件的大小：du

参数：- h 人类能看懂的形式显示出来
注：显示指定的目录或文件所占用的磁盘空间

		[root@localhost wzx]# du -h aa
		4.0K	aa

## 四十一、显示当前进程 (process) 的状态：ps

	[root@localhost wzx]# ps
	   PID TTY          TIME CMD
	  3223 pts/0    00:00:00 su
	  3230 pts/0    00:00:00 bash
	  8240 pts/0    00:00:00 su
	  8243 pts/0    00:00:00 bash
	  8270 pts/0    00:00:00 su
	  8336 pts/0    00:00:00 su
	  8344 pts/0    00:00:00 bash
	  8843 pts/0    00:00:00 grep
	  8871 pts/0    00:00:00 grep
	  8885 pts/0    00:00:00 grep
	  9948 pts/0    00:00:00 ps
