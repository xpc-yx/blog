---
title: 谈谈QT和OpenGL
tags:
  - CGAL
  - OpenGL
id: 953
categories:
  - 图形学
  - OpenGL
date: 2013-11-07 17:47:33
---

最近用了点时间学习了QT，重新阅读了下OpenGL超级宝典第四版，并且基本阅读完了。坑爹的是看完了第四版居然在网上发现了已经可以下载第五版的中文版了。翻阅了下第五版的目录，发现作者已经把GPU编程融合到整本书里面去了。而不像第四版和第三版那样只是分出几张做些介绍而已。我以前在图书馆借了本OpenGL编程宝典第三版，居然只有第三版（PS：我堂堂大中南的图书馆也该更新下了，真不明白图书馆买那么多不需要的办公室软件书籍作甚，整个图书馆只能索引到3本qt相关的书籍），里面居然还有用汇编语言形式的GPU底层着色操作。这个在第四版就去掉了。第五版我没有仔细阅读。以后有时间的话，还是阅读下第五版的内容吧。接下来，也不打算继续看Qt的东西了，毕竟界面编程这种东西，看多了没意义。我毕竟用了几年的MFC，看qt这种封装的太好的东西跟看手册一样的，所以我还是不需要继续去背书了。。。
所以，接下来可能学习下着色语言的所谓橙皮书。也可能阅读英文原版的，毕竟我还没看过一本英文原版的书籍，也提高一下英语。还有要看看微分几何的书籍了。如果还有时间的话，看看数字图像处理，以及matlab的一些东西。
我还是回到标题吧。。。
前段时间，用MFC做了个交互式分割模型的程序，我用的CSplitWnd切分主窗口为三个视图。做这个界面的过程中，遇到最恶心的问题是，我的一个基于对话框的视图无法很好的自放缩子控件，也就是自动调整控件大小。不要跟我说在OnSize里面处理下就行了。不要告诉我再禁止掉滚动条。总之很难达到想要的结果。而且，代码会乱成一团，本来就不爽mfc框架生成的那么多代码。不要以为我在这里喷MFC，我毕竟是学MFC过来的，用了很多次。我以前的界面99%都是MFC做的。可以说是MFC养大了我，但是我慢慢发现我还是对MFC越来越不满了。
所以，我就去看Qt了。同学介绍有个豆子的空间里面关于qt的教程不错，我就把前面的大部分看了一遍，并且都把代码提取出来，全部整合到一个工程里面实验了一下。总之，发现qt还不错吧。至少对于前面的那个问题，qt里面非常好解决，因为它有水平布局和垂直布局的概念。
至于Qt和Opengl的结合，也非常简单。直接继承QGLWidget，实现几个函数就行了。qt5还提供了增强版本的3d类QGLView。这里我要说的是libQglviewer。这个是在qt上的一个增强opengl渲染C++库。封装了很多默认的功能，非常强大。cgal上面的qt框架的3d显示就是推荐的这个东西。
至于模型加载，我打算试试Assimp，用这个加载模型之后，提取出数据，再来初始化cgal的数据结构。这样就不用处理各种烦人的obj,m格式等等了。。。
估计下一个需要渲染的东西就是用这些东西实现了吧。