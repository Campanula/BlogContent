---
date: 2017-01-21T15:28:18+08:00
tags: ["markdown","test"]
title: markdown练习
topics: ""
---

# 一级标题

## 二级标题

###### 六级标题

---

> 试一试。

>      试一试。 //引用和缩进的简单组合--引用中的代码
试一试。

更多实验

> 引用注释
>      前面五个空格 //无回车


回车实验

> xxx
>
> 隔行实验

---
*斜体*
_斜体_

**粗体**
__粗体__

_**斜粗体实验**_
__*斜粗体实验*__
***粗斜体实验***

~~长长长长长的删除线~~

---
* 列表
+ listplus
- listreduce
 + 子列表
     + 三级子列表
     + 三级子列表
+ + 子子列表
 + 子子列表

---
1. 有序列表
2. 有序列表
3.无空格实验（标号后面无空格为普通文本）
4. 行号为4，再次有空格

---
[百度链接](http://www.baidu.com "百度")
[百度链接有空格]   (http://www.baidu.com "百度")

I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].

[1]: http://google.com/        "Google" 
[2]: http://search.yahoo.com/  "Yahoo Search" 
[3]: http://search.msn.com/    "MSN Search"

---

试一下行内公式：`$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$`

<div>$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$</div>

<div>$$y(x)=\int \theta(x)\mathrm{d}x + C_2 =\int \left(\int \frac{M(x)}{EI} \mathrm{d}x + C_1 \right)\mathrm{d}x + C_2 \tag{2-4}$$</div>

---

试试行内代码，`hugo server`用于启动网站。`hugo`本身则会生成`public`文件夹，文件夹内是静态网页内容。

试试图片

{{< img src="/img/night-moon.png" title="Night Moon" >}}

{{< img src="/img/night-moon.png" position="right" title="Night Moon" >}}

总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈

{{< img src="/img/moon.jpg" position="left" title="Moon" caption="何夜无月" >}}

总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈

{{< img src="/img/night-moon.png" position="right" title="Night Moon" >}}

总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈，总想搞前端的后端多半是个假全栈

---

{{< code "C++" >}}
#include <iostream>
using namespace std;
// just a test
void main()
{
    cout << "Hello World!" << endl;
}
void main()
{
    cout << "Hello World!" << endl;
}
void main()
{
    cout << "Hello World!" << endl;
}
void main()
{
    cout << "Hello World!" << endl;
}
{{< /code >}}