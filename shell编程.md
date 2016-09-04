#Shell编程

###shell小技巧
**什么是shell？**

* 命令解析器，帮助人机交互的翻译官！
* windows的桌面也是shell的一种！
![shell][1]
* Linux的shell有哪些呢？
	* `vim /etc/shells` 记录了该linux安装了那些shells
	* B类: sh bash
	* C类: tcsh
	* shell不同，命令提示符不同
	* 几乎所有linux缺省都是bash  (Bourne-again Shell) ，非常适合于一些管理操作
	* 一些比较老的unix，缺省都是sh

###bash提供的常用功能如下：
1. 命令补全
	* 使用Tab键
	* 命令补全、文件名补全（避免敲错命令或文件名）
	* 如果不是唯一的，按两下Tab，全列出来

1. 快捷操作
	* CTRL+C 终止命令
	* CTRL+A 光标到行首
	* CTRL+E 光标到行尾
	* CTRL+U 剪切光标前内容
	* CTRL+K 剪切光标后内容
	* CTRL+Y 粘贴剪切的内容
	* CTRL+L 清理屏幕
	* CTRL+D 注销登陆相当于exit和logout或者保存
	* CTRL+Z 将进程在后台挂起	`bg` `fg`
	
1. 命令历史
	* `history`		列出所有的命令（默认最多保存条数1000）
	* `!序号	`	执行历史中第几个命令		
	* `!命令`		执行最近的这条命令
	* 按向上(或向下)箭头，翻出历史记录
	
1. 命令别名
	* 什么是别名？（类似快捷命令）	
		* 命令：`alias`（显示当前可用别名命令）
		* `ls`为什么可以显示颜色？因为是`ls --color=tty`的别名
		* 可以看到 `ll` 是`ls -l --color=tty`的别名
	* 添加一个别名（临时）：
		* `alias copy=cp` 就可以用`copy`替代`cp`来复制文件
	* 还可以带参数：
		* `alias drm="rm -rf"`
	* 删除别名：
		* `unalias copy`
	* 别名永久生效：在用户宿主目录 ~/.bashrc 文件中添加别名信息如：*alias vi=vim*。重启生效或者`source  ~/.bashrc`及时生效
	
1. 输入输出重定向
	1. Shell对于每个进程预先定义了3个文件描述符
		* 0 标准输入  STDIN	键盘
		* 1 标准输出  STDOUT	显示器
		* 2 标准错误输出 STDERR
	1. 重定向，就是改变这个标准设备，不用键盘输入，不用显示器输出
	1. 输出重定向 `>` or `>>`
		* 例子：
			* `echo hello` 直接显示到了显示器
			* `echo hello>test.txt` 将输出重定向到了test.txt
			* `ls -l /tmp>files.txt`将输出重定向到了files.txt
			* `more` 查看文件内容
			* `find /website -size +204800 >/backup/100M+.file.list`把/website下大于100M的文件列表
	1. 输入重定向（不从键盘输入内容）
		* 例如：
			* `wall < /test/msg` 从一个文件读取内容发广播,这样，就可以用计划任务，把一年的节日祝福语写上，到时自动发送.
	
	1. 错误输出重定向
		* `2>`or`2>>`**描述字和符号间不许有空格**
		* 例子：
			* `cp -R /usr /backup/use 2>>/bak.error`将错误信息，定向到一个文件中.自动备份 通常用计划任务在凌晨自动执行
			* `ls /aaaaaa 2>ls.err`	如果`/aaaaa`这个目录不存在，则将错误信息保存到ls.err中

		* 这里面的2，就是前面讲的 Shell对于每个进程预先定义了3个文件描述字
		* 0和1都可以省略，2不能省略了

1. 管道连接符
	* 将一个命令的输出，传送给另一个命令，作为另一个命令的输入，可以连接多个命令.
	* usrage：`命令1|命令2|命令3...` 命令直接用`|`分隔
	* 例子：
		* `ls -l /etc | more` 文件太多，一次看不完，用more来查看下一页：空格或f 下一行：回车 退出:q 或Q
		* `ls -l /etc | grep init` 只显示init相关的行
		* `ls -l /etc | grep init | wc -l` 查看init相关的有多少行，也就是包含init的文件有多少个
		* `who | grep root` 只显示root的登录信息
		* `wc -l` 统计文件有多少行
		* `who | grep root | wc -l` 查看root 用户登录了几次

1. 命令连接符
	* `;`不管执行是否成功，多个命令依次执行
		* 例: `pwd ; ls ; date`

	* `&&` 前面执行成功，才执行后面的命令，如果第一个失败，则不执行第二个
		* `write user1 < /home/jack/love.txt && rm /home/jack/love.txt` 消息发成功，就删除
		* `ls && pwd`  `ls`成功后才会执行`pwd`命令

	* `||`	前面执行失败，才执行后面的命令
		* `write mary < /home/jack/love.txt || mail mary< /home/jack/love.txt`  情书发失败，则发邮件
	
	* **``** 命令替换符
		* 将一个命令的输出作为另一个命令的参数
		* 命令1 `命令2`，命令1的参数，是命令2的执行结果
		* ls -l `which touch` 找到touch命令的路径，然后用ls查看属性
	    * 看起来有点类似管道，不过顺序相反，会先执行后面的





[1]:https://cl.ly/022F2l2V0V15/Image%202016-09-04%20at%2011.59.05.png