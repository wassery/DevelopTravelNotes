## 环境
> 系统：Windows 10
> 引擎：VS2017

## 实例
> 通过制作自定义的Attribute类，进行检测是否绑定某特性的实例。

## 实例

```
using System;
using System.Reflection;

namespace AttributeTest
{
    #region 特性类
    [AttributeUsage(AttributeTargets.All, Inherited = true)]
    internal class AAttribute : Attribute
    {

    }

    [AttributeUsage(AttributeTargets.Class, Inherited = false)]
    internal class BAttribute : Attribute
    {

    }

    [AttributeUsage(AttributeTargets.Method, Inherited = true)]
    internal class CAttribute : Attribute
    {

    }
    #endregion

    #region 测试类
    [A][B]
    internal class BaseType
    {

    }

    internal class DerideType : BaseType
    {

    }
    #endregion

    class Program
    {
        static void Main(string[] args)
        {
            MemberInfo attrInfo = typeof(DerideType);
            Type attrType = typeof(BAttribute);

            #region IsDefined检测法
            Console.WriteLine("IsDefined检测法:");
            Boolean isDefined = Attribute.IsDefined(attrInfo, attrType);
            if (isDefined == true)
                Console.WriteLine("{0} is used to {1}", attrType, attrInfo);
            else
                Console.WriteLine("{0} is not used to {1}", attrType, attrInfo);
            #endregion

            #region GetCustomAttribute检测法
            Console.WriteLine("\nGetCustomAttribute检测法:");
            Attribute singleAttr = Attribute.GetCustomAttribute(attrInfo, attrType);
            if (singleAttr != null)
                Console.WriteLine("{0} is used to {1}", attrType, attrInfo);
            else
                Console.WriteLine("{0} is not used to {1}", attrType, attrInfo);
            #endregion

            #region GetCustomAttributes检测法
            Console.WriteLine("\nGetCustomAttributes检测法:");
            Attribute[] attrs = Attribute.GetCustomAttributes(attrInfo);
            foreach (Attribute attr in attrs)
            {
                Console.WriteLine("{0} is used to {1}", attr.GetType().ToString(), attrInfo);
            }
            #endregion
        }
    }
}

```



以上简单回顾。

参考资料： 

《CLR via C#(第3版)》第18章