系统：Windows 10
引擎：Unity 2017.2.1f1

（1）添加Scroll View控件
 ![pic](.\pic\1.png)

（2）添加Text控件
 ![pic](.\pic\2.png)

（3）本例不需要水平和垂直滚动条，Delete。
 ![pic](.\pic\3.png)

（4）本例不需要Scroll View背景图，Remove。
 ![pic](.\pic\4.png)

（5）Scroll View设置如下：
 ![pic](.\pic\5.png)

（6）在Scroll View下的Content对象加入Vertical Layout Group和Content Size Fitter脚本
 ![pic](.\pic\6.png)

（7）Text设置如下：
 ![pic](.\pic\7.png)

（8）运行时，Content高度会随着Text内容多少而改变。
 ![pic](.\pic\8.png)

（9）超出部分可以滑动显示，并且不会回弹到头部，这是Vertical Layout Group和Content Size Fitter的功劳。
 ![pic](.\pic\9.png)



以上简单回顾。

参考资料：
工作项目...