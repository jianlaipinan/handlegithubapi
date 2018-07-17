这是个操作githubzpi的说明
操作github上的库用的是githubapiv3
使用pyhton requests完成
	requests的 get post patch put delete 的几种方法实现主要使用到了get post
代码实现
在ubuntu16.04上
	$ sudo apt install docker.io


将用户添加到的docker组
	$ sudo groupadd docker
	$ sudo usermod -aG docker $USER


重启服务

	$ sudo /etc/init.d/docker restart


然后使用root权限编辑/etc/default/docker:

	$ export http_proxy=http://proxy-shz.intel.com:911/
	$ export HTTP_PROXY=http://proxy-shz.intel.com:911/
	$ export https_proxy=https://proxy-shz.intel.com:912/
	$ export HTTPS_PROXY=https://proxy-shz.intel.com:912/


Then edit /etc/docker/daemon.json with root permission:

	$ {"dns":["10.248.2.5","10.239.27.236","172.17.6.9"]}

重启docker服务
	$ sudo /etc/init.d/docker restart


为docker单独设置代理
	$ sudo mkdir /etc/systemd/system/docker.service.d
	$ sudo vim /etc/systemd/system/docker.service.d/http-proxy.conf
		[Service]
		Environment="HTTP_PROXY=http://proxy-shz.intel.com:911"


重启守护进程
	$ sudo systemctl daemon-reload
查看设置的的docker代理
	$ sudo systemctl show docker --property Environment

clone docker installer
	$ git clone https://github.intel.com/projectacrn/acrn-builder.git
	$ cd acrn_builder
	$ git clone https://github.intel.com/projectacrn/acrn-ebtool
	$ ./docker_install_clearlinux_22530.sh 

报错类型1
Step 7/27 : RUN pip3 install kconfiglib
 ---> Running in 361accec2f2a
Collecting kconfiglib
  Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x7efc595f9908>: Failed to establish a new connection: [Errno 101] Network is unreachable',)': /simple/kconfiglib/

解决方法
	改脚本:docker_install_clearlinux_22530.sh第25行#RUN pip3 install kconfiglib

运行docker脚本
	$ docker images
	$ ~/acrn-builder/docker_run.sh REPOSITORY:TAG

报错类型2
	r$ ./docker_run.sh byang1217/clrdev:22530
Could not load host key: /etc/ssh/ssh_host_rsa_key
Could not load host key: /etc/ssh/ssh_host_dsa_key
Could not load host key: /etc/ssh/ssh_host_ecdsa_key
Could not load host key: /etc/ssh/ssh_host_ed25519_key
sshd: no hostkeys available -- exiting.
解决方法
	$ ssh-keygen -t rsa -c "useremail"
	$ ./docker_install_clearlinux_22530.sh
	$ ./docker_run.sh REPOSITORY:TAG

安装kconfiglib
	$ sudo pip3 install kconfiglib

报错类型
	$sudo pip3 install kconfiglib
Collecting kconfiglib
  Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x7f6b3566b828>: Failed to establish a new connection: [Errno 101] Network is unreachable',)': /simple/kconfiglib/


解决方法
	$ wget https://files.pythonhosted.org/packages/f4/9b/b09ca627e8fae3d286f7b5a05dfc94a2b6db2d5d5cb4971a35bca788e31c/kconfiglib-3.2.0-py2.py3-none-any.whl
	$ sudo pip install kconfiglib-3.2.0.py2.py3-none-any.whl

编译
	$ cd acrn-ebtool
	$ sudo make env_set
	

