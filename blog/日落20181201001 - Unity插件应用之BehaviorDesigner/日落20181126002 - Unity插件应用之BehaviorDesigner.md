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

（10-1）并行节点（Parallel）作为主节点，让子节点从左到右都执行。

（10-2）并行节点的右边子节点是选择节点，选择节点从左到右访问子节点，遇到返回True的子节点则执行，其他子节点不执行。

（10-3）然后说说选择节点的子节点，其左边和中间节点都采用序列节点，序列节点从左到右访问子节点，若遇到返回True的子节点则执行，而一旦遇到返回False的子节点不再执行此节点以及其后子节点。

（11）行为树节点设置详情如下。
 ![pic](.\pic\11-1.png)
 ![pic](.\pic\11-2.png)
 ![pic](.\pic\11-3.png)
 ![pic](.\pic\11-4.png)
 ![pic](.\pic\11-5.png)
 ![pic](.\pic\11-6.png)

（12）实测效果。
 ![pic](.\pic\12.gif)



以上简单回顾。

参考资料：

行为树（Behavior Tree）实践（1）– 基本概念
http://www.aisharing.com/archives/90

行为树（Behavior Tree）实践（2）– 进一步的讨论
http://www.aisharing.com/archives/99

[源码]
Translate.cs
IsChildOf.cs
Log.cs