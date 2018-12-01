## 环境
> 系统：Windows 10
> 虚拟机：VMware-workstation-full-10.0.2-1744117.1415342309
> https://my.vmware.com/zh/web/vmware/downloads
> Linux：Ubuntu 16.04.5 LTS (Xenial Xerus)
> http://tw.archive.ubuntu.com/ubuntu-cd/xenial/ubuntu-16.04.5-server-amd64.iso
> SSH客户端：SecureCRT 6.5.0 (build 380)
> https://www.vandyke.com/cgi-bin/releases.php?product=securecrt

## 目的
> 在虚拟机上安装Linux系统，然后通过SSH进行“远程”操作。



### 一、安装虚拟机
（1）打开安装程序，点击下一步
 ![pic](.\pic\101.png)

（2）选择接受条款，下一步。
 ![pic](.\pic\102.png)

（3）选择典型后，下一步。
 ![pic](.\pic\103.png)

（4）更改安装目录，下一步。
 ![pic](.\pic\104.png)

（5）不勾选“启动时检查产品更新”选项，下一步。
 ![pic](.\pic\105.png)

（6）不勾选“帮助改善...”，下一步。
 ![pic](.\pic\106.png)

（7）只勾选“桌面”，下一步。
 ![pic](.\pic\107.png)

（8）点击继续进行安装。
 ![pic](.\pic\108.png)

（9）安装中。
 ![pic](.\pic\109.png)

（10）输入密钥。
 ![pic](.\pic\110.png)

（11）完成安装。
 ![pic](.\pic\111.png)



### 二、在虚拟机上安装Linux系统
（1）打开VMware界面
 ![pic](.\pic\201.png)

（2）创建新的虚拟机，选择典型。
 ![pic](.\pic\202.png)

（3）选择需要安装的系统安装文件。下载Ubuntu系统可以在这个地址选择：http://tw.archive.ubuntu.com/ubuntu-cd/
 ![pic](.\pic\203.png)

（4）输入Linux名称、用户名、密码和确认密码。
 ![pic](.\pic\204.png)

（5）输入虚拟机名称、安装目录。
 ![pic](.\pic\205.png)

（6）设置磁盘大小、虚拟磁盘的存储方式。磁盘大小按默认的20G。由于一般不用移动虚拟机，虚拟磁盘存为单个文件就可以了。
 ![pic](.\pic\206.png)

（7）自定义硬件也按照默认就可以了，尝试过把内存1G改为2G也没感觉区别，所以按默认1G就可以了。
 ![pic](.\pic\207.png)

（8）安装Ubuntu中。
 ![pic](.\pic\208.png)

（9）安装完毕。
 ![pic](.\pic\209.png)

（10）在“ubuntu login:”的提示之后输入预设的用户名。然后“Password:”提示就输入预设的密码。注意，密码是不会显示的在屏幕的，所以是盲打。
 ![pic](.\pic\210.png)



### 三、通过ssh进行“远程”操作
（1）安装ssh服务器，使用命令：sudo apt-get install openssh-server
 ![pic](.\pic\301.png)

（2）安装ssh服务器完毕。
 ![pic](.\pic\302.png)

（3）检查ssh服务器是否启动，使用命令：ps  -e|grep ssh
 ![pic](.\pic\303.png)

（4）由于我用的是SecureCRT绿色版，直接打开，第一次运行需要指定SecureCRT的配置数据的目录。
 ![pic](.\pic\304.png)

（5）按Yes，设置SecureCRT为系统默认的Telnet程序。
 ![pic](.\pic\305.png)

（6）先在VMware虚拟机那边使用命令：ifconfig，查看ip（信息的inet addr项）。把ip输入到SecureCRT的“快速连接”设置窗口的主机名。端口默认22，不用改。用户名是wass，选择下方的密码选项，再点击属性按钮，输入密码。确定后，点击“快速连接”窗口的“连接”按钮。
 ![pic](.\pic\306.png)

（7）然后会有“新建主机密钥”的提示，选择“接受并保存”。
 ![pic](.\pic\307.png)

（8）下面界面点击“确定”按钮。
 ![pic](.\pic\308.png)

（9）此时SecureCRT已经可以远程控制Ubuntu。
 ![pic](.\pic\309.png)

（10）选择菜单“选项”，再选择“会话选项”。
 ![pic](.\pic\310.png)

（11）选择“外观”，改变颜色方案为“白/黑”，点击确定。
 ![pic](.\pic\311.png)

（12）噢~色调不错！
 ![pic](.\pic\312.png)



## 参考资料
VMware、Linux（Ubuntu）下载安装
https://blog.csdn.net/qq_37546891/article/details/80482031

ubuntu开启SSH服务
http://www.cnblogs.com/xiazh/archive/2010/08/13/1798844.html

VMware Workstation 显示内部错误
https://jingyan.baidu.com/article/72ee561ab9d72be16138df87.html
