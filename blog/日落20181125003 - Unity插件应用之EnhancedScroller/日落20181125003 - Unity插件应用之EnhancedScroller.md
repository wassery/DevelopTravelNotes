## 环境
> 系统：Windows 10
> 引擎：Unity 2017.2.1f1
> 工具：Enhanced Scroller v2

## 目的
> 使用Enhanced Scroller制作一个简单实例。

（1）首先把场景布局如此
 ![pic](.\pic\1.png)

（2-1）添加脚本，单元格数据模型。M。
CellData.cs
```
public class CellData
{
    public int id;
    public string title;
    public string content;
}
```

（2-2）添加脚本，单元格显示设置。V。
CellView.cs
```
using UnityEngine;
using UnityEngine.UI;
using System.Collections;
using EnhancedUI.EnhancedScroller;

public delegate void OnClickCellDelegate(int value);

public class CellView : EnhancedScrollerCellView
{
    private CellData _data;
    public Text _text;

    public OnClickCellDelegate onClickCell;

    public void SetData(CellData data)
    {
        _data = data;
        _text.text = data.title;
    }

    public void Cell_OnClick()
    {
        if (onClickCell != null)
            onClickCell(_data.id);
    }
}
```

（2-3）添加脚本，滚动条管理器。C。
ScrollerManager.cs
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using EnhancedUI.EnhancedScroller;

public class ScrollerManager : MonoBehaviour, IEnhancedScrollerDelegate
{
    public EnhancedScroller m_Scroller;
    public CellView m_Cell;
    public Text m_Content;
    public RectTransform m_RectTransform;

    private List<CellData> _data;

    void Start()
    {
        InitData();

        m_Scroller.Delegate = this;
        m_Scroller.ReloadData();
    }

    private void InitData()
    {
        _data = new List<CellData>();
        for (int i = 0; i < 100; i++)
        {
            _data.Add(new CellData()
            {
                id = i + 1,
                title = "aaa-" + i.ToString(),
                content = "id:" + i.ToString()
            });
        }
    }

    public int GetNumberOfCells(EnhancedScroller scroller)
    {
        return _data.Count;
    }

    public float GetCellViewSize(EnhancedScroller scroller, int dataIndex)
    {
        return m_RectTransform.sizeDelta.y;
    }

    public EnhancedScrollerCellView GetCellView(EnhancedScroller scroller, int dataIndex, int cellIndex)
    {
        CellView cellView = scroller.GetCellView(m_Cell) as CellView;
        cellView.onClickCell = OnClickCell;
        cellView.SetData(_data[dataIndex]);

        return cellView;
    }

    private void OnClickCell(int id)
    {
        m_Content.text = _data[id].content;
    }
}
```

（3）场景对象Scroller的设置
 ![pic](.\pic\2.png)

（4）预制体Cell的设置
 ![pic](.\pic\3.png)

（5）预制体Cell的按钮设置
 ![pic](.\pic\4.png)

（6）场景对象ScrollerLoader的设置
 ![pic](.\pic\5.png)

（7）实测效果。
 ![pic](.\pic\6.png)

单元格设置得太小，手指很难选中...



以上简单回顾。

参考资料：
[官方例子]
01 - Quick Start Tutorial
09 Cell Events