## 环境
> 系统：Windows 10
> 编辑器：Sublime Text 3
> https://www.sublimetext.com/3
> Lua：Lua 5.3.5
> https://sourceforge.net/projects/luabinaries/files/5.3.5/

## 目的
> 通过在Sublime Text设定的Lua编译配置，进行Lua编译。



### 一、安装Sublime Text 
（1）下载软件，portable version，即绿色版
 ![pic](.\pic\101.png)

（2）解压后，移到自选目录下，例如：D:\software\Sublime Text Build 3207 x64，之后直接打开sublime_text.exe则可用



### 二、下载Lua
（1）进入[LuaBinaries页面](http://luabinaries.sourceforge.net/)，选择当前最新版Lua5.3.5
 ![pic](.\pic\201.png)

（2）下载Lua
 ![pic](.\pic\202.png)

（3）解压后，移到自选目录下，例如：D:\software\lua-5.3.5_Win32_bin



### 三、Lua编译配置的两种方式
#### 1、 在Sublim Text新增Lua编译配置
（1）打开Sublime Text，选择菜单Tools >> Build System >> New Build System...

（2）把以下内容复制刚打开的Sublime Text文本中，
其中的D:/software/lua-5.3.5_Win32_bin/lua53.exe，是刚才下载的Lua编译器文件，
然后保存到默认目录，命名为lua.sublime-build

```
{
    "cmd": ["D:/software/lua-5.3.5_Win32_bin/lua53.exe", "$file"],  
    "file_regex": "^(?:lua:)?[\t ](...*?):([0-9]*):?([0-9]*)",  
    "selector": "source.lua"  
}
```

（3）选择菜单Tools >> Build System >> lua，注意大小写

#### 2、使用Sublime Text自带的Lua编译设置
（1）配置环境变量
 ![pic](.\pic\301.png)

（2）把自定义的Lua编译器目录（D:/software/lua-5.3.5_Win32_bin/）里exe文件进行重命名（去掉53）：
```
lua53.exe	->	lua.exe（注意：此处的修改会影响上一种方式的配置文件）
luac53.exe	->	luac.exe
wlua53.exe	->	wlua.exe
```

（3）选择菜单Tools >> Build System >> Lua，注意大小写



### 四、编译
新建一个Lua文件，命名为test.lua，输入如下：
```
print('1')
```
按F7或Ctrl + B，结果为：
```
1
[Finished in 0.2s]
```



以上简单回顾。

## 参考资料
Sublime Text3配置Lua运行环境
https://www.cnblogs.com/liangjf/p/9030831.html