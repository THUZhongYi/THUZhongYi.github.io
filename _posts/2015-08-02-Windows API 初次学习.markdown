---
layout: post
title:  "Windows API 初次学习"
tags: [windows-api]
---

前段时间有一个手机游戏很火，叫做Crossy Road，我也玩了很久。在玩的过程中为了玩的更好，我思考了关于这个游戏的原理的问题，从而萌生了在Windows下写这个游戏的一个简易版的念头。
贴一张游戏截图：

<img src="http://vignette3.wikia.nocookie.net/crossyroad/images/8/8c/Baby_Duck.png/revision/latest?cb=20150226113948">

哦不，贴错了=。=，这是其中一个角色Baby duck

<img src="http://www.gamezebo.com/wp-content/uploads/2015/02/CrossyRoad_InAction_Dragon.jpg">

这才是游戏截图...

所以我开始了解Windows游戏开发的知识，第一个遇到的需要克服的大块是Direct3D，然后在MSDN上找到了怎么使用Direct3D绘制界面以及编写小游戏的简单程序演示，在这里就遇到了第二个需要克服的大块。在Direct3D之前，必须先要学会使用Windows API编写基本的Windows程序的框架，了解Windows窗口的基本原理。所以就有了下面将提到的一些基本知识，而这篇文章就是一个非常基础的Windows API的初尝体验。

编写Windows应用程序时，必须（至少对于一般人来说）通过Windows API才能够实现对于Windows系统的基础服务和图形接口等等的调用。

先创建一个空的C++工程。

{% highlight c++ linenos %}
//include部分
#include <Windows.h>
#include <stdlib.h>
#include <string.h>
#include <tchar.h>
#include "resource.h"

//然后定义两个全局常量
//the main window class name
static TCHAR szWindowClass[] = _T("Win32Demo1");
//the string appears in the title bar
static TCHAR szTitle[] = _T("Win32 Guided Tour Application");
{% endhighlight %}

和最基本的C++程序不同的是，Win32程序的核心函数是WinMain函数，而且必须指定其调用方式WINAPI，所以定义的规范写法是：
{% highlight c++ linenos %}
    int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow)
//下面我们进入WinMain函数的函数体
{
//首先必须明确一种窗口结构，并且对它进行register。所谓register，就是把必须指定的成员都显式指定。
    WNDCLASSEX wcex;
    wcex.cbSize = sizeof(WNDCLASSEX);
    wcex.style = CS_HREDRAW | CS_VREDRAW;
    wcex.lpfnWndProc = WndProc;    
    wcex.cbClsExtra = 0;
    wcex.cbWndExtra = 0;
    wcex.hInstance = hInstance;
    wcex.hIcon = LoadIcon(GetModuleHandle(NULL), MAKEINTRESOURCE(IDI_MYICON));
    wcex.hCursor = LoadCursor(NULL, IDC_ARROW);
    wcex.hbrBackground = (HBRUSH)(COLOR_WINDOW + 1);
    wcex.lpszMenuName = MAKEINTRESOURCE(IDR_MYMENU);
    wcex.lpszClassName = szWindowClass;
    wcex.hIconSm = (HICON)LoadImage(GetModuleHandle(NULL), MAKEINTRESOURCE(IDI_MYICON),IMAGE_ICON, 16,16,0);

//然后我们检查register是否成功
    if (!RegisterClassEx(&wcex)) {
        MessageBox(
            NULL,
            _T("Call to RegisterClassEx failed!"),
            _T("Win32 Guided Tour"),
            NULL);
        return 1;
    }

//接下来生成一个具体的窗口实例
    HWND hWnd = CreateWindow(
        szWindowClass,
        szTitle,
        WS_OVERLAPPEDWINDOW,
        CW_USEDEFAULT, CW_USEDEFAULT,
        500, 500,
        NULL,
        NULL,
        hInstance,
        NULL
        );

//检查窗口实例有没有正确产生
    if (!hWnd) {
        MessageBox(
            NULL,
            _T("Call to CreateWindow failed!"),
            _T("Win32 Guided Tour"),
            NULL);
        return 1;
    }

//窗口实例按照我们输入的参数和上面指定的窗口结构正确产生之后，就可以显示了
    ShowWindow(
        hWnd,
        UpdateWindow(hWnd));

//最后是整个程序的一个核心组件，消息监听循环
    MSG msg;
    while (GetMessage(&msg, NULL, 0, 0)>0) {
        TranslateMessage(&msg);
        DispatchMessage(&msg);
    }

//最终返回一个值
    return (int)msg.wParam;
}
{% endhighlight %}
WinMain函数至此结束。

需要注意的是，我们在WinMain函数中经常用到的一个函数WndProc必须在WinMain函数定义之前先声明一下：
{% highlight c++ linenos %}
LRESULT CALLBACK WndProc(HWND, UINT, WPARAM, LPARAM);
{% endhighlight %}

在定义完WinMain函数之后，必须定义WndProc函数，这个函数是用来处理程序所收到的消息的，也就是定义响应方式的地方。
{% highlight c++ linenos %}
LRESULT CALLBACK WndProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam){

    PAINTSTRUCT ps;
    HDC hdc;
    TCHAR greeting[] = _T("Hello, World!");

    switch (message) {
        case WM_LBUTTONDOWN: {
        TCHAR szFileName[MAX_PATH];
        HINSTANCE hInstance = GetModuleHandle(NULL);
        GetModuleFileName(hInstance, szFileName, MAX_PATH);
        MessageBox(hWnd, szFileName, szFileName, MB_OK | MB_ICONINFORMATION);
        }
            break;
        case WM_RBUTTONDOWN: {
            PostMessage(hWnd, WM_CLOSE, 0, 0);
            break;
        }
        case WM_PAINT:
            hdc = BeginPaint(hWnd, &ps);
            TextOut(hdc, 5, 5, greeting, _tcslen(greeting));
            EndPaint(hWnd, &ps);
            break;
        case WM_DESTROY:
            PostQuitMessage(0);
            break;
        default:
            return DefWindowProc(hWnd, message, wParam, lParam);
            break;
    }
    return 0;
}
{% endhighlight %}
在上面的响应中，定义了：
<ul>
<li>左键——弹出一个窗口显示这个程序所在路径</li>
<li>右键——关闭窗口</li>
<li>“画”界面——显示Hello, World!</li>
<li>销毁——关闭窗口</li>
<li>以及默认操作</li>

<br>

需要指出的是，上面的程序还尝试地加入了顶部菜单和程序图标。这个特性是在register的时候，在关于Menu和Icon的成员处指定的。而关于如何加入菜单，我将在仔细学习之后另外写一篇文章，现在需要说明的是，需要在Headers中加入自己编写的resource.h，在Resources中加入自己编写的Resource.rc，并且include进main.cpp，才能实现菜单和图标。

这就是一个很简单的利用Windows API创建的Win32窗口程序，具有很有限的响应功能。


