一、Linux常用命令

	1、init 0   关机 

	2、init 6   重启   

	3、ls  、 ls -l  、  ll 列出出当前目录下的文件 

	4、cd  切换目录

	5、pwd            查看当前路径

	7、cd -             切换最近使用过的两个目录

	8、ctrl+c      中断当前程序

	9、ctrl+l  / (clear)   清屏

	10、ip addr  /  ifconfig    查看网卡信息

	11、ping 127.0.0.1   看网络是否通畅


二、Linux shell命令技巧
	1.tab补全
		命令+（1次）tab
		命令+（2次）tab

	2、上下键盘    查看最近的历史命令

	3.history
		查看命令历史

		!22
		调用历史中编号为22的命令

	4.!h
		调用历史中最后一次以h开头的命令

	获取帮助:
		
		ls --help

		man ls  


三、Linux 创建用户修改密码
	


	1.添加用户
		useradd zhangsan

	2.设置密码
		passwd zhangsan

	3.删除用户
		
		userdel -rf zhangsan

		-r：递归的删除目录下面文件以及子目录下文件。



四、文件管理


	1.创建文件

		touch file1

	2.删除文件
		
		rm -rf file11

		-r：递归的删除目录下面文件以及子目录下文件。
		-f：强制删除，忽略不存在的文件，从不给出提示		


	3.修改文件名
		mv  file1 file11

	4.查看文件内容

		cat file1

	5.复制文件

		cp file2 file22

	6.移动文件

		mv file1 file11

	7.编辑文件

		vi file1

	8.批量创建文件

		touch file{1..10}

		rm -rf file{1..10}


	9.查看文件前3行

		| 把前面的执行结构给后端

		cat file1 | head -3

	10.查看文件后3行

		cat file1 | tail -3

	11、liunx服务器上面查找文件
	
		1)find
			find / -name  httpd.conf

			find 目录 -name  文件名
 
		2)updatedb   查找速度快

			1、建立一个小型数据库    updatedb

			2、再数据库里面搜索       locate httpd.conf


		    
			yum install mlocate -y

			mlocate是新型的locate比updatedb速度更快。


	12、查找文件里面内容   找到httpd.conf 里面有listen

				
		cat httpd.conf | grep listen

		cat httpd.conf | grep -ignore listen   /  cat httpd.conf | grep -i listen  忽略大小写

			
	13、查找文件里面内容  vi搜索 

		vi  httpd.conf

		输入 /Listen    搜索Listen     N下一个



五、Linux 目录管理

	1.创建目录
		mkdir dir1 dir2 dir3

	2.删除目录
		rm -rf dir1 dir2

		-r：递归的删除目录下面文件以及子目录下文件。

		-f：强制删除，忽略不存在的文件，从不给出提示


		rm -rf  dir*      以dir开头的所有文件删除


	3.重命名目录或移动目录

		mv dir1 dir11

	
	4.查看目录

		ls  / ll

	5.递归创建目录

		mkdir -p a/b/c/d/e/f/g

	6.递归查看目录
		tree a

	7、复制目录

		 cp  -rf  wwwroot/ mywwwroot/	

	8、tree命令不存在的话需要安装
			
	yum install tree -y


六 、Linux 打包压缩  别名管理

		
	一、打包压缩

		1、zip压缩包
			1.制作
			zip -r public.zip public

			-r 递归 表示将指定的目录下的所有子目录以及文件一起处理

		2.解压
			unzip public.zip

			unzip public.zip -d dir             

		3.查看
			nzip -l public.zip

		4、安装zip减压软件

			yum install -y unzip zip


		2、gz压缩包:  (源代码压缩)
		Linux下最常用的打包程序就是tar了，使用tar程序打出来的包我们常称为tar包，tar包文件的命令通常都是以.tar结尾的。生成tar包后，就可以用其它的程序来进行压缩了，所以首先就来讲讲tar命令的基本用法

			1.制作gz包
				tar czvf public.tar.gz public

			2.解压gz包
				tar xzvf public.tar.gz

			3.查看gz包
				tar tf public.tar.gz

		4、制作tar包

				tar cvf wwwroot.tar wwwroot         仅打包，不压缩！

		5、减压tar包

				 tar xvf wwwroot.tar        


		参数：

		特别注意，在参数的下达中， c/x/t 仅能存在一个！不可同时存在！因为不可能同时压缩与解压缩。


			-c  ：建立一个压缩档案的参数指令(create 的意思)
			-x  ：解开一个压缩档案的参数指令！
			-t  ：查看 tarfile 里面的档案！

				-z  ：是否同时具有 gzip 的属性？亦即是否需要用 gzip 压缩？
			-j  ：是否同时具有 bzip2 的属性？亦即是否需要用 bzip2 压缩？
			-v  ：压缩的过程中显示档案！这个常用，但不建议用在背景执行过程！
			-f  ：使用档名，请留意，在 f 之后要立即接档名喔！不要再加参数！
			
		3、xz压缩包:  	

		对于xz这个压缩相信很多人陌生，但xz是绝大数linux默认就带的一个压缩工具，xz格式比7z还要小。

		1.制作
			tar  cvf xxx.tar xxx  // 这样创建xxx.tar文件先，
			xz  xxx.tar        //将 xxx.tar压缩成为 xxx.tar.xz	   删除原来的tar包
			xz  -k xxx.tar       //将 xxx.tar压缩成为 xxx.tar.xz	  保留原来的tar包


		2.解压
			xz   -d  ***.tar.xz     //先解压xz   删除原来的xz包
			   
			xz  -dk  ***.tar.xz     //先解压xz  保留原来的xz包

			tar  -xvf  ***.tar    //再解压tar

		2.查看

			xz  -l  ***.tar.xz     //先解压xz
			
	二、别名管理
		1.添加别名
		
			alias chttp='cat /etc/httpd/conf/httpd.conf'
				
			chttp

		2.删除别名

			unalias chttp

		3.查看别名
			alias




六 、用户管理、用户权限管理

	用户管理

		1.添加用户
		
			useradd lisi

		2.设置密码

			passwd lisi

			
		3.删除用户

			userdel -r lisi

			-r：递归的删除目录下面文件以及子目录下文件。
			备注：删除用户的时候用户组被删除

		4.查看用户

			id user

		5.把用户加入组
					
			gpasswd -a testuser root

		把用户testuser加入到root组，加入组后testuser获取到user组及root组所有权限

		6、把用户移出租
			gpasswd -d testuser root

		
	用户权限管理



		drwxr-xr-x.   2 root root    6 4月  11 2018 mnt

		rwx   当前用户对mnt有读写执行权限      u

		r-x   当前用户的组对mnt文件有读和执行  g

		r-x   其他用户对mnt也具有读和执行      o


	权限:
		r 读
		w 写
		x 执行


	用户:
		所有者   user   u
		所属组   group  g
		其他用户 other  o
		所有用户 all     a            u+g+o=a(表示所有人) 


	目录的rwx
		r  查看目录里面的文件(4)
		w 在目录里创建或删除文件(2)
		x  切换进目录(1)

	文件的rwx

		r 查看文件内容
		w 在文件里写内容
		x 执行该文件(文件不是普通文件，是程序或脚本)


	chmod权限分配
		+增加权限         -删除权限

		chmod u+x my.sh   给当前用户分配执行my.sh的权限

		chmod o+r,o+w file.txt    给其他用户分配对file.txt的读写权限

		chmod o+r,o+w,o+x mnt/     给所有其他用户分配对mnt目录的进入、读取、写入权限

		chmod -R o+r,o+w,o+x mnt/       修改目录下的所有文件的权限为可读、可修改、可执行

		chmod 755 file

		chmod -R 777 wwwroot/  修改目录下的所有文件的权限为可读、可修改、可执行
	

	ACL权限控制


		[root@localhost /]# setfacl -m u:zhangsan:rx opt/
		[root@localhost /]# setfacl -m u:lisi:rwx opt/

		1.查看opt拥有的acl权限 
			getfacl opt/        

		2.设置opt的acl权限
			setfacl -m u:zhangsan:rwx opt/

		3.删除opt的user1拥有的acl权限 
			setfacl -x u:zhangsan opt/          -x删除权限

		4.删除opt上所设置过的所有acl权限 
			setfacl -b opt/

	用户权限管理visudo	

		sbin下面的命令执行权限

		1.设置
		输入： visudo   

			编辑    %zhangsan localhost=/usr/sbin/useradd
				%zhangsan localhost=/usr/sbin/userdel

		2.使用  普通用户家sudo

			sudo useradd wangwu
			sudo userdel wangwu

	查找命令所在目录

		which useradd


七 、rpm软件安装卸载

	rpm命令安装卸载查找rpm包


		1、挂载光盘

			1、mount dev/cdrom /media  挂载
			2、df  查看光盘是否挂载
			3、卸载umount /media

		2、rpm安装

			rpm -ivh rpm软件包

		3、rpm卸载软件

			rpm -e net-tools           net-tools表示要卸载的软件包
		4、查看rpm软件包的安装位置 / 软件包是否安装


			rpm -ql net-tools

	Yum安装rpm 卸载rpm  查看rpm包


		1、yum安装rpm包

			yum install -y net-tools              包括 netstat ifconfig等命令
			yum install -y unzip zip               zip压缩减压
			yum install -y mlocate                 updatedb
			yum install -y wget                    下载文件包
			yum -y install psmisc                   pstree | grep httpd   查看进程    pstree -p   显示进程以及子进程

		2、yum卸载rpm包

			yum -y remove wget
			
			
		3.yum搜索npm包

			yum search 名称

			
		4.yum查看rpm包

			yum list 

			yum list | grep httpd

			yum list updates  列出所有可更新的软件包

			yum list installed   列出所有已安装的软件包

		5.yum显示rpm包信息

			yum info package1
			如：
			yum info httpd   
			yum info zip
			yum info unzip


		6、yum 安装Apache 

			yum -y install httpd                  service httpd start   安装启动apache

			1、启动apache
			2、关闭防火墙                     systemctl stop firewalld

	yum的主配置文件 etc/yum.conf 



	yum的仓库配置文件 /etc/yum.repo.d/*.repo



	Yum 安装Nginx：
		1、安装nginx源
			sudo rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
		2、查看Nginx源是否配置成功　
			通过yum search nginx看看是否已经添加源成功。如果成功则执行下列命令安装Nginx。
			或者 npm info nginx也可以看看nginx源是否添加成功
		3、安装Nginx 
			sudo yum install -y nginx
		3、启动Nginx并设置开机自动运行 
			sudo systemctl start nginx.service
			sudo systemctl enable nginx.service

		
		防火墙配置：http://bbs.itying.com/topic/5bd5d4460e525017c449479a

八、源代码包的安装


	1、先安装源代码编译的软件gcc，make，openssl 如下：

		yum install -y gcc make gcc-c++ openssl-devel

		检查系统中是否已经安装 gcc：

		rpm -qa | grep gcc  /  rpm -ql  gcc  


	2、编译安装源代码包
		1.生成编译配置文件(Makefile)
		2.开始编译(make)
		3.开始安装(make install)

		安装httpd-2.2.9.tar.gz源代码:
			1)减压并cd到对应目录
			2)./configure --prefix=/usr/local/nodejs              安装路径设置为/usr/local/apache
			3)  make   /  make -j4
			4)  make install


	3、删除源代码包


		1、结束当前源代码进程
		2、删除源代码


		如：

			1、结束进程
				pstree|grep httpd
				pkill httpd

			2、删除源代码
			cd  /usr/local/
			直接删除源代码   rm -rf apache/

	4、linux下源代码安装nodejs:
		1、 下载nodejs源码包
		2、 减压到usr/local/nodejs 目录
		3、 ./configure
		4、 make   /  make -j4
		5、 make install

	
九、二进制包安装nodejs


	二进制包里面包括了已经经过编译，可以马上运行的程序,所以二进制包的安装只需要丢到一个目录里面就可以了。



	去官网下载nodejs二进制包并减压：
		wget https://nodejs.org/dist/v8.9.3/node-v8.9.3-linux-x64.tar.xz

		xz -d node-v8.9.3-linux-x64.tar.xz
		tar -xvf node-v8.9.3-linux-x64.tar

		mv node-v8.9.3-linux-x64 /usr/local/nodejs


	配置环境变量
		vi /etc/profile

	最后面添加：
		export NODE_HOME=/usr/local/nodejs/bin
		export PATH=$NODE_HOME:$PATH

	:wq保存，然后运行
		source /etc/profile

	可以用node -v和npm -v来检查下： 
		node -v

	查看环境变量是否生效
		echo $PATH



十、 Linux 内存、cpu、进程、端口、硬盘管理  


	 top命令 查看内存 cpu 进程 以及服务器负载


		1、top命令的第一行：

			top - 15:31:47 up  9:30,  3 users,  load average: 0.00, 0.02, 0.05

			依次对应：系统当前时间 up 系统到目前为止i运行的时间， 当前登陆系统的用户数量， load average后面的三个数字分别表示距离现在一分钟，五分钟，十五分钟的负载情况。

		2、top命令的第二行：

			Tasks: 133 total,   1 running, 132 sleeping,   0 stopped,   0 zombie

			依次对应：tasks表示任务（进程），133 total则表示现在有133 个进程，其中处于运行中的有1个，132 个在休眠（挂起），stopped状态即停止的进程数为0，zombie状态即僵尸的进程数为0个。

		3、top命令的第三行，cpu状态：
		     
			%Cpu(s):  0.2 us,  0.4 sy,  0.0 ni, 99.3 id,  0.0 wa,  0.0 hi,  0.1 si,  0.0 st
		 
			只看空闲就可以了：cpu空闲率为99.3%

		4、top命令的第四行，内存状态：
     
			KiB Mem :  2897496 total,  1995628 free,   191852 used,   710016 buff/cache
			 
			总内存:2.76g  空闲：1995628/1024/1024=1.9g   已经使用0.18g   缓存区内存0.67g  

			缓冲区是从主内存中特地预留出的内存，用来存放特定的一些信息，例如从磁盘中取得的文件表，程序正在读取的内容等等



	 uptime命令

		1.服务器工作时间
		2.在线用户
		3.平均负载  一分钟，五分钟，十五分钟的负载情况


	看当前登录的账户who、查看最新操作电脑的用户last
		who命令:
			显示当前正在系统中的所有用户名字，使用终端设备号，注册时间。 
		whoami :
			显示出当前终端上使用的用户。 
		last:
			last作用是显示近期用户或终端的登录情况


		

	查看进程关闭进程


		1、查看进程
		
			pstree        查看进程树
			pstree -ap     显示所有信息

			pstree | grep httpd

			pstree -ap | grep httpd

			ps -au
			ps -au |grep httpd
			ps -aux


			ps 中aux的含义:

			显示现行终端机下的所有程序，包括其他用户的程序（a）
			以用户为主的格式来显示程序状况。 （x）
			显示所有程序，不以终端机来区分（u）

		2、关闭进程

			pkill httpd             pkill进程的名字

			kill 2245               kill进程号

			kill -9 1234             kill -9进程号  强制杀死
			       

			kill：执行kill命令，系统会发送一个SIGTERM信号给对应的程序。当程序接收到该signal信号后，将会发生以下事情：
			程序立刻停止
			当程序释放相应资源后再停止
			程序可能仍然继续运行
			大部分程序接收到SIGTERM信号后，会先释放自己的资源，然后再停止。但是也有程序可能接收信号后，做一些其他的事情（如果程序正在等待IO，可能就不会立马做出响应，我在使用wkhtmltopdf转pdf的项目中遇到这现象），也就是说，SIGTERM多半是会被阻塞的。

			kill -9:  kill -9命令，系统给对应程序发送的信号是SIGKILL，即exit。exit信号不会被系统阻塞，所以kill -9能顺利杀掉进程。

	查看端口

		netstat -tunpl |grep httpd



	查看硬盘信息：


		df命令作用是列出文件系统的整体磁盘空间使用情况。可以用来查看磁盘已被使用多少空间和还剩余多少空间。
		


		df 

		df -h  以人们易读的方式显示，总共多少g用了多少g

		df /home   查看该文件夹所在磁盘的使用情况



			
十一、Linux systemctl管理服务

	1、二进制安装nodejs 

		1、减压到对应的目录usr/local/nodejs

		2、配置环境变量
		
			配置环境变量
				vi /etc/profile

			最后面添加：
				export NODE_HOME=/usr/local/nodejs/bin
				export PATH=$NODE_HOME:$PATH

			:wq保存，然后运行
				source /etc/profile

			可以用node -v和npm -v来检查下： 
				node -v

	2、yum安装httpd

		yum install -y httpd

		systemctl start httpd

	3、systemctl管理服务


		
		1、启动服务：systemctl start httpd

		2、关闭服务：systemctl stop httpd

		3、重启服务：systemctl restart httpd


		3、查看一个服务的状态：systemctl status httpd

		4、查看一个服务是否在运行：systemctl is-active httpd

		5、查看当前已经运行的服务：systemctl list-units -t service

		6、列出所有服务：  systemctl list-units -at service       注意顺序 

		8.设置开机自启动：	systemctl enable httpd

		9.停止开机自启动：	systemctl disable httpd

		10、列出所有自启动服务：

			systemctl list-unit-files|grep enabled
			systemctl list-unit-files|grep disabled
			systemctl list-unit-files|grep disabled | grep httpd

		使指定服务从新加载配置：systemctl reload httpd    



十二、Firewalld防火墙和SELinux防火墙的设置


Firewalld防火墙的设置

	1、firewalld的基本使用:
		启动： systemctl start firewalld
		关闭： systemctl stop firewalld
		查看状态： systemctl status firewalld
		开机禁用 ： systemctl disable firewalld
		开机启用 ： systemctl enable firewalld

	2、firewall-cmd的基本使用:
		那怎么开启一个端口呢:
			firewall-cmd --zone=public --add-port=80/tcp --permanent （–permanent永久生效，没有此参数重启后失效）
		重新载入:
			firewall-cmd --reload       修改firewall-cmd配置后必须重启
		查看:
			firewall-cmd --zone= public --query-port=80/tcp
		删除:
			firewall-cmd --zone= public --remove-port=80/tcp --permanent

		查看所有打开的端口：
			firewall-cmd --zone=public --list-ports
SELinux防火墙的设置

		修改/etc/selinux/config 文件
		将SELINUX=enforcing改为SELINUX=disabled
