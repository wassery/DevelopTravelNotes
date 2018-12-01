## 环境
> 系统：Windows 10 & Ubuntu 16.04.5 LTS
> 引擎：Unity 2017.2.1f1
> 工具：Cache Server v6.1.2

## 目的
> 使用Cache Server制作一个简单实例。

## Windows
（1）安装Unity Cache Server，首先打开Windows命令行工具，然后使用命令：npm install unity-cache-server -g
 ![pic](.\pic\101.png)

（2）安装完成后，启动Unity Cache Server，使用命令：unity-cache-server
 ![pic](.\pic\102.png)
可以看到版本号（v6.1.2）和默认端口（8126）。

（3）打开Unity，选择菜单项Edit > Preferences...
 ![pic](.\pic\103.png)

（4）在Preferences窗口，选择Cache Server选项卡，选择Cache Server模式，改为Remote。
 ![pic](.\pic\104.png)

（5）弹出是否删除原数据，删！（按个人选择...）
 ![pic](.\pic\105.png)

（6）需要查看IP地址，回到命令行，使用命令：ipconfig
 ![pic](.\pic\106.png)

（7）把查到的IP地址，输入到“IP Address”。输入后，焦点尚在输入框时，注意需要回车，才有效，然后再点击Check Connection。如果显示Connection successful，就成功了。
 ![pic](.\pic\107.png)

（8）在Build Settings窗口切换平台，第一次切换会进行数据生成及缓存，再度切换回到缓存过的平台，就会有直接切换，而不再需要生成数据。
 ![pic](.\pic\108.png)

（9）每次切换平台，会在命令行窗口看到耗时。
 ![pic](.\pic\109.png)



## Linux

（1）安装Unity Cache Server，使用命令：npm install unity-cache-server -g
 ![pic](.\pic\201.png)

（2）安装完成后，启动Unity Cache Server，使用命令：unity-cache-server
 ![pic](.\pic\202.png)
可以看到版本号（v6.1.2）和默认端口（8126）。

（3）打开Unity，选择菜单项Edit > Preferences...
 ![pic](.\pic\203.png)

（4）在Preferences窗口，选择Cache Server选项卡，选择Cache Server模式，改为Remote。
 ![pic](.\pic\204.png)

（5）弹出是否删除原数据，删！（按个人选择...）
 ![pic](.\pic\205.png)

（6）需要查看IP地址，回到Linux，使用命令：ifconfig
 ![pic](.\pic\206.png)

（7）把查到的IP地址，输入到“IP Address”。输入后，焦点尚在输入框时，注意需要回车，才有效，然后再点击Check Connection。如果显示Connection successful，就成功了。
 ![pic](.\pic\207.png)

（8）在Build Settings窗口切换平台，第一次切换会进行数据生成及缓存，再度切换回到缓存过的平台，就会有直接切换，而不再需要生成数据。
 ![pic](.\pic\208.png)

（9）每次切换平台，会在Linux看到耗时。
 ![pic](.\pic\209.png)



以上简单回顾。

## 参考资料

Unity Cache Server README.md
https://github.com/Unity-Technologies/unity-cache-server