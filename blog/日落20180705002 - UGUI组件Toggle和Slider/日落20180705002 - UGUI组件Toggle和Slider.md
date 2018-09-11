系统：Windows 7
引擎：Unity 5.6.5p4

在Hierarchy窗口右键选中Create Empty，生成GameObject作为根节点，右键根节点选UI下的组件，则在根节点里添加各种组件Toggle/Slider/Button/Text/Image等等。

以Toggle和Slider为例：

通过添加OnValueChanged的列表项，节点设为根节点，事件设为GameObject.SendMessage，然后可以自定义事件函数的名称，如OnXXXX这样的，那么在根节点添加脚本，该脚本继承MonoBehaviour类，在该子类中定义之前在OnValueChanged中设置的OnXXXX函数，即能用当前的组件值进行相应操作，其中Toggle的组件值value是个float型，而Slider的组件值isOn是个bool型。另外，也可以在Start函数中对组件值进行设置默认值。

Slider还可以在面板属性上勾选Whole Numbers的选项，滑条则以整数增减，否则以浮点数增减。

以上简单回顾。

参考资料：
https://docs.unity3d.com/Manual/script-Toggle.html
https://docs.unity3d.com/Manual/script-Slider.html
