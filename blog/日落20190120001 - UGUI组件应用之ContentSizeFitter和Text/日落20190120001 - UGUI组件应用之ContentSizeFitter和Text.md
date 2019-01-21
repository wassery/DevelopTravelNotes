系统：Windows 10
引擎：Unity 2017.2.1f1



一、布局
 ![pic](.\pic\101.png)



二、搭配Horizontal Layout Group
（1）
 ![pic](.\pic\201.png)
其实Horizontal Layout Group换成Vertical Layout Group，使用相同的设置参数，也有相同效果。

（2）
 ![pic](.\pic\202.png)



三、搭配Vertical Layout Group
（1）
 ![pic](.\pic\301.png)

（2）
 ![pic](.\pic\302.png)



四、搭配Scroll View
（1）
 ![pic](.\pic\401.png)

（2）
 ![pic](.\pic\402.png)

（3）
 ![pic](.\pic\403.png)

（4）
 ![pic](.\pic\404.png)



五、加入控制
（1）
 ![pic](.\pic\401.png)

（2）
 ![pic](.\pic\502.png)

（3）
 ![pic](.\pic\503.png)

（4）
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class TextController : MonoBehaviour {

    public InputField m_input_field;
    public List<Text> m_text_list;
	
	void Update () {
        foreach (Text txtObj in m_text_list)
        {
            txtObj.text = m_input_field.text;
        }
    }
}
```

（5）
 ![pic](.\pic\505.png)



六、实测效果 
 ![pic](.\pic\601.gif)



以上简单回顾。

参考资料：
无