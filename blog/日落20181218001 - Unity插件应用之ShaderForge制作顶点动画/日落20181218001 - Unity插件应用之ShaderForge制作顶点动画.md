## 环境
> 系统：Windows 10
> 引擎：Unity 2017.2.1f1
> 工具：Shader Forge 1.38

## 目的
> 使用Shader Forge制作顶点动画的实例。

（1）场景布局如下。
 ![pic](.\pic\1.png)

（1-1）
 ![pic](.\pic\1-1.png)

（1-2）
 ![pic](.\pic\1-2.png)

（1-3）
 ![pic](.\pic\1-3.png)

（1-4）
 ![pic](.\pic\1-4.png)

（1-5）
 ![pic](.\pic\1-5.png)

（1-6）
 ![pic](.\pic\1-6.png)

（1-7）
 ![pic](.\pic\1-7.png)

（2）Shader Forge编辑如下。（编辑方式看《[Unity插件应用之ShaderForge制作颜色渐变效果](https://blog.csdn.net/minami_takumi/article/details/85054896)》）
 ![pic](.\pic\2.png)

（3）
 ![pic](.\pic\3.png)

（4-1）其shader代码如下。
```
// 前略...

Shader "Shader Forge/StreamerShader" {
    Properties {
        _ColorA ("ColorA", Color) = (0.07843138,0.3921569,0.7843137,1)
        _ColorB ("ColorB", Color) = (1,1,1,1)
    }
    SubShader {
        Tags {
            "IgnoreProjector"="True"
            "Queue"="Transparent"
            "RenderType"="Transparent"
        }
        Pass {
            Name "FORWARD"
            Tags {
                "LightMode"="ForwardBase"
            }
            Blend SrcAlpha OneMinusSrcAlpha
            ZWrite Off
            
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #define UNITY_PASS_FORWARDBASE
            #include "UnityCG.cginc"
            #pragma multi_compile_fwdbase
            #pragma only_renderers d3d9 d3d11 glcore gles gles3 
            #pragma target 3.0
            uniform float4 _ColorA;
            uniform float4 _ColorB;
            struct VertexInput {
                float4 vertex : POSITION;
                float3 normal : NORMAL;
                float2 texcoord0 : TEXCOORD0;
            };
            struct VertexOutput {
                float4 pos : SV_POSITION;
                float2 uv0 : TEXCOORD0;
                float3 normalDir : TEXCOORD1;
            };
            VertexOutput vert (VertexInput v) {
                VertexOutput o = (VertexOutput)0;
                o.uv0 = v.texcoord0;
                o.normalDir = UnityObjectToWorldNormal(v.normal);
                float4 node_6222 = _Time;
                float node_5654 = saturate(sin((((0.5*node_6222.g)+o.uv0.r)*2.0*6.28318530718)));
                v.vertex.xyz += (node_5654*v.normal*0.3);
                o.pos = UnityObjectToClipPos( v.vertex );
                return o;
            }
            float4 frag(VertexOutput i) : COLOR {
                i.normalDir = normalize(i.normalDir);
                float3 normalDirection = i.normalDir;
////// Lighting:
////// Emissive:
                float4 node_6222 = _Time;
                float node_5654 = saturate(sin((((0.5*node_6222.g)+i.uv0.r)*2.0*6.28318530718)));
                float3 emissive = lerp(_ColorA.rgb,_ColorB.rgb,node_5654);
                float3 finalColor = emissive;
                return fixed4(finalColor,1);
            }
            ENDCG
        }
        Pass {
            Name "ShadowCaster"
            Tags {
                "LightMode"="ShadowCaster"
            }
            Offset 1, 1
            Cull Back
            
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #define UNITY_PASS_SHADOWCASTER
            #include "UnityCG.cginc"
            #include "Lighting.cginc"
            #pragma fragmentoption ARB_precision_hint_fastest
            #pragma multi_compile_shadowcaster
            #pragma only_renderers d3d9 d3d11 glcore gles gles3 
            #pragma target 3.0
            struct VertexInput {
                float4 vertex : POSITION;
                float3 normal : NORMAL;
                float2 texcoord0 : TEXCOORD0;
            };
            struct VertexOutput {
                V2F_SHADOW_CASTER;
                float2 uv0 : TEXCOORD1;
                float3 normalDir : TEXCOORD2;
            };
            VertexOutput vert (VertexInput v) {
                VertexOutput o = (VertexOutput)0;
                o.uv0 = v.texcoord0;
                o.normalDir = UnityObjectToWorldNormal(v.normal);
                float4 node_6222 = _Time;
                float node_5654 = saturate(sin((((0.5*node_6222.g)+o.uv0.r)*2.0*6.28318530718)));
                v.vertex.xyz += (node_5654*v.normal*0.3);
                o.pos = UnityObjectToClipPos( v.vertex );
                TRANSFER_SHADOW_CASTER(o)
                return o;
            }
            float4 frag(VertexOutput i) : COLOR {
                i.normalDir = normalize(i.normalDir);
                float3 normalDirection = i.normalDir;
                SHADOW_CASTER_FRAGMENT(i)
            }
            ENDCG
        }
    }
    FallBack "Diffuse"
    CustomEditor "ShaderForgeMaterialInspector"
}

```

（4-2）如果不需要阴影效果，可以把“ShadowCaster”的Pass去掉。
```
// 前略...

Shader "Shader Forge/StreamerShader" {
    Properties {
        _ColorA ("ColorA", Color) = (0.07843138,0.3921569,0.7843137,1)
        _ColorB ("ColorB", Color) = (1,1,1,1)
    }
    SubShader {
        Tags {
            "IgnoreProjector"="True"
            "Queue"="Transparent"
            "RenderType"="Transparent"
        }
        Pass {
            Name "FORWARD"
            Tags {
                "LightMode"="ForwardBase"
            }
            Blend SrcAlpha OneMinusSrcAlpha
            ZWrite Off
            
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #define UNITY_PASS_FORWARDBASE
            #include "UnityCG.cginc"
            #pragma multi_compile_fwdbase
            #pragma only_renderers d3d9 d3d11 glcore gles gles3 
            #pragma target 3.0
            uniform float4 _ColorA;
            uniform float4 _ColorB;
            struct VertexInput {
                float4 vertex : POSITION;
                float3 normal : NORMAL;
                float2 texcoord0 : TEXCOORD0;
            };
            struct VertexOutput {
                float4 pos : SV_POSITION;
                float2 uv0 : TEXCOORD0;
                float3 normalDir : TEXCOORD1;
            };
            VertexOutput vert (VertexInput v) {
                VertexOutput o = (VertexOutput)0;
                o.uv0 = v.texcoord0;
                o.normalDir = UnityObjectToWorldNormal(v.normal);
                float4 node_6222 = _Time;
                float node_5654 = saturate(sin((((0.5*node_6222.g)+o.uv0.r)*2.0*6.28318530718)));
                v.vertex.xyz += (node_5654*v.normal*0.3);
                o.pos = UnityObjectToClipPos( v.vertex );
                return o;
            }
            float4 frag(VertexOutput i) : COLOR {
                i.normalDir = normalize(i.normalDir);
                float3 normalDirection = i.normalDir;
////// Lighting:
////// Emissive:
                float4 node_6222 = _Time;
                float node_5654 = saturate(sin((((0.5*node_6222.g)+i.uv0.r)*2.0*6.28318530718)));
                float3 emissive = lerp(_ColorA.rgb,_ColorB.rgb,node_5654);
                float3 finalColor = emissive;
                return fixed4(finalColor,1);
            }
            ENDCG
        }
    }
    FallBack "Diffuse"
    CustomEditor "ShaderForgeMaterialInspector"
}

```

（4-3）看到saturate，就会想起《Unity Shader入门精要》第6.4节提到过，把值截取在[0,1]的范围内。而对照编辑界面，可知，saturate就是“Clamp 0-1”节点。

（5）实测效果。（看起来质地有点硬，需要再优化。）
 ![pic](.\pic\5.gif)

以上简单回顾。

参考：

Shader Forge - Gradients (Part 2, Manipulation, Waves & Angular Healthbar)
https://www.youtube.com/watch?v=VnBNBMfk9HM

ShaderForge官网
http://acegikmo.com/shaderforge/nodes/?lang=zh_cn

《Unity Shader入门精要》第6.4节和第11.3节
