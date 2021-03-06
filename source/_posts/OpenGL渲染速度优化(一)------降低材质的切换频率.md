---
title: OpenGL渲染速度优化(一)------降低材质的切换频率
tags:
id: 1088
categories:
  - 图形学
  - OpenGL
date: 2014-02-24 17:27:23
---

在这里我只写我遇到过的一种情况。因为以前没有发现原因，好几个月的我的代码渲染速度都很慢，以至于最后被老师狠狠得说了一顿。最后，没办法了，我才通过仔细对比，一步步排查，发现了最终的原因。
说到渲染速度优化，大家肯定会说用**显示列表**啊。这个我知道，书上都有。我尝试过显示列表，但是还是解决不了我的问题。再一个，假如你写的是一个模型编辑的软件，**也就是渲染数据会发生变化的，那么用显示列表好像不太方便**。当然，肯定也能使用显示列表，数据改变的时候重新生成一次显示列表呗。
我用的界面框架是MFC，刚开始我以为是用MFC的原因导致渲染速度大幅度下降。但是，我对比过别人的MFC渲染程序，发现不存这样的事情。毕竟windows下的glut肯定是用windows api实现的，MFC只是多了层封装而已。那么原因在哪里了。
大家都知道我们在贴纹理的时候，需要在每个顶点处指定纹理坐标，但是这样做渲染速度也很快。假如把纹理换成颜色怎么样了。假设不同的顶点有各自的颜色，这种情况下，我们必须开启光照，然后不断设置不同顶点的材质。那么，这个速度和设置纹理坐标的速度相比怎么样了？
结果是慢得不行，基本上50w左右的顶点，连旋转都延迟了。谁让我以前都使用以k为数量级的模型了，一直没面对这个问题。
也许是纹理的实现比光照的实现要快很多。毕竟贴纹理得到最终像素的颜色，差不多就是双线性差值之类的方法。当然纹理的具体实现肯定要复杂很多，内容多很多。但是，光照的实现需要更复杂的计算公式。但是这就是真正的原因么？
我只是在一直切换顶点的材质而已，为什么比切换顶点的纹理坐标慢了至少10倍了。我针对这种情况修改了代码，将材质切换进行了判断，使材质切换大大减少了，渲染速度果断达到了要求，可以顺畅渲染**100w**以上的数据。
现在，我只能经验性的知道不能**频繁切换材质**，但是能频繁切换纹理坐标。具体原因，我就不深入探究了。也许得从渲染片段的顺序之类的讨论起吧。
另外谈一下优化代码速度的关键，别磨磨蹭蹭想其它的原因了，直接去找一直在哪里**循环执行**的东西吧。优化循环或者循环被调用的东西吧。