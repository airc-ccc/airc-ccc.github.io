---
layout: post
title:  "Oculus Unity Step Three"
date:   2022-11-27
categories: VR, Unity, Oculus Quest2
comments: true
---

# Oculus Unity
```
接下来，主要围绕阅读器的部分进行开发
```


## Script
----
### Setup
- 新建一个C#脚本Component，把他Add到一个GameObject上
- 编辑该脚本，监听一个你需要的Key来进行操作
- 创建一个内容承载GameObject (TextMeshPro) Text，这里需要操作一下Unity，使它支持简体中文
- 然后根据Unity教程：操作TextMeshPro组件，进行内容更新替换


### 额外的操作
这里利用操作组件的方法，可以改变Ball的颜色以及复制Ball，GameObject的操作

{% highlight c# %}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using TMPro;

public class GreaterBall : MonoBehaviour
{

    public GameObject redball;


    public GameObject player;

    public int chapterId = 0;

    public string[] content = 
        { 
            "我叫邢云， “不做亏心事，不怕鬼敲门”这句话是我的座右铭。 但是男人活着有很多无奈的时候，我就做了一件亏心事，随后的事情惊心动魄。",
            "二零零八年的时候，父亲生病急需用钱，被逼无奈，我托朋友在南方找到了一个在江里打捞尸体的工作。虽然活儿有点脏，但是挣钱不少。" ,
            "这工作不仅危险，还很辛苦，尤其还会经常遇到一些科学解释不了的事情，但我一点不迷信。有时候累了，只要想起父母妻儿，我的心里就觉得暖暖的，干劲十足。",
            "那年6月，暴雨导致200多公里以外的上游突发洪灾，我创下一个星期里打捞上70多具尸体的“奇迹”。除了自然灾害导致的事故之外，其他的溺水者主要以女性为主，从农村到城里打工的女性民工尤其多。"
        };

    public GameObject novelContent;

    // Start is called before the first frame update
    void Start()
    {
        Debug.Log("Hello,GreateerBall");

        novelContent = GameObject.Find("novel_content");
    }

    // Update is called once per frame
    void Update()
    {
        if (OVRInput.GetDown(virtualMask: OVRInput.Button.One))
        {
            ReadNovel();
        }

        if (OVRInput.GetDown(virtualMask: OVRInput.Button.Two))
        {
            ProvChapter();
        }

        if (OVRInput.GetDown(virtualMask: OVRInput.Button.Three))
        {
            NewBall();
        }


        if (OVRInput.GetDown(virtualMask: OVRInput.Button.Four))
        {
            ChangeBall();
        }
    }


    void ReadNovel()
    {
        novelContent.GetComponent<TextMeshPro>().text = content[chapterId];
        chapterId++;
    }


    void ProvChapter()
    {
        if (chapterId > 0)
        {
            chapterId--;
            novelContent.GetComponent<TextMeshPro>().text = content[chapterId];
        }
    }

    void ChangeBall()
    {
        redball = GameObject.Find("ball");
        redball.GetComponent<MeshRenderer>().material.color = RandomColor();
    }


    void NewBall()
    {
        Instantiate(redball,new Vector3(redball.transform.position.x * 2.0f, 0, 0), Quaternion.identity);
    }

    Color RandomColor()
    {
        float r = Random.Range(0f, 1f);
        float g = Random.Range(0f, 1f);
        float b = Random.Range(0f, 1f);
        Color color = new Color(r, g, b);
        return color;
    }
}
{% endhighlight %}