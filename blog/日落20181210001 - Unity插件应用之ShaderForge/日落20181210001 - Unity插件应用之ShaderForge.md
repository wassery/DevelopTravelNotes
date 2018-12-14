（1）四元数为例，xyzw可以与rgba互换，三元数xyz、二元数rg如此类推。

（2）UV Coordinates：uv坐标是一个二元数。从顶点着色器输出给段着色器。

（3）Component Mask：例如，以uv坐标的node为基础，当uv坐标传给C.M的是一元数r或g，那么C.M也只能是个一元数，如：uv.r或uv.g，只能变成uv.r.r或uv.g.r。但uv传给C.M的是二元数时，C.M相当于UV的一个引用。

以上简单回顾。

参考：

Shader Forge - Gradients (Part 1, The Basics)
https://www.youtube.com/watch?v=kMHxQukEFoE

Shader Forge - Gradients (Part 2, Manipulation, Waves & Angular Healthbar)
https://www.youtube.com/watch?v=VnBNBMfk9HM

Shader Forge - Gradients (Part 3, Color Ramps & Dissolve)
https://www.youtube.com/watch?v=qCkdVX1RhJ4

Shader Forge Tutorials
https://www.youtube.com/playlist?list=PLHkZsIwT_SixXK95l0IHaCTwaRKqzGYiC

ShaderForge-旗帜飘动
https://blog.csdn.net/wwlcsdn000/article/details/78866806

ShaderForge-波光铠甲
https://blog.csdn.net/wwlcsdn000/article/details/78858416

ShaderForge-水面折射
https://blog.csdn.net/wwlcsdn000/article/details/78874268

ShaderForge 入门火焰流动效果
https://blog.csdn.net/u014028063/article/details/82689269

ShaderForge官网
http://acegikmo.com/shaderforge/nodes/?lang=zh_cn
