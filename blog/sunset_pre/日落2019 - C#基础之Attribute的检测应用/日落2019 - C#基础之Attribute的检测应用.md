## 环境
> 系统：Windows 10
> 引擎：VS2017

## 目的
> 通过制作自定义的Attribute类，进行检测目标元素是否绑定某特性的实例。

## 实例

```
using System;
using System.Reflection;

namespace AttributeTest
{
    #region 特性类
    [AttributeUsage(AttributeTargets.All, Inherited = true)] // 可应用于各种目标元素，并可应用于该目标元素的派生元素。
    internal class AattrAttribute : Attribute { }

    [AttributeUsage(AttributeTargets.Class, Inherited = false)] // 可应用的目标元素类型是“类”，但不可应用于该目标元素的派生元素。
    internal class BattrAttribute : Attribute { }

    [AttributeUsage(AttributeTargets.Method, Inherited = true)] // 可应用的目标元素类型是“类方法”，并可应用于该目标元素的派生元素。
    internal class CattrAttribute : Attribute { }
    #endregion

    #region 测试类
    [Aattr][Battr]
    internal class BaseType
    {
        [Cattr]
        protected virtual void DoWhat() { }
    }

    internal class DerideType : BaseType
    {
        protected override void DoWhat() { }
    }
    #endregion

    class Program
    {
        static void Main(string[] args)
        {
            MemberInfo attrInfo = typeof(DerideType);
            Type attrType = typeof(BattrAttribute);

            #region IsDefined检测法
            Console.WriteLine("IsDefined检测法:");
            Boolean isDefined = Attribute.IsDefined(attrInfo, attrType);
            if (isDefined == true)
                Console.WriteLine("{0} is used to {1}", attrType, attrInfo);
            else
                Console.WriteLine("{0} is not used to {1}", attrType, attrInfo);
            Console.WriteLine();
            #endregion

            #region GetCustomAttribute检测法
            Console.WriteLine("GetCustomAttribute检测法:");
            Attribute singleAttr = Attribute.GetCustomAttribute(attrInfo, attrType);
            if (singleAttr != null)
                Console.WriteLine("{0} is used to {1}", attrType, attrInfo);
            else
                Console.WriteLine("{0} is not used to {1}", attrType, attrInfo);
            Console.WriteLine();
            #endregion

            #region GetCustomAttributes检测法
            Console.WriteLine("GetCustomAttributes检测法:");
            Attribute[] attrs = Attribute.GetCustomAttributes(attrInfo);
            foreach (Attribute attr in attrs)
            {
                Console.WriteLine("{0} is used to {1}", attr.GetType().ToString(), attrInfo);
            }
            Console.WriteLine();
            #endregion
        }
    }
}

```

## 结果

```
IsDefined检测法:
AttributeTest.BattrAttribute is not used to AttributeTest.DerideType

GetCustomAttribute检测法:
AttributeTest.BattrAttribute is not used to AttributeTest.DerideType

GetCustomAttributes检测法:
AttributeTest.AattrAttribute is used to AttributeTest.DerideType
```



以上简单回顾。

参考资料： 

《CLR via C#(第3版)》第18.2节和第18.4节