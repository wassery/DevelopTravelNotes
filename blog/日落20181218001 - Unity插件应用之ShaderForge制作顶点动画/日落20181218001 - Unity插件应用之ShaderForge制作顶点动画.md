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

（4）其shader代码如下。
```
// Shader created with Shader Forge v1.38 
// Shader Forge (c) Neat Corporation / Joachim Holmer - http://www.acegikmo.com/shaderforge/
// Note: Manually altering this data may prevent you from opening it in Shader Forge
/*SF_DATA;ver:1.38;sub:START;pass:START;ps:flbk:,iptp:0,cusa:False,bamd:0,cgin:,lico:1,lgpr:1,limd:0,spmd:1,trmd:0,grmd:0,uamb:True,mssp:True,bkdf:False,hqlp:False,rprd:False,enco:False,rmgx:True,imps:True,rpth:0,vtps:0,hqsc:True,nrmq:1,nrsp:0,vomd:0,spxs:False,tesm:0,olmd:1,culm:0,bsrc:3,bdst:7,dpts:2,wrdp:False,dith:0,atcv:False,rfrpo:True,rfrpn:Refraction,coma:15,ufog:False,aust:True,igpj:True,qofs:0,qpre:3,rntp:2,fgom:False,fgoc:False,fgod:False,fgor:False,fgmd:0,fgcr:0.5,fgcg:0.5,fgcb:0.5,fgca:1,fgde:0.01,fgrn:0,fgrf:300,stcl:False,atwp:False,stva:128,stmr:255,stmw:255,stcp:6,stps:0,stfa:0,stfz:0,ofsf:0,ofsu:0,f2p0:False,fnsp:False,fnfb:False,fsmp:False;n:type:ShaderForge.SFN_Final,id:3138,x:32719,y:32712,varname:node_3138,prsc:2|emission-1165-OUT,voffset-6921-OUT;n:type:ShaderForge.SFN_Color,id:7241,x:32291,y:32536,ptovrint:False,ptlb:ColorA,ptin:_ColorA,varname:node_7241,prsc:2,glob:False,taghide:False,taghdr:False,tagprd:False,tagnsco:False,tagnrm:False,c1:0.07843138,c2:0.3921569,c3:0.7843137,c4:1;n:type:ShaderForge.SFN_Lerp,id:1165,x:32520,y:32813,varname:node_1165,prsc:2|A-7241-RGB,B-4923-RGB,T-5654-OUT;n:type:ShaderForge.SFN_Color,id:4923,x:32055,y:32619,ptovrint:False,ptlb:ColorB,ptin:_ColorB,varname:node_4923,prsc:2,glob:False,taghide:False,taghdr:False,tagprd:False,tagnsco:False,tagnrm:False,c1:1,c2:1,c3:1,c4:1;n:type:ShaderForge.SFN_TexCoord,id:1409,x:31573,y:32754,varname:node_1409,prsc:2,uv:0,uaff:False;n:type:ShaderForge.SFN_Add,id:3800,x:31767,y:32754,varname:node_3800,prsc:2|A-2994-OUT,B-1409-U;n:type:ShaderForge.SFN_Time,id:6222,x:31573,y:32579,varname:node_6222,prsc:2;n:type:ShaderForge.SFN_Tau,id:4887,x:31733,y:33018,varname:node_4887,prsc:2;n:type:ShaderForge.SFN_Multiply,id:71,x:31933,y:32843,varname:node_71,prsc:2|A-3800-OUT,B-8556-OUT,C-4887-OUT;n:type:ShaderForge.SFN_Vector1,id:8556,x:31716,y:32929,varname:node_8556,prsc:2,v1:2;n:type:ShaderForge.SFN_Sin,id:8175,x:32098,y:32830,varname:node_8175,prsc:2|IN-71-OUT;n:type:ShaderForge.SFN_Multiply,id:6921,x:32471,y:33047,varname:node_6921,prsc:2|A-5654-OUT,B-6108-OUT,C-9280-OUT;n:type:ShaderForge.SFN_NormalVector,id:6108,x:32228,y:33018,prsc:2,pt:False;n:type:ShaderForge.SFN_Vector1,id:9280,x:32239,y:33186,varname:node_9280,prsc:2,v1:0.3;n:type:ShaderForge.SFN_Multiply,id:2994,x:31767,y:32601,varname:node_2994,prsc:2|A-1844-OUT,B-6222-T;n:type:ShaderForge.SFN_Vector1,id:1844,x:31692,y:32528,varname:node_1844,prsc:2,v1:0.5;n:type:ShaderForge.SFN_Clamp01,id:5654,x:32283,y:32830,varname:node_5654,prsc:2|IN-8175-OUT;proporder:7241-4923;pass:END;sub:END;*/

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

（5）实测效果。
 ![pic](.\pic\5.gif)

以上简单回顾。

参考：

Shader Forge - Gradients (Part 2, Manipulation, Waves & Angular Healthbar)
https://www.youtube.com/watch?v=VnBNBMfk9HM

ShaderForge官网
http://acegikmo.com/shaderforge/nodes/?lang=zh_cn

《Unity Shader入门精要》第11.3节
