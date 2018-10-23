系统：Windows 8
引擎：Unity 2017.2.1f1

#### （1）在unity官网注册账号，然后从Assets Store获取免费模型资源unity-chan（陈氏）。

 ![1](.\pic\1.jpg)

#### （2）下载后，点击Import，导入资源。

 ![2](.\pic\2.jpg)

如果你要找回下载的资源，按操作系统区分，Untiy的资源下载目录是：（win7网上说的，win8 & win10是实测）
> win7：C:\Users\你的用户名\AppData\Roaming\Unity\Asset Store\Unity Technologies\
> win8 & win10：C:\Users\你的用户名\AppData\Roaming\Unity\Asset Store-5.x\

#### （3）可以选择导入的资源

 ![3](.\pic\3.jpg)

#### （4）不可缺少的是模型文件，unitychan.fbx

 ![4](.\pic\4.jpg)

#### （5）还有动画，材质和shader。

 ![5](.\pic\5.jpg)

#### （6）把模型拉入场景。

 ![6](.\pic\6.jpg)

#### （7）创建动画控制器，Animator Controller。

 ![7](.\pic\7.jpg)

#### （8）把刚创建的动画控制器拉进模型的Animator组件的Controller属性。

 ![8](.\pic\8.jpg)

#### （9）打开Animator窗口。

 ![9](.\pic\9.jpg)

#### （10）动画文件拉进Animator窗口，然后Entry连接步行动画，那就一开始就走路了。

 ![10](.\pic\10.jpg)

#### （11）运行效果如下，会看到Animator窗口的正在使用的动画文件会出现进度条。

 ![11](.\pic\11.jpg)



以上简单回顾。

参考资料：
https://docs.unity3d.com/2017.2/Documentation/Manual/class-Animator.html
http://www.cnblogs.com/hejianchun/articles/3069432.html