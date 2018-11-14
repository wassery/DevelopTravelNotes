系统：Windows 10
引擎：Unity 2017.2.1f1
工具：AssetBundles-Browser

（1）以[《Unity打包之AssetBundle简单实例》](https://blog.csdn.net/minami_takumi/article/details/84026765)的工程为基础。

（2）下载[AssetBundles-Browser](https://github.com/Unity-Technologies/AssetBundles-Browser)，该工具用于对AssetBundle的管理。

（3）把目录塞进项目目录的Assets目录中，打开工程，将会在菜单项Window找到AssetBundle Browser。
 ![pic](.\pic\1.png)

（4）点击上述菜单项，则打开该工具的窗口。左上是Bundle列表，左下是选中的Bundle详情；右上是Asset列表，右下是选中的Asset详情。
 ![pic](.\pic\2.png)

（5）选择Bundle列表的一项，可以在右上栏找到发现同样AssetBundle名的Asset。此时通过观察左下栏和右上栏，重复资源会增加Bundle的大小。可以在右下栏找到重复Asset的路径，从而过滤重复资源。
 ![pic](.\pic\3.png)

其他功能尚未使用到。

以上简单回顾。

参考资料：

[原文]
Unity AssetBundle Browser tool
https://github.com/Unity-Technologies/AssetBundles-Browser/blob/master/Documentation/com.unity.assetbundlebrowser.md

[译文]
【Unity3D技术文档翻译】第1.9篇 使用 Unity AssetBundle Browser tool (AssetBundle系列完结)
https://www.cnblogs.com/hearthstone/p/8478530.html
