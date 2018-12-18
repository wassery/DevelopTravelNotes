## 环境
> 系统：Windows 10
> 引擎：Unity 2017.2.1f1
> 工具：Shader Forge 1.38

## 目的
> 使用Shader Forge制作渐变效果的实例。

（1）导入Shader Forge插件。
 ![pic](.\pic\1.png)

（2）从菜单项Window的子项，找到Shader Forge。
 ![pic](.\pic\2.png)

（3）选择New Shader。
 ![pic](.\pic\3.png)

（4）点击“Unlit”，保存新的Shader文件。
 ![pic](.\pic\4.png)

（5-1）做渐变嘛，少不了线性插值，因为它作用于混合两个值或颜色。在Shader Forge编辑界面，按L键，出现L开头的选项集合。
 ![pic](.\pic\5-1.png)

（5-2）选择Lerp，出现Lerp节点。
 ![pic](.\pic\5-2.png)

（5-3）Lerp的计算：
按照本例设置，
插值系数：横向坐标U（或者纵向坐标V），设值为t；
起点颜色：ColorA，设值为(r0, g0, b0, a0)；
终点颜色：ColorB，设值为(r1, g1, b1, a1)；
过渡颜色：Color，设值为(r, g, b, a)；
由于数值为一元数，二维坐标为二元数xy，颜色为四元数rgba。
而本例虽然用到的是颜色，但回看代码：
```
uniform float4 _ColorA;
uniform float4 _ColorB;
// 其中代码略......
float3 emissive = lerp(_ColorA.rgb,_ColorB.rgb,i.uv0.r);
```
虽然ColorA和ColorB均设为四元数，只是用到三元数rgb。
根据线性插值原理，
则有t = (r - r0) / (r1 - r0) = (g - g0) / (g1 - g0) = (b - b0) / (b1 - b0)
即：
r = t * (r1 - r0) + r0
g = t * (g1 - g0) + g0
b = t * (b1 - b0) + b0

（6-1）按C键，出现C开头的选项集合。
 ![pic](.\pic\6-1.png)

（6-2）选择Color，出现Color节点，渐变需要两个Color节点。
 ![pic](.\pic\6-2.png)

（7）把Color节点改名为ColorA(蓝色)，ColorB(红色)。
 ![pic](.\pic\7.png)

（8）左键点击Color的输出端，拖拉出一条线到Lerp的输入端，此处混合颜色，就拖RGB输入端，R、G、B的输出只是一个值。两个Color分别连入Lerp的A和B端。
 ![pic](.\pic\8.png)

（9-1）按U键，出现U开头的选项集合。
 ![pic](.\pic\9-1.png)

（9-2）选择UV Coordinates，出现UV Coord.节点。
 ![pic](.\pic\9-2.png)

（10-1）使用UV坐标的U值作为插值系数的效果是：横向渐变。
 ![pic](.\pic\10-1.png)

（10-2）使用UV坐标的V值作为插值系数的效果是：纵向渐变。
 ![pic](.\pic\10-2.png)

（11）关闭Shader Forge编辑器，选择生成的Shader文件。点击Open shader code，打开代码。
 ![pic](.\pic\11.png)

（12-1）UV Coordinates：uv坐标，是一个二元数。从顶点着色器输出给片段着色器。
 ![pic](.\pic\12-1.png)

（12-2）四元数为例，xyzw可以与rgba互换，三元数xyz、二元数rg如此类推。横向渐变使用R通道，即.r。如果纵向渐变使用G通道，即.g。
 ![pic](.\pic\12-2.png)

（13）回到Unity，选择Shader文件，点击Open in Shader Forge，重新进入Shader Forge编辑器。
 ![pic](.\pic\13.png)

（14-1）添加Component Mask节点。Component Mask：分量遮罩，用于重新排序或提取向量的通道。例如，以uv坐标为基点，当uv坐标传给分量遮罩的是一元数r或g，那么分量遮罩也只能是个一元数，如：uv.r或uv.g，只能变成uv.r.r或uv.g.r。但uv传给分量遮罩的是二元数时，分量遮罩相当于UV的一个引用。
 ![pic](.\pic\14-1.png)

（14-2）把分量遮罩插入到UV坐标和Lerp节点中间。
 ![pic](.\pic\14-2.png)

（14-3）此时，分量遮罩输出的是UV的R通道的R通道，实质就是UV的R通道，上述（14-1）已说明原因。
 ![pic](.\pic\14-3.png)

（15）布局如下。
 ![pic](.\pic\15.png)

（16）实测效果，全黑？（实测机系统：Android 6.0.1）
 ![pic](.\pic\16.png)

（17-1）回到Shader Forge编辑器界面，选择Shader Setting...选项。
 ![pic](.\pic\17-1.png)

（17-2）勾选OpenGLES 3.0
 ![pic](.\pic\17-2.png)

（17-3）代码加入gles3
 ![pic](.\pic\17-3.png)

（18）实测效果，正常。
 ![pic](.\pic\18.png)

以上简单回顾。

参考：

Shader Forge - Gradients (Part 1, The Basics)
https://www.youtube.com/watch?v=kMHxQukEFoE

ShaderForge官网
http://acegikmo.com/shaderforge/nodes/?lang=zh_cn

线性插值
https://en.wikipedia.org/wiki/Linear_interpolation
