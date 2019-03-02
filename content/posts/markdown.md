---
title: "Markdown语法手册"
date: 2019-03-01T19:36:47+08:00
draft: false
categories: ["技能学习"]
tags: ["Markdown"]
---

# Markdown 简明语法手册

---

### 1. 斜体和粗体

使用 `*`(`_`) 和 `**`(`_ _`) 表示斜体和粗体。

示例：

这是*斜体*，这是**粗体**。

### 2. 分级标题

使用任意个 = 表示一级标题，使用 - 表示二级标题，不过一共只能表示两级。

示例：

```html
这是一个一级标题
==============

这是一个二级标题
--------------
```

这是一个一级标题
=============

这是一个二级标题
-------------

你也可以选择在行首加井号表示不同级别的标题 (H1-H6)，例如：# H1，## H2，### H3，#### H4，##### H5，###### H6。

### 3. 外链接

使用 \[描述](链接地址) 为文字增加外链接。

示例：

这是 [本人博客](https://yeqiongzhou.top) 的链接。

### 4. 无序列表

使用 *，+，- 表示无序列表。

示例：

- 无序列表项 一
- 无序列表项 二
- 无序列表项 三

### 5. 有序列表

使用数字和点表示有序列表。

示例：

1. 有序列表项 一
2. 有序列表项 二
3. 有序列表项 三

### 6. 文字引用

使用 > 表示文字引用。

示例：

> Talk is cheap. Show me the code.

### 7. 行内代码块

使用 \`代码` 表示行内代码块。

示例：

让我们聊聊 `Kubernetes`。

### 8. 代码块

使用四个缩进空格表示代码块。

示例：

    这是一个代码块，此行左侧有四个不可见的空格哟。

### 9. 插入图像

使用 \!\[描述](图片链接地址) 插入图像。

示例：

![我的头像](http://img.yeqiongzhou.top/avatar.jpg)

# Markdown 高阶语法手册

---

### 1. 内容目录(注：GitHub Markdown 不支持`[TOC]`目录)

在段落中填写 `[TOC]` 以显示全文内容的目录结构。

![目录](http://img.yeqiongzhou.top/toc.png)

### 2. 标签分类

在编辑区任意行的列首位置输入以下代码给文稿标签：

标签： Docker Kubernetes Markdown

或者

Tags： Docker Kubernetes Markdown

### 3. 删除线

使用 ~~ 表示删除线。

~~这是一段错误的文本。~~

### 4. 注脚

使用 [^keyword] 表示注脚。

这是一个注脚[^footnote]的样例。

这是第二个注脚[^footnote2]的样例。

### 5. LaTeX 公式(注：GitHub Markdown 不支持 LaTeX 公式)

$ 表示行内公式：

`$E=mc^2$`

质能守恒方程可以用一个很简洁的方程式来表达。

![](http://img.yeqiongzhou.top/gs1.png) 

$$ 表示整行公式：

`$$\sum_{i=1}^n a_i=0$$`

`$$f(x_1,x_x,\ldots,x_n) = x_1^2 + x_2^2 + \cdots + x_n^2 $$`

`$$\sum^{j-1}_{k=0}{\widehat{\gamma}_{kj} z_k}$$`

![](http://img.yeqiongzhou.top/gs2.png)

访问 [MathJax](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference) 参考更多使用方法。

### 6. 加强的代码块

支持四十一种编程语言的语法高亮的显示，行号显示。

非代码示例：

```
$ sudo apt-get install vim-gnome
```

Python 示例：

```python
@requires_authorization
def somefunc(param1='', param2=0):
    '''A docstring'''
    if param1 > param2: # interesting
        print 'Greater'
    return (param2 - param1 + 1) or None

class SomeClass:
    pass

>>> message = '''interpreter
... prompt'''
```

JavaScript 示例：

``` javascript
/**
* nth element in the fibonacci series.
* @param n >= 0
* @return the nth element, >= 0.
*/
function fib(n) {
  var a = 1, b = 1;
  var tmp;
  while (--n >= 0) {
    tmp = a;
    a += b;
    b = tmp;
  }
  return a;
}

document.write(fib(10));
```

### 7. 流程图(注：GitHub Markdown 不支持流程图)

#### 示例

```flow
st=>start: Start:>https://yeqiongzhou.top
io=>inputoutput: verification
op=>operation: Your Operation
cond=>condition: Yes or No?
sub=>subroutine: Your Subroutine
e=>end
st->io->op->cond
cond(yes)->e
cond(no)->sub->io
```

![流程图示例](http://img.yeqiongzhou.top/flow.svg)

### 8. 序列图(注：GitHub Markdown 不支持序列图)

#### 示例 1

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

![序列图示例1](http://img.yeqiongzhou.top/seq1.svg)

#### 示例 2

```sequence
Title: Here is a title
A->B: Normal line
B-->C: Dashed line
C->>D: Open arrow
D-->>A: Dashed open arrow
```

![序列图示例2](http://img.yeqiongzhou.top/seq2.svg)

### 9. 甘特图(注：GitHub Markdown 不支持甘特图)

甘特图内在思想简单。基本是一条线条图，横轴表示时间，纵轴表示活动（项目），线条表示在整个期间上计划和实际的活动完成情况。它直观地表明任务计划在什么时候进行，及实际进展与计划要求的对比。

#### 示例

```gantt
title 项目开发流程
section 项目确定
    需求分析       :a1, 2016-06-22, 3d
    可行性报告     :after a1, 5d
    概念验证       : 5d
section 项目实施
    概要设计      :2016-07-05  , 5d
    详细设计      :2016-07-08, 10d
    编码          :2016-07-15, 10d
    测试          :2016-07-22, 5d
section 发布验收
    发布: 2d
    验收: 3d
```

![甘特图示例](http://img.yeqiongzhou.top/gantt.svg)

### 10. 表格支持

#### 示例

```html
| 项目        | 价格   |  数量  |
| --------   | -----:  | :----:  |
| 计算机     | $1600 |   5     |
| 手机        |   $12   |   12   |
| 管线        |    $1    |  234  |
```

| 项目        | 价格   |  数量  |
| --------   | -----:  | :----:  |
| 计算机     | $1600 |   5     |
| 手机        |   $12   |   12   |
| 管线        |    $1    |  234  |

### 11. 定义型列表

名词 1
:   定义 1（左侧有一个可见的冒号和四个不可见的空格）

代码块 2
:   这是代码块的定义（左侧有一个可见的冒号和四个不可见的空格）

        代码块（左侧有八个不可见的空格）

### 12. Html 标签

Markdown 语法中支持嵌套 Html 标签，譬如，你可以用 Html 写一个纵跨两行的表格：

#### 示例

```html
<table>
    <tr>
        <th rowspan="2">值班人员</th>
        <th>星期一</th>
        <th>星期二</th>
        <th>星期三</th>
    </tr>
    <tr>
        <td>李强</td>
        <td>张明</td>
        <td>王平</td>
    </tr>
</table>
```

<table>
    <tr>
        <th rowspan="2">值班人员</th>
        <th>星期一</th>
        <th>星期二</th>
        <th>星期三</th>
    </tr>
    <tr>
        <td>李强</td>
        <td>张明</td>
        <td>王平</td>
    </tr>
</table>

### 13. 待办事宜 Todo 列表

使用带有 [ ] 或 [x] （未完成或已完成）项的列表语法撰写一个待办事宜列表，并且支持子列表嵌套以及混用Markdown语法，例如：

- [ ] **博客开发**
    - [x] 增加黑白背景色切换功能
    - [x] 支持评论功能
    - [ ] 新增Todo列表功能 [语法参考](https://github.com/blog/1375-task-lists-in-gfm-issues-pulls-comments)
    - [ ] 改进 LaTex 功能
        - [ ] 修复 LaTex 公式渲染问题
        - [ ] 新增 LaTex 公式编号功能 [语法参考](http://docs.mathjax.org/en/latest/tex.html#tex-eq-numbers)
- [ ] **六月毕业旅行准备**
    - [x] 购买武汉到大阪来回的机票
    - [ ] 准备去往日本的签证
    - [ ] 浏览日本免税店的物品

[^footnote]: 这是一个 *注脚* 的 **文本**。

[^footnote2]: 这是另一个 *注脚* 的 **文本**。
