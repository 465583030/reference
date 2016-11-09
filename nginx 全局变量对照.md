## nginx 全局变量对照

> 请求链接:http://dwz.stamhe.com/index.php?_a=index&_m=show&count=10

> 在openresty中所有这些变量都可以用`ngx.var.xxx`来获取,其中xxx代表下面这些变量

> 在 Nginx 配置中，变量只能存放一种类型的值，因为也只存在一种类型的值，那就是字符串。

> Nginx 配置文件引用变量，需要在变量名前面加一个 $ 符号类似于php

1. `remote_addr` *客户端ip,如：192.168.5.5* 

1. `binary_remote_addr` *客户端ip（二进制)* 

1. `remote_port` *客户端port，如：50472* 

1. `remote_user` *已经经过Auth Basic Module验证的用户名* 

1. `host` *请求主机头字段，否则为服务器名称，如:dwz.stamhe.com* 

1. `request` *用户请求信息，如：GET /?_a=index&_m=show&count=10 HTTP/1.1* 

1. `request_filename` *当前请求的文件的路径名，由root或alias和URI request组合而成，如：/webserver/htdocs/dwz/index.php* 

1. `status` *请求的响应状态码,如:200* 

1. `body_bytes_sent` *响应时送出的body字节数数量。即使连接中断，这个数据也是精确的,如：40* 

1. `content_length` *请求头中的Content-length字段* 

1. `content_type` *请求头中的Content-Type字段* 

1. `http_referer` *引用地址* 

1. `http_user_agent` *客户端agent信息,如：Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11* 

1. `args` *如：_a=index&_m=show&count=10* 

1. `document_uri` *与$uri相同,如：/index.php* 

1. `document_root` *针对当前请求的根路径设置值,如：/webserver/htdocs/dwz* 

1. `hostname` *如：centos53.localdomain* 

1. `http_cookie` *客户端cookie信息* 

1. `cookie_COOKIE` *cookie COOKIE变量的值(具体的某个cookie值)* 

1. `is_args` *如果有$args参数，这个变量等于”?”，否则等于”"，空值，如?* 

1. `query_string` *与$args相同,如：_a=index&_m=show&count=10* 

1. `realpath_root` *如：/webserver/htdocs/dwz* 

1. `request_body` * 记录POST过来的数据信息* 

1. `request_body_file` *客户端请求主体信息的临时文件名* 

1. `request_method` *客户端请求的动作，通常为GET或POST,如：GET* 

1. `request_uri` *包含请求参数的原始URI，不包含主机名，如：”/foo/bar.php?arg=baz”。不能修改* 

1. `scheme` *HTTP方法（如http，https）,如：http* 

1. `uri` *如：/index.php* 

1. `server_protocol` *请求使用的协议，通常是HTTP/1.0或HTTP/1.1，如：HTTP/1.1* 

1. `server_addr` *服务器地址，在完成一次系统调用后可以确定这个值，如：192.168.4.129* 

1. `server_name` *服务器名称，如：dwz.stamhe.com (配置文件指令：server_name)* 

1. `server_port` *请求到达服务器的端口号，如：80* 
