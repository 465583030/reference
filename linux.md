#Linux基础知识

####致敬linux**[Linus Torvalds采访][1]**

1. 虚拟机的使用
	* VMware主要特点
		1. 不需要分区或重新开机就能在同一台PC上使用两种以上的操作系统
		2. 本机系统可以与虚拟机系统网络通信
		3. 可以设定并且随时修改虚拟机操作系统的硬件环境
		4. 快照
		
1. 云计算平台
	1. AWS
	2. 阿里云
	3. 腾讯云

1. 安装

1. 分区&格式化&挂载(?????)


1. 命令提示符 [命令提示符][8]*可配置*
	* [当前登陆用户@主机名 当前所在目录]# 
	* `#` 超级用户
	* `$` 普通用户
	* 当前所在目录：
		* `~`家目录
		* `/root`root管理员的家目录
		* `/home/用户名`普通用户的家目录

1. **启动网卡**
	* `vim /etc/sysconfig/network-scripts/ifcfg-eth0`
	* 修改`ONBOOT=”yes”`
	* 重启网络服务`service network restart`
	
	[网卡配置文件][2]
	
1. **关闭防火墙iptables**
	1. 使用Setup工具关闭(*Centos系列*)
	
	[setup截图][3]

1. **关闭SELinux** (增强安全组件)
	1. 临时：`setenforce 0`
	2. 永久：`vim /etc/selinux/config` 修改为 `SELINUX=disabled` 最后重启生效
	
	[SELinux配置文件][4]
	
1. `man [command]`在线查看命令用法
1. `ls`显示目录下的内容
	* `ls -l` `ls -a` `ls -al` `ls -lls -lh`
	
	[ls-l解释][5]
	
	[文件颜色及类型][6]
	
	[常见文件类型][7]
	
1. `cd`切换所在目录 (change directory的缩写)
	* **一定要配合table键自动补全使用**
	* **绝对路径：**从根目录开始指定，逐级递归查找。在任何目录下，都能进入指定位置。`cd /usr/local` 切换到/usr/local目录下面
	* **相对路径** 参照当前所在目录，进行查找。一定要先确定当前所在目录。`cd  ../usr/local/src`
	* `cd ~` 进入当前用户的家目录		`/root` `/home/aa/`
	* `cd` 同上也是进入当前用户的家目录
	* `cd -` 进入上次目录
	* `cd ..` 进入上一级目录
	* `cd .` 进入当前目录(没用) 
	
1. `pwd` 显示当前所在工作目录 (print working directory)


1.  linux常见目录
	* `/` 根目录
	* `/bin` 命令保存目录（普通用户就可以使用的命令）
	* `/boot`启动目录，启动相关文件
	* `/dev`设备文件保存目录	
	* `/etc`**配置文件保存目录**
	* `/home`普通用户家目录
	* `/lib`系统库文件保存目录
	* `/mnt`挂载目录
	* `/root`初级用户的家目录
	* `/tmp`临时目录
	* `/sbin`超级用户使用的命令保存目录
	* `/proc`记录服务器内存及cpu情况的的动态文件系统
	* `/sys`同上
	* `/usr`系统软件资源目录
		* `/usr/bin/`系统命令（安装的软件可执行文件所在目录）
		* `/usr/sbin/`系统命令
		* `/usr/local`常用软件安装目录
	* `var`系统相关文档内容
		* `/var/log/`系统日志位置
		* `/var/spool/mail/`系统默认邮箱位置
	
	[linux目录结构][9]	
	
	[/usr目录结构][10]
		
1. 新建目录 `mkdir <目录名称>` (make directories)
	* `mkdir test`
	* `mkdir -p test/test1/test2`递归创建目录
	
1. 删除目录`rmdir <dirname>`
	* `rmdir <dirname>` **只能删除空目录,如果目录不为空会提示**

1. 删除文件 `rm filename`
	* `rm <filename>` 会询问你是否删除，需要输入`y`or`n`
	* `rm -f <filename>`直接强制删除，取消询问模式 **`f`**
	* `rm -r <dirname>`递归删除目录,会一个一个询问是否删除
	* `rm -rf <dirname>`递归强制删除目录及目录内的所有东西,不会询问

	
	
	




####Linux常识
1. 文件命名规则
	* 大小写敏感
	* 以(.)开头的文件为隐藏文件
	* 除了(/)之外，所有的字符都合法
	
2. linux命令的格式 `命令 [选项] [参数]`
	

	








[1]:http://open.163.com/movie/2016/6/3/9/MBPNHJU6K_MBR358639.html
[2]:https://cl.ly/0N3L0P2m3g3Z/Image%202016-09-04%20at%2009.37.14.png
[3]:https://cl.ly/1u441R1k3O3C/Image%202016-09-04%20at%2009.40.10.png
[4]:https://cl.ly/0H2K1m0P0p1I/Image%202016-09-04%20at%2009.48.52.png
[5]:https://cl.ly/2e3a0s3M3t2v/Image%202016-09-04%20at%2010.09.16.png
[6]:https://cl.ly/2i3b3b0v003X/Image%202016-09-04%20at%2010.11.38.png
[7]:https://cl.ly/3B0Z3q1k0B1n/Image%202016-09-04%20at%2010.16.01.png
[8]:https://cl.ly/1H0R321J1Z2A/Image%202016-09-04%20at%2010.19.48.png
[9]:https://cl.ly/2b3f0E26231D/Image%202016-09-04%20at%2010.51.48.png
[10]:https://cl.ly/3F261s46182I/Image%202016-09-04%20at%2010.53.55.png

















