---
title: Wowchemy上的页面元素Page Elements：Markdown, LaTeX, and Shortcodes（短代码）
summary: 
tags:
  - hugo
  - wowchemy
date: 2023-05-09

---
## wowchemy上的页面元素Page Elements：Markdown, LaTeX, and Shortcodes（短代码）。

可以使用**Markdown**、LaTeX math和**Shortcodes**在Wowchemy中编写丰富的内容。

>**短代码是与Wowchemy捆绑在一起或继承自Hugo的插件。此外，HTML可以编写在Markdown文档中以进行高级格式化。**

#### 子标题

---

```
## Heading 2
### Heading 3
#### Heading 4
```
## Heading 2
### Heading 3
#### Heading 4

#### 强调，粗体，斜体，删除线

---

<pre>
_underscores_
**asterisks**
**asterisks and _underscores_**
~~two tildes~~
</pre>

_underscores_

**asterisks**

**asterisks and _underscores_**

~~two tildes~~
#### 文本颜色（特有）

---

将样式为`{style="color: red"}`的HTML color属性添加到Markdown块后的行。

<pre>
Red colored text
{style="color: red"}
</pre>

Red colored text
{style="color: red"}

#### 区块引用

---

<pre>
> This is a blockquote.
</pre>

> This is a blockquote.

#### 高亮引用（特有）

---

<pre>
This is a {{< hl >}}highlighted quote{{< /hl >}}.
</pre>

This is a {{< hl >}}highlighted quote{{< /hl >}}.
#### 无序列表

---

<pre>
- First item
  - A sub-item
- Another item
</pre>

- First item
  - A sub-item
- Another item

#### Todo代办清单

---

通过使用标准Markdown语法，可以在Wowchemy中编写待办事项列表

<pre>
- [x] Write math example
  - [x] Write diagram example
- [ ] Do something else
</pre>

- [x] Write math example
  - [x] Write diagram example
- [ ] Do something else

#### 可折叠列表（特有）

---
向页面添加切换列表，以便在单击切换按钮后显示文本，例如问题的答案。
对于常见问题，剧透，或隐藏答案时，教学在线课程是很有用处的。
```
{{ < spoiler text="Click to view the spoiler" >}}//自行删除空格
You found me!
{{ < /spoiler >}}
```
{{< spoiler text="Click to view the spoiler" >}}
You found me!  
A  
B  
C  
D  
{{< /spoiler >}}
<pre>
[I'm an external link](https://www.baidu.com)
[A post]({{ < relref "/post/freecad" > }})
[A publication]({{ < relref "/publication/my-page-name" > }})
[A project]({{ < relref "/project/freecad/" > }})
[A relative link from one post to another post]({{ < relref "../my-page-name" > }})
[ Scroll down to a page section with heading *hugo wowchemy研究* ](#hugo wowchemy研究)
</pre>

[I'm an external link](https://www.baidu.com)  
[A post]({{ < relref "/post/freecad" > }})  
[A publication]({{ < relref "/publication/my-page-name" > }})  
[A project]({{ < relref "/project/freecad/" > }})  
[A relative link from one post to another post]({{ < relref "../my-page-name" > }})  
[ Scroll down to a page section with heading *hugo wowchemy研究* ](#hugo wowchemy研究)  


#### 链接到文件

---

**您可以在除Widget Pages(主页)之外的任何页面的页头中创建指向文件的按钮链接。**

否则，要链接到内容主体中的文件，例如PDF，请将该文件放在`static/uploads/`文件夹中，然后使用以下形式链接到该文件:

```
{{% staticref "uploads/cv.pdf" "newtab" %}}Download my CV{{% /staticref %}}
```

{{% staticref "uploads/cv.pdf" "newtab" %}}Download my CV{{% /staticref %}}

staticref的可选参数"newtab"将导致链接在新选项卡中打开。

#### 引用出版物

---

要引用一个页面或出版物，您可以使用引用短代码，引用您创建的文件夹和页面名称:

```
{{  < cite page="/publication/preprint" view="citation" >  }}
```

其中，视图对应于整个Wowchemy中使用的可用列表视图之一:

1. Stream
2. Compact
3. Card
4. Citation - 一个传统的学术引文, 通过在`params.yaml` 中设置`citation_style` 

如果你不指定视图，则默认为Compact精简视图。
#### 内容目录

---

目录可以帮助用户浏览冗长的页面。

粘贴这个`{{ < toc >}}`短代码无论在页面中的任何位置。

您可能还希望考虑使用[*book* layout](https://wowchemy.com/docs/content/docs/) 布局，它在大屏幕的右侧栏中显示内置的目录。

在使用book layout时，您可能仍然希望添加一个页内目录，该目录仅在隐藏右侧栏时显示。你可以使用```{{ < toc hide_on="xl" >}}```  

#### 脚注

---

<pre>
I have more [^1] to say.
[^1]: Footnote example.
</pre>

I have more [^1] to say.
[^1]: 脚注例子.

#### 图形

---

要交叉引用一个图形，请为其提供ID，例如:

```
 {{ < figure src="image.jpg" id="wowchemy" style="zoom:33%"> }}.
 
```

现在可以通过表单中的链接交叉引用该图形

```
[A Figure](#figure-wowchemy).
```
#### 标签和目录

---
<pre>
 使用`{{ < list tags > }}`来提供链接标签的列表，
 或者使用`{{ < list categories > }}`来提供链接类别的列表。 
</pre>
#### 文字-动作按钮

---

使用**CTA**短代码**创建按钮和调用操作**(CTA：Call-to-Action)。

