## 环境
> 系统：Windows 10
> 引擎：VS2017

## 目的
> 通过制作自定义的条件Attribute类及预定义参数，降低元数据的无效信息量。

## 实例

```
#define TEST_1
//#define TEST_2

using System;
using System.Diagnostics;

namespace ConditionalAttributeTest
{
    #region 特性类
    [Conditional("TEST_1")] // 只有定义了TEST_1，才会应用于目标元素，并在元数据生成此特性信息。
    public sealed class Cond_1_Attribute : Attribute { }

    [Conditional("TEST_2")] // 只有定义了TEST_2，才会应用于目标元素，并在元数据生成此特性信息。
    public sealed class Cond_2_Attribute : Attribute { }

    [Conditional("TEST_1")][Conditional("TEST_2")] // 当定义了TEST_1或TEST_2时，就会应用于目标元素，并在元数据生成此特性信息。
    public sealed class Cond_3_Attribute : Attribute { }
    #endregion

    #region 测试类
    [Cond_1_][Cond_2_][Cond_3_]
    public sealed class TargetType {}
    #endregion

    class Program
    {
        private static void ShowResult(Type targetType, Type attrType)
        {
            Console.WriteLine("{0} is {1}applied to {2} type.", attrType, Attribute.IsDefined(targetType, attrType) ? "" : "not ", targetType);
            Console.WriteLine();
        }

        static void Main(string[] args)
        {
            Type targetType = typeof(TargetType);
            Type[] attrTypes =
            {
                typeof(Cond_1_Attribute),
                typeof(Cond_2_Attribute),
                typeof(Cond_3_Attribute),
            };

            foreach (Type attrType in attrTypes)
            {
                Program.ShowResult(targetType, attrType);
            }
        }
    }
}

```

## 结果

```
ConditionalAttributeTest.Cond_1_Attribute is applied to ConditionalAttributeTest.TargetType type.

ConditionalAttributeTest.Cond_2_Attribute is not applied to ConditionalAttributeTest.TargetType type.

ConditionalAttributeTest.Cond_3_Attribute is applied to ConditionalAttributeTest.TargetType type.
```



以上简单回顾。

参考资料： 

《CLR via C#(第3版)》第18.7节