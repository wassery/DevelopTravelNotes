## 环境
> 系统：Windows 10
> 引擎：Unity 2017.2.1f1
> 工具：DOTween Pro v1.0.075

## 目的
> 使用DOTween制作一个简单实例。

（1）首先把场景布局如此
 ![pic](.\pic\1.png)

（2）准备导入插件
 ![pic](.\pic\2.png)

（3）选择导入DOTween
 ![pic](.\pic\3.png)

（4）选择All后，点击Import
 ![pic](.\pic\4.png)

（5）导入后Assets会出现Demigiant目录和新增到Resources的资源
 ![pic](.\pic\5.png)

（6）场景对象Cube加入DOTween Animation脚本，分别设为移动效果
 ![pic](.\pic\6.png)

（7）旋转效果
 ![pic](.\pic\7.png)

（8）缩放效果
 ![pic](.\pic\8.png)

（9）变色效果
 ![pic](.\pic\9.png)

（10）按钮DoMove的点击事件与Cube的移动效果ID绑定，其他按钮相同。
 ![pic](.\pic\10.png)

（11）而DoPlay按钮绑定的是DOPlay事件，即绑定Cube所有DOTWeen效果
 ![pic](.\pic\11.png)

（12）注意要把DOTWeen属性的AutoPlay关闭。
 ![pic](.\pic\12.png)

（13）实测效果。
 ![pic](.\pic\13.gif)



以上简单回顾。

参考资料：
[官方例子]
DOTweenAnimation_Advanced