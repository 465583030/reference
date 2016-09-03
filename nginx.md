#nginx 参考
#### 常用命令
1. 帮助命令`nginx地址 -h` 
	![nginx -h][1]
2. 启动
	* `nginx地址 -c nginx配置文件地址`
	* 默认情况下为`/usr/local/nginx/sbin/nginx  -c /usr/local/nginx/conf/nginx.conf`
3. 查看进程号：
	* `ps -ef | grep nginx`
4. 停止：
	* 从容停止：`kill -QUIT $主进程号`
	* 快速停止：`kill -TERM $主进程号` or `kill -INT $主进程号`
	* 强制停止：`pkill -9 nginx`
5. 重启：**修改配置文件必须重启生效！**
	* `nginx地址 -t`*验证nginx配置文件语法是否正确*
	* `nginx地址 -s reload`
	* `kill -HUP $主进程号`
6. 信号控制：
	
	
	







[1]:https://cl.ly/193A3C041l2a/Image%202016-09-03%20at%2023.50.03.png