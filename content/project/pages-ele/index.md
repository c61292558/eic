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

<pre>
This is a {{< hl >}}highlighted quote{{< /hl >}}.
</pre>

This is a {{< hl >}}highlighted quote{{< /hl >}}.