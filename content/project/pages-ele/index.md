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

```markdown
## Heading 2
### Heading 3
#### Heading 4
```

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

```
This is a {{< hl >}}highlighted quote{{< /hl >}}.
```

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
{{< spoiler text="Click to view the spoiler" >}}
You found me!
{{< /spoiler >}}
```
{{< spoiler text="Click to view the spoiler" >}}
You found me!
A
B
C
D
{{< /spoiler >}}



#### 链接到文件

---

**您可以在除Widget Pages(主页)之外的任何页面的页头中创建指向文件的按钮链接。**

否则，要链接到内容主体中的文件，例如PDF，请将该文件放在`static/uploads/`文件夹中，然后使用以下形式链接到该文件:

```
{{% staticref "uploads/cv.pdf" "newtab" %}}Download my CV{{% /staticref %}}
```

{{% staticref "uploads/cv.pdf" "newtab" %}}Download my CV{{% /staticref %}}

<!-- staticref的可选参数"newtab"将导致链接在新选项卡中打开。 -->

<!-- [I'm an external link](https://www.baidu.com) -->




