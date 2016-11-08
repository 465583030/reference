#curl 常用命令
>### 1. curl可以通过网络将信息传递给服务器或者从服务器获取数据，它支持http,https,ftp,ftps,telnet等多种协议，常被用来抓取网页和监控Web服务器状态。
>### 2. http请求地址的url要使用""括起来
>### 3. wget是另外一个类似于curl，可以用来获取URL的命令行工具。并且wget也一样允许你使用一个自定义的HTTP头。
>### 4.   官网[tutorial](https://curl.haxx.se/docs/manual.html)

1. 下载单个文件，默认将输出打印到标准输出中(STDOUT)中

	`curl https://www.example.com`
	
2. 通过-o/-O选项保存下载的文件到指定的文件中：

	* `-o`：将文件保存为命令行中指定的文件名的文件中

		`curl -o yourname.html http://www.example.com/index.html`
		`curl http://www.example.com/index.html >> yourname.html`*效果同上*
	* `-O`：使用URL中默认的文件名保存文件到本地

		`curl -O http://www.example.com/index.html`*当前目录下生成一个index.html的文件*
		
3. 同时请求多个文件
	
	`curl -O url1 -O url2`
	
4. 通过-L选项进行重定向

	>默认情况下CURL不会发送HTTP Location headers(重定向).当一个url被重定向到另一个url时，HTTP响应头中会有一个 `Loaction xxxx` 头信息，然后客户端将请求重定向到新的地址上。

	`curl -L http://www.example.com`
	
5. 保存与使用网站cookie信息
	
	* 将网站的cookies信息保存到cookies文件中

		`curl -c /tmp/cookies http://www.baidu.com`*cookies保存到/tmp/cookies文件，只有cookie信息*
	
		`curl -D /tmp/cookies http://www.example.com/login.php`*保存所有请求头信息到/tmp/cookies文件*
		
	* 使用保存的cookie信息

		`curl -b /tmp/cookies http://www.example.com/index.php `  *从文件中读取cookies*
		`curl -b "key1=val1;key2=val2;" http://www.baidu.com` *发送cookies文本*
		
6. 传递请求数据
	
	>默认curl使用GET方式请求数据，这种方式下直接通过URL传递数据
可以通过 --data/-d 方式指定使用POST方式传递数据

		
	* GET
		
		`curl https://www.example.com/?username=xxx&age=24`
		`curl -G -d "name=value&name2=value2" http://www.baidu.com`
		
	* POST

		`curl --data "username=xxxx&passwd=123456" http://www.example.com/login/php`
		
		`curl --data-urlencode "value 1" http://hostname.com` 
		
	>除了使用GET和POST协议之外，还可以通过-X 选项指定其他协议
	
	* PUT / DELETE	

		`curl -X DELETE http://www.example.com`
		
	* 上传文件

		`curl --form "fileupload=@filename.txt" http://hostname/resource`
	
	
	
7. CURL授权

	* 在访问需要授权的页面时，可通过-u选项提供用户名和密码进行授权

		`curl -u username:password URL`	
		
		>通常的做法是在命令行只输入用户名，之后会提示输入密码，这样可以保证在查看历史记录时不会将密码泄露
		
		`curl -u username URL`	
		
8. 查看完整的请求信息，包括请求头header

	* 通过使用 `-v`和`-trace` 参数获取更多请求信息

		`curl -v http://www.baidu.com`
		
9. 为CURL设置代理 `-x`

	`curl -x proxyserver.test.com:3128 http://www.example.com`
	
10. 设置http请求头信息 `-H`或`--header`

	>在一些个例中，或许你想要在一个HTTP请求中覆盖掉默认的HTTP头或者添加一个新的自定义头部字段。例如，你或许想要重写“HOST”字段来测试一个负载均衡，或者通过重写"User-Agent"字符串来假冒特定浏览器以解决一些访问限制的问题。
	
	`curl -A "Mozilla/5.0 Firefox/21.0" http://www.baidu.com` *设置http请求头User-Agent*
	`curl -e "http://pachong.org/" http://www.baidu.com`*设置http请求头Referer*
	`curl -H "Connection:keep-alive \n User-Agent: Mozilla/5.0"  http://www.aiezu.com`
	`curl -H 'Host: 157.166.226.25' -H 'Accept-Language: es' -H 'Cookie: ID=1234' http://cnn.com`
	
	>对于"User-Agent", "Cookie", "Host"这类标准的HTTP头部字段，通常会有另外一种设置方法。curl命令提供了特定的选项来对这些头部字段进行设置:


	`-A (or --user-agent)` *设置 "User-Agent" 字段* 
	
	`-b (or --cookie)`*设置 "Cookie" 字段*
	
	`-e (or --referer)`*设置 "Referer" 字段*
11. 接收http响应头

	`curl -I http://www.aiezu.com` *仅仅返回header* 
	
	`curl -D /tmp/header http://www.aiezu.com`*将http header保存到/tmp/header文件*
		
		
	
	
	
	
	
	