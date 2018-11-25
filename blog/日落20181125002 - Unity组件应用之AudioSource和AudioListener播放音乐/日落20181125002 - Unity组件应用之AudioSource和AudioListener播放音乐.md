## 环境
> 系统：Windows 10
> 引擎：Unity 2017.2.1f1

## 目的
> 使用Audio Source和Audio Listener播放微妙的音乐效果。

（1）首先把场景布局如此
 ![pic](.\pic\1.png)

（2）添加脚本文件。
AudioManager.cs
```
using UnityEngine;
using System.Collections;

public class AudioManager : MonoBehaviour {
	public AudioSource m_Music;
	public float m_VolumeChange = 0.01f;
	public float m_StereoChange = 0.05f;

	private bool isTurnLeft = true;
	private bool isTurnLow = true;

	void Start() {
		m_Music.panStereo = 0;
		m_Music.volume = 0.5f;
	}

	void Update() {
		UpdateStereo();
		UpdateVolume();
	}

	void UpdateVolume()
	{
		if (m_Music.volume >= 1)
			isTurnLow = true;
		else if (m_Music.volume <= 0.3f)
			isTurnLow = false;

		if (isTurnLow)
			m_Music.volume -= m_VolumeChange;
		else
			m_Music.volume += m_VolumeChange;
	}

	void UpdateStereo()
	{
		if (m_Music.panStereo >= 1)
			isTurnLeft = true;
		else if (m_Music.panStereo <= -1)
			isTurnLeft = false;

		if (isTurnLeft)
			m_Music.panStereo -= m_StereoChange;
		else
			m_Music.panStereo += m_StereoChange;
	}
}
```

（3）拉个mp3文件进工程。
 ![pic](.\pic\2.png)

（4）场景对象AudioLoader属性设置。
 ![pic](.\pic\3.png)

（5）实测效果，听...



以上简单回顾。

参考资料：
https://www.xuanyusong.com/archives/550