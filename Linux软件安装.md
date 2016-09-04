#软件包管理
>Linux两大系列的区别——软件包管理不同：Redhat系列rpm/yum,Debian系列apt-get/dpkg

>一般软件在官网都有安装教程

###软件包分类：
1. 二进制（rpm）包
	* 特点: 安装速度快		简易
	* 缺点: 自定义性差		依赖性
2. 源码包
	* **由软件开发源码组成，安装时需要编译工具如gcc、gcc-c++等**
	* 优点：开源、定制
	* 缺点：安装时间长，一旦报错，不易解决
3. 脚本安装包
	* shell脚本编写的安装包，实际内容依然是两种基本的安装方式，安装过程可以交互。
	
###二进制(rpm)包的管理 
#####（一）rpm管理工具 (次要)
1. 软件包命名
	* 包名-版本号-发布次数-适合linux系统-硬件平台.rpm
	* 包全名：操作没有安装的软件包，软件包使用包全名
	* 包	名：操作的是已经安装的软件，软件包使用包名

2. 安装及升级
	* `rpm  -ivh  包全名`（绝对路径，一般在光盘的软件包目录中）
		* -i 安装		
		* -v 显示详细信息		
		* -h 显示进度
	* `rpm  -Uvh  包全名	` 提前下载好高版本的软件包
		* -U  升级
3. 卸载
	* `rpm  -e  包名` 如有依赖卸载失败
		* `--nodeps`	不检查依赖性，强卸！
4. 查询
	* `rpm  -q  包名	`	查询包是否安装
	* `rpm  -qa  | grep  httpd` 		显示所有安装包
	* `rpm  -qi  包名`	查询包的信息		`-p`  未安装包
	* `rpm  -qip  包全名`	查询没有安装包的信息
			`-i`	information
	* `rpm  -ql  包名`	查询包中文件的安装位置
	* `rpm  -qlp  包全名`	查询没有安装的包，打算安装位置
				-l	list
	* `rpm  -qf  系统文件名`		查询系统文件属于哪个包
		
##### （二）yum在线管理工具 (重点,主要)

1. **yum相对于rpm管理工具的优势：**

	* yum可以在线安装升级，使用CentOS提供的网络站点下载所需软件包。
	* yum可以自动解除软件包之间的依赖关系，方便安装卸载。

1. 安装 install
	
	* `yum -y install 包名`  `-y` 安装过程自动回答`yes`

1. 卸载 remove
	
	* `yum -y remove 包名`

1. 升级 update
	
	* `yum -y update 包名`
	
1. 查看
	* `yum list` 查询所有可以安装的包
	* `yum info 包名`
	
1. 如果没有网络，yum管理工具可以将多媒体软件库作为yum源（池），继续完成软件管理。

	* yum默认将/etc/yum.repo.d/CentOS-base.repo文件作为第一yum源配置文件，此文件描述了网络站点的下载地址，如果此文件存在，则继续上网安装，断网时会安装失败。需要将yum源切换为光盘的多媒体文件中去。
	
	* 将光盘作为yum源（以下步骤顺序部分先后）：
		1. 修改yum源配置文件
			* `mv /etc/yum.repo.d/CentOS-Base.repo /root/` 剪切或改名皆可，只要在原位置无同名配置文件即可。
		2. 挂载使用光盘
			* `mount /dev/cdrom  /mnt/cdrom`

		3. 修改Media配置文件，指定yum源为挂载点
			* `vi  /etc/yum.repos.d/CentOS-Media.repo`
			* `baseurl=file:///mnt/cdrom/`	指定yum源位置
			* `enabled=1`		yum源文件生效
			* `gpgcheck=1`	rpm验证不生效
			
###源码包安装

1. 上传软件包
	* 使用winscp,xshell等工具远程连接Linux，上传所需软件包

2. 安装（重点）

	1. 解压 `tar	-zxvf	包文件`
	
	2. `cd 解压目录` 进入到解压文件目录
	
	3. 查看安装文档
	
		* INSTALL README
		
	4. ./configure
		* 例如：`./configure  --prefix=/usr/local/apache2`
		* 功能作用：
			1. 检测系统环境，生成Makefile
			2. 定义软件选项
				* `--prefix` 指定软件安装目录
		
	5. 编译
		* `make`
	
	6. 安装
		make install
		
	7. 报错判断
		* 安装过程是否停止
		* 停止处是否出现 `error  warning  no ` 等错误报警

3. 启动
	
	* 源码包的启动脚本大多存在于安装目录下
	* `/usr/local/apache2/bin/apachectl  start`
	
4. 卸载

	* `rm  -rf /usr/local/apache2/` 直接删除安装目录




###脚本安装

1. 有提示一步步的跟着执行。

















