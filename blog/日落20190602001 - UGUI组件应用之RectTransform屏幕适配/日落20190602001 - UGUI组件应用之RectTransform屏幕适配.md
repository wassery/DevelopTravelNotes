系统：Windows 10
引擎：Unity 2017.2.1f1

（1）界面设置如下
 ![pic](.\pic\101.png)

各控件设置：
 ![pic](.\pic\102.png)
 ![pic](.\pic\103.png)
 ![pic](.\pic\104.png)
 ![pic](.\pic\105.png)
 ![pic](.\pic\106.png)
 ![pic](.\pic\107.png)
 ![pic](.\pic\108.png)
 ![pic](.\pic\109.png)
 ![pic](.\pic\110.png)
 ![pic](.\pic\111.png)
 ![pic](.\pic\112.png)
 ![pic](.\pic\113.png)
 ![pic](.\pic\114.png)

（2）初始设置比例是16:9，然后改为2:1，4:3，16:10都是可以的。
 ![pic](.\pic\201.png)

（3）然而改为9:16（或者1:2），就少了个HorizontalRelativeImage的控件。
 ![pic](.\pic\301.png)

如果把该控件的锚点又还原回Middle&Center的模式，就可以看到此时该控件的宽度Width值为负数。
 ![pic](.\pic\302.png)

这是因为原设置要求与两边距离分别相隔238px，共476px，而整个画布小于这个值。此时根据[《UGUI组件应用之Canvas屏幕适配》](https://blog.csdn.net/minami_takumi/article/details/86592569)的方法，就可以让小黄条重现。
 ![pic](.\pic\303.png)



以上简单回顾。

参考：

UGUI之RectTransform知识点
http://www.manew.com/thread-41633-1-1.html
