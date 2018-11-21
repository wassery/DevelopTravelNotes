## 环境
> 系统：Windows 10
> 引擎：Unity 2017.2.1f1
> 工具：Behavior Designer Version 1.5.12

## 目的
> 使用Behavior Designer制作一个简单实例。

（1）首先把场景布局如此
 ![pic](.\pic\1.png)

（2）导入插件后，目录多了这两个目录。
 ![pic](.\pic\2.png)

（3）添加菜单
 ![pic](.\pic\3.png)

（4）点击Editor会打开Behavior Design窗口
 ![pic](.\pic\4.png)

（5）添加脚本。
IsGoal.cs
```
using UnityEngine;

namespace BehaviorDesigner.Runtime.Tasks
{
    [TaskCategory("Basic/Transform")]
    public class IsGoal : Conditional
    {
        [Tooltip("The GameObject that the task operates on. If null the task GameObject is used.")]
        public SharedGameObject targetGameObject;
        [Tooltip("Goal position")]
        public SharedVector3 goalPosition;

        private Transform targetTransform;
        private GameObject prevGameObject;
        private bool m_IsGoal = false;

        public override void OnStart()
        {
            var currentGameObject = GetDefaultGameObject(targetGameObject.Value);
            if (currentGameObject != prevGameObject) {
                targetTransform = currentGameObject.GetComponent<Transform>();
                prevGameObject = currentGameObject;
            }
        }

        public override TaskStatus OnUpdate()
        {
            if (targetTransform == null) {
                Debug.LogWarning("Transform is null");
                return TaskStatus.Failure;
            }

            // 一旦成功就不再执行
            if (m_IsGoal == true)
            {
                return TaskStatus.Failure;
            }

            // 简单的坐标判断
            bool isGoal = true;
            isGoal = isGoal && goalPosition.Value.x.Equals(Mathf.Floor(targetTransform.position.x));
            isGoal = isGoal && goalPosition.Value.y.Equals(Mathf.Floor(targetTransform.position.y));
            isGoal = isGoal && goalPosition.Value.z.Equals(Mathf.Floor(targetTransform.position.z));
            // 记录结果
            m_IsGoal = isGoal;

            return isGoal ? TaskStatus.Failure : TaskStatus.Success;
        }

        public override void OnReset()
        {
            targetGameObject = null;
            m_IsGoal = false;
        }
    }
}
```
（6）添加Animator。
 ![pic](.\pic\6.png)

（7）添加待机动画idle。
 ![pic](.\pic\7.png)

（8）添加旋转动画rotate。
 ![pic](.\pic\8.png)

（9）给Cube添加脚本Behavoir Tree和Animator。
 ![pic](.\pic\9.png)

（10）行为树设置如下。
 ![pic](.\pic\10.png)

（11）行为树节点设置详情如下。
 ![pic](.\pic\11-1.png)
 ![pic](.\pic\11-2.png)
 ![pic](.\pic\11-3.png)
 ![pic](.\pic\11-4.png)
 ![pic](.\pic\11-5.png)
 ![pic](.\pic\11-6.png)

（12）实测效果。
 ![pic](.\pic\12.png)



以上简单回顾。

参考资料：
[源码]
Translate.cs
IsChildOf.cs
Log.cs