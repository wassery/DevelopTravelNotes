目录 【未来】：1.Unity性能分析2.Unity性能优化3.C#基础4.C#设计模式5.Unity打包之资源管理6.Unity屏幕适配方案7.图形学基础之向量8.Unity打包之闪屏界面9.Unity打包之Android热更与强更【现在】：【过去】：《日落20180808001 - Unity调用SDK之Android截屏分享》《日落20180807001 - Unity调用SDK之Android唤起其他App》

---

【未来】：

1.Unity性能分析

参考：

Unity性能优化（2）-官方教程Diagnosing performance problems using the Profiler window翻译

http://www.cnblogs.com/alan777/p/6135703.html

笔记：

（1）帧率对于我们来说可以用于理解为渲染一帧必须用多少毫秒以内完成。通过公式 1000/想要达到的帧率。通过这个公式可以得到，游戏要每秒渲染30帧（30FPS），那么必须在33.3毫秒之内渲染完每一帧。一个60FPS运行的游戏，必须在16.6毫秒内渲染完每一帧。

（2）垂直同步（VSync）用来同步游戏的帧率和屏幕的刷新率。垂直同步会影响游戏的帧率

2.Unity性能优化

参考：

Unity性能优化（3）-官方教程Optimizing garbage collection in Unity games翻译

http://www.cnblogs.com/alan777/p/6155501.html

Unity性能优化（4）-官方教程Optimizing graphics rendering in Unity games翻译

http://www.cnblogs.com/alan777/p/6204759.html

zjz博客

https://blog.csdn.net/zjz520yy/article/list/2?t=

笔记：

内存

（1）Unity在两种内存池中存取：栈内存和堆内存。栈用来存储短期的和小块的数据，堆用来存储长期的和大块的数据。

（2）当内存被返回到内存池时，我们称之为内存释放。

（3）当一个堆变量被创建时，堆上内存不足，则，既可能执行垃圾回收，也可能增加堆内存容量。

（4）堆碎片化，也会导致堆上内存不足。（疑问：堆碎片化具体形成原因？）

内存优化

（1）局部的引用类型变量，改为全局，称为缓存。

（2）不要在频繁函数（如Update）里分配堆内存。如果需要在频繁函数中分配堆内存，则要加入条件控制，只在必要时分配。

（3）用Clear方法清空全局变量，代替New方法分配局部变量。

（4）需要拼接字符串则用StringBuilder。

（5）Unity有部分调用方式会产生垃圾，例如直接用GameObject.tag来做比较会产生垃圾，但用GameObject.CompareTag()则不会。

（6）当一个值类型变量被装箱时，Unity创建一个临时的System.Object在堆上，去包装值类型变量。System.Object是引用类型的变量，而这个临时对象被创建和销毁时产生垃圾。

（7）谨慎使用协程。可以用其他方法替代协程的情况有：例如，如果我们使用协程只是为了管理时间，我们可以直接在Update（）方法中处理时间相关的内容。如果我们使用协程是为了管理函数的执行顺序，我们可以创建一个消息系统来使对象之间互相交流。

（8）结构体包含引用类型（如string），垃圾回收器就要检查整个结构体。

（9）哪怕是全局变量，在函数里也尽量调用值类型，而非引用类型。这样可以降低垃圾回收器的负载。

（10）在适当的时机，手动强制执行垃圾回收ystem.GC.Collect();

渲染

（1）CPU给每个draw call创建一个数据包，称为batch。Batch有时会包含一些draw call以外的数据，每一个batch必须包含一个draw call。

（2）GPU按照CPU发送的指令顺序处理这些指令。如果当前任务是SetPass call，那么GPU更新渲染状态。如果当前任务是draw call，那么GPU渲染网格。

（3）在渲染一帧中，CPU的工作分为三类：决定什么必须被绘制，为GPU准备好命令，发送命令给GPU。

（4）主线程用于游戏的主要CPU任务，包括一些渲染任务。渲染进程是专门用于发送命令给GPU的。每个工人线程执行一个单独的任务，例如剔除和网格蒙皮。

（5）CPU的核心数量越多，就会生成越多的工人线程数。

（6）注意：不是所有的平台都支持多线程渲染，例如：WebGL不支持这个功能。

（7）填充率是指GPU在屏幕上每秒可以渲染的像素数。如果游戏受到填充率的限制，意味着游戏每帧尝试绘制的像素数量超过了GPU的处理能力。

（8）Overdraw是指相同的像素绘制了多次。这是在物体绘制在其他物体之上的时候发生的，也在很大程度上引起了填充率问题。

（9）显存带宽是指GPU读写它的专用内存的速度。如果游戏受限于显存带宽，通常意味着所使用的纹理太大了，以至于GPU无法快速处理。

（10）顶点处理是指GPU必须渲染网格中的每一个顶点的工作。

渲染分析

（1）使用Profiler分析，注意GPU时间，在Player settings中降低显示分辨率后，性能改善，很大几率是填充率的问题。

（2）使用Profiler分析，注意GPU时间，在质量设置中降低当前平台的纹理质量，性能改善，很大几率是显存带宽的问题。

（3）如果游戏是GPU限制，并且已经确认了不是填充率和显存带宽引起的问题，那么就很可能是顶点处理引起的。

渲染优化

（1）发送命令到GPU中，其中最耗时的操作是SetPass call。如果CPU限制是由发送命令到GPU引起的，那么降低SetPass的数量通常是最好的改善性能的办法。

（2）降低batch数量或者使更多的对象共享相同的渲染状态，通常会减低SetPass call数量。

（3）没有降低SetPass call数量，他本身也会导致性能改进。这是因为CPU能够更有效率的处理单个batch，即使它和几个batch包含了数量相同的网格数据。

（4）降低要渲染的对象数量，通常可以同时降低SetPass call和batch的数量。

（5）降低每个要渲染的对象的渲染次数，通常可以降低SetPass call。

（6）合并要渲染的对象的数据到更少的batches，可以降低batches数量。

（7）动态阴影的优化方案：我们可以设置阴影距离，确保只有近处的物体投射阴影。

（8）使用Renderer.material会复制材质，并且返回一个新副本的引用，这样做会破坏batching。如果访问一个在合并中的物体的材质，应使用Renderer.sharedMaterial。

（9）剔除操作会遍历场景中或摄像机中的每个激活物体，为了降低这些，我们应该关闭摄像机，并且对于当前不使用的物体反激活或者禁用renderer。

（10）模型不需要运动时，使用MeshRenderer组件替换SkinnedMeshRenderers。

（11）蒙皮的消耗是在每个顶点上，因此，使用顶点较少的模型可以有效降低工作量。

（12）在某个时刻，游戏需要做消耗很大的渲染操作并且在主线程上的脚本操作的消耗也很大，将使得CPU限制，此时主线程操作和渲染无关，所以要优化渲染和脚本，才能优化性能。

（13）GPU受限出现在填充率问题上，很大机率是由于片元shader。

（14）最常见的引起Overdraw的因素是透明材质，未优化的粒子，和重叠的UI元素。

（15）使用屏幕后处理技术也会极大的影响填充率，尤其是我们使用了不止一种的屏幕后处理的时候。

（16）同一个摄像机下使用了多个屏幕后处理，这将造成成倍的shader pass。这种情况下，我们应该合并shader到一个单独的pass，例如Unity’s PostProcessing Stack。

（17）显存带宽出现问题的两个处理方案：纹理压缩技术（可以同时极大的降低纹理在磁盘和内存中的大小），多级渐远纹理（是Unity对远处的物体使用的低分辨率版本的纹理）。

（18）顶点处理出现问题的处理方案一：使用法线贴图技术去模拟更复杂的网格。

（19）顶点处理出现问题的处理方案二：没有使用法线贴图技术，可以在网格的导入设置中关闭顶点的切线，这会降低GPU处理顶点的数据量。

（20）顶点处理出现问题的处理方案三：LOD（Level of detail），这是当物体远离摄像机时，降低物体网格的复杂度的技术。这可以有效的降低GPU需要渲染的顶点数量。

代码优化

[LUA]
（1）table[#table+1] = xxx 代替table.insert

3.C#基础

参考：

c#特性-中括号

https://zm8.sm-tc.cn/?src=l4uLj4zF0NCIiIjRnJGdk5CYjNGckJLQ0pueiJHQno2cl5aJmtDNz87N0M%2FG0M3G0M3Iz8fPyszRl4uSkw%3D%3D&uid=6b05d9dfca7f9a6d49c5a17a8195b0db&hid=c9a7f41523323cbea327076d44ad9885&pos=2&cid=9&time=1531790463322&from=click&restype=1&pagetype=0000000000000000&bu=web&query=c%23%E4%B8%AD%E6%8B%AC%E5%8F%B7&mode=&v=1&force=true&wap=false&province=%E5%B9%BF%E4%B8%9C%E7%9C%81&city=%E5%B9%BF%E5%B7%9E%E5%B8%82&uc_param_str=dnntnwvepffrgibijbprsvdsdichei

C#关键字之override详解

https://blog.csdn.net/yiyelanxin/article/details/71711383

C# 基础系列--类一(partial 部分类和部分方法)

https://www.cnblogs.com/qionghua/archive/2012/07/16/2594200.html

c#反射机制

http://52csharp.com/1077.html

https://www.jb51.net/article/86280.htm

C# 反射，通过类名、方法名调用方法

https://www.cnblogs.com/coderJiebao/p/CSharp09.html

4.C#设计模式

参考：

C#设计模式总结

https://www.cnblogs.com/zhili/p/DesignPatternSummery.html

5.Unity打包之资源管理

参考：

Unity资源管理（一）-资源（Assets）、对象（Objects）和序列化

https://blog.csdn.net/qq_21397217/article/details/80500276

Unity资源管理（二）-Resources文件夹

https://blog.csdn.net/qq_21397217/article/details/80542155

Unity资源管理（三）-AssetBundle基本原理

https://blog.csdn.net/qq_21397217/article/details/80571819

Unity资源管理（四）-AssetBundle使用模式

https://blog.csdn.net/qq_21397217/article/details/80586867

6.Unity屏幕适配方案

参考：

UGUI之RectTransform知识点

http://www.manew.com/thread-41633-1-1.html

7.图形学基础之向量

参考：

《3D数学基础：图形与游戏开发》第4章&第5章

向量的减法

https://wenku.baidu.com/view/ade8df52bfd5b9f3f90f76c66137ee06eef94e15.html

笔记：

（1）从原点开始，向量[x,y]的位移，总是会到达点(x,y)的位置。 == 向量[x,y]描述了原点到点(x,y)的位移量。

（2）向量的大小=向量的长度=模=标量，标量是没有方向的向量。

（3）零向量=加性单位元，就是一维以上维度的零。

（4）负向量=加性逆元，就是把某向量x给cancel作用的向量(-x)，cancel之后就变成零向量。

（5）单位向量=标准化向量=法向量=法线，标准化normalize，法=标准normal，normalize=使…符合标准=标准化。什么法？1之法

（6）向量a和向量b，向量起点为箭尾，向量终点为箭头，a+b的几何表现是a起点到b终点，a-b的几何表现是b终点到a终点。a+b=b+a，a-b≠b-a。

（7）利用向量的减法求出两点间距离，n维通用。

（8）两向量点乘结果越大，方向越趋近完全相同，即两向量夹角接近0度。两向量点乘结果越小，方向越趋近完全相反，即两向量夹角接近180度。

（9）成夹角的两向量(a和b)，其一向量(a)的某个分量(a1)若能平行于另一向量(b)，则此分量(a1)是另一向量(b)的投影。

8.Unity打包之闪屏界面

参考：

Android启动页面（闪屏页面）的实现

https://blog.csdn.net/PlainWaterh/article/details/78184847

安卓闪屏界面作用及总结

https://blog.csdn.net/twc18638942853/article/details/72770267

9.Unity打包之Android热更与强更

参考：

Android热更新技术的研究与实现(一)

https://blog.csdn.net/u012513972/article/details/78269288

Android app强更解决方案

http://www.360doc.com/content/17/0710/11/16915_670255100.shtml

使用Android系统提供的DownloadManager来下载文件

http://www.cnblogs.com/zhengxt/p/3657833.html?utm_source=tuicool&utm_medium=referral



---

【现在】：

---

【过去】：

《日落20180808001 - Unity调用SDK之Android截屏分享》

缺：Application.CaptureScreenshot理解

《日落20180807001 - Unity调用SDK之Android唤起其他App》

缺：Intent理解，PackageManager 和 PackageInfo 

{

Android总结篇——Intent机制详解及示例总结

https://www.cnblogs.com/X-knight/p/5438042.html

Intent详解

https://www.cnblogs.com/engine1984/p/4146621.html

}
