---
layout: post
title:  "Learning markdown 1"
category: programming
tags: [markdown]
---

要制约的只有一些 HTML 区块元素――比如 <div>、<table>、<pre>、<p>等标签，必须在前后加上空行与其它内容区隔开，还要求它们的开始标签与结尾标签不能用制表符或空格来缩进。

这是一个普通段落。

<table>
    <tr>
        <td>Foo</td>
    </tr>
</table>

这是另一个普通段落。
和处在 HTML 区块标签间不同，Markdown 语法在 HTML 区段标签间是有效的。

我是一个小标题
=====

我是一个大标题
-----

#我是一种更好的大标题

#####我是一种更好的小小标题

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

>>我是更小的引用

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.


下面是列表啦
*blue
*green
*red

*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.

is better than

*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
Suspendisse id sem consectetuer libero luctus adipiscing.

*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.



当然，项目列表很可能会不小心产生，像是下面这样的写法：

1986. What a great season.

换句话说，也就是在行首出现数字-句点-空白，要避免这样的状况，你可以在句点前面加上反斜杠。

1986\. What a great season.


Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell

___
[This link](http://www.bdwm.net) has no title attribute.

This is [an example][id] reference-style link.

[id]:http://weibo.com "Optional title here"

链接内容定义的形式为：

    方括号（前面可以选择性地加上至多三个空格来缩进），里面输入链接文字
    接着一个冒号
    接着一个以上的空格或制表符
    接着链接的网址
    选择性地接着 title 内容，可以用单引号、双引号或是括弧包着

**need emphasized**

<em>emphasized</em>.\*this text is surrounded by literal asterisks\*

Use the `printf()` function.

```There is a literal backtick `` here.```

![Queen](http://attach3.bdwm.net/attach/0Announce/groups/GROUP_0/PersonalCorpus/T/triumph/D5F576B99//A6CD3D9C5/12.jpg)

&#160; &#160; &#160; &#160;下面编程语言（programming language），是用来定义计算机程序的形式语言。它是一种被标准化的交流技巧，用来向计算机发出指令。一种计算机语言让程序员能够准确地定义计算机所需要使用的数据，并精确地定义在不同情况下所应当采取的行动。[1] <br>&#160; &#160; &#160; &#160;最早的编程语言是在电脑发明之后产生的，当时是用来控制提花织布机及自动演奏钢琴的动作。在电脑领域已发明了上千不同的编程语言，而且每年仍有新的编程语言诞生。很多编程语言需要用指令方式说明计算的程序，而有些编程语言则属于声明式编程，说明需要的结果，而不说明如何计算。[1] <br>&#160; &#160; &#160; &#160;编程语言的描述一般可以分为语法及语义。语法是说明编程语言中，哪些符号或文字的组合方式是正确的，语义则是对于编程的解释。有些语言是用规格文件定义，例如C语言的规格文件也是ISO标准中一部份，2011年后的版本为ISO/IEC 9899:2011，而其他语言（像Perl）有一份主要的编程语言实现文件，视为是参考实现。[1] <br>&#160; &#160; &#160; &#160;编程语言俗称“计算机语言”，种类非常的多，总的来说可以分成机器语言、汇编语言、高级语言三大类。电脑每做的一次动作，一个步骤，都是按照已经用计算机语言编好的程序来执行的，程序是计算机要执行的指令的集合，而程序全部都是用我们所掌握的语言来编写的。所以人们要控制计算机一定要通过计算机语言向计算机发出命令。 目前通用的编程语言有两种形式：汇编语言和高级语言。[1] 

![Queen](http://ww2.sinaimg.cn/large/be5b4606jw1es1yqrdmeij21kw1kw7jr.jpg)

