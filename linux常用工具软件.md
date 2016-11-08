#Linux常用工具软件

###SSH  
1. [SSH Tutorial for Linux][1]
1. [SSH Tutorial for Windows][1]
1. 安装ssh
	* Centos: `yum install openssh-server openssh-clients`
	* Ubuntu: `apt-get install openssh-server openssh-clients`
	* MacOS:  `brew install openssh-server openssh-clients`
2. `ssh-keygen -t rsa`
3. `ssh <username>@<hostname>`
4. `ssh-copy-id yourname@yourmachine`









[1]:https://support.suso.com/supki/SSH_Tutorial_for_Linux
[1]:https://support.suso.com/supki/SSH_Tutorial_for_Windows