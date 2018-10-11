系统：Windows 10
引擎：Unity 2017.2.1f1
插件：Easy Touch 5.0.17

（1）首先设置布局如下

 ![1](.\pic\1.png)

（2）然后是TouchController.cs的脚本内容如下

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using HedgehogTeam.EasyTouch;

public class TouchController : MonoBehaviour {

	public Text m_Text;
    public Transform m_Transform;

    public float m_MinScale = 10f;
    public float m_MaxScale = 20f;
    public float m_ScaleSpeed = 1f;
    public float m_MoveSpeed = 10f;

    private Vector3 _deltaPosition;
    private Gesture _currentGesture;

    //*/ ----------------- Easy Touch 4 -----------------
	void OnEnable() 
	{
        EasyTouch.On_TouchStart += this.On_TouchStart;
        EasyTouch.On_TouchDown += this.On_TouchDown;
        EasyTouch.On_Twist += this.On_Twist;
        EasyTouch.On_PinchIn += this.On_PinchIn;
        EasyTouch.On_PinchOut += this.On_PinchOut;
    }

    void OnDisable() 
    {
        EasyTouch.On_TouchStart -= this.On_TouchStart;
        EasyTouch.On_TouchDown -= this.On_TouchDown;
        EasyTouch.On_Twist -= this.On_Twist;
        EasyTouch.On_PinchIn -= this.On_PinchIn;
        EasyTouch.On_PinchOut -= this.On_PinchOut;
    }
    //*/


    /*/ ----------------- Easy Touch 5 -----------------
    void Update() 
    {
    	_currentGesture = EasyTouch.current;
    	if (_currentGesture == null)
    	{
    		return;
    	}

    	if (EasyTouch.EvtType.On_TouchStart == _currentGesture.type)
    	{
    		this.On_TouchStart(_currentGesture);
    	}
    	else if (EasyTouch.EvtType.On_TouchDown == _currentGesture.type)
    	{
    		this.On_TouchDown(_currentGesture);
    	}
    	else if (EasyTouch.EvtType.On_Twist == _currentGesture.type)
    	{
    		this.On_Twist(_currentGesture);
    	}
    	else if (EasyTouch.EvtType.On_PinchIn == _currentGesture.type)
    	{
    		this.On_PinchIn(_currentGesture);
    	}
    	else if (EasyTouch.EvtType.On_PinchOut == _currentGesture.type)
    	{
    		this.On_PinchOut(_currentGesture);
    	}
    }
    //*/

    void OnShowLog(string strLog)
    {
        Debug.Log(strLog);
        m_Text.text = strLog;
    }

    void On_TouchStart(Gesture gesture)
    {
        if (gesture.touchCount != 1)
            return;

        Vector3 position = gesture.GetTouchToWorldPoint(m_MoveSpeed);
        _deltaPosition = position - m_Transform.position;
        OnShowLog("TouchStart:" + _deltaPosition);
    }

    void On_TouchDown(Gesture gesture)
    {
        if (gesture.touchCount != 1)
            return;

        Vector3 oldPosition = gesture.GetTouchToWorldPoint(m_MoveSpeed);
        Vector3 newPosition = oldPosition - _deltaPosition;
        m_Transform.position = new Vector3(newPosition.x, 0f, newPosition.z);
        OnShowLog("TouchDown:" + oldPosition);
    }

    void On_Twist(Gesture gesture)
    {
        m_Transform.Rotate(new Vector3(0f, -gesture.twistAngle, 0f));
        OnShowLog("Twist:" + gesture.twistAngle);
    }

    void On_PinchIn(Gesture g)
    {
        float zoom = Time.deltaTime * g.deltaPinch * m_ScaleSpeed;
        Vector3 scale = m_Transform.localScale;

        float scale_x = Mathf.Max(m_Transform.localScale.x - zoom, m_MinScale);
        float scale_z = Mathf.Max(m_Transform.localScale.z - zoom, m_MinScale);
        m_Transform.localScale = new Vector3(scale_x, scale.y, scale_z);
    }

    void On_PinchOut(Gesture g)
    {
        float zoom = Time.deltaTime * g.deltaPinch * m_ScaleSpeed;
        Vector3 scale = m_Transform.localScale;

        float scale_x = Mathf.Min(scale.x + zoom, m_MaxScale);
        float scale_z = Mathf.Min(scale.z + zoom, m_MaxScale);
        m_Transform.localScale = new Vector3(scale_x, scale.y, scale_z);
    }

}

```

可以选择用Easy Touch 4写法，还是Easy Touch 5写法。测试一下，用Easy Touch 4的注册方式比较流畅，Easy Touch 5用法写在Update里，估计是受到频率影响。

（3）效果如下

 ![1](.\pic\2.png)

总结，UI上有个Raycast Target的勾选要注意，会挡掉触摸事件。



以上简单回顾。

参考资料：
Easy Touch 自带例子