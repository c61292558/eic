---
title: 幻灯片测试
summary: 关于使用Wowchemy的幻灯片功能的介绍。
authors: []
tags: ['幻灯片']
categories: [hugo]
date: '2019-02-05'
slides:
  
  theme: black 
  highlight_style: dracula
---

# 幻灯片演示文章

[Wowchemy](https://wowchemy.com/) | [文档](https://wowchemy.com/docs/content/slides/)

---

## 特点

- 高效地用Markdown编写幻灯片
- 3合1：创建、展示和发布你的幻灯片
- 支持演讲者注释
- 对移动端平台友好的幻灯片

---

## 控制

- Next: `Right Arrow` or `Space`
- Previous: `Left Arrow`
- Start: `Home`
- Finish: `End`
- Overview: `Esc`
- Speaker notes: `S`
- Fullscreen: `F`
- Zoom: `Alt + Click`
- [PDF Export](https://revealjs.com/pdf-export/)

---

## 代码高亮

内联代码: `variable`

代码块:

```python
porridge = "blueberry"
if porridge == "blueberry":
    print("Eating...")
```

---

## 数学公式

In-line math: $x + y = z$

Block math:

$$
f\left( x \right) = \;\frac{{2\left( {x + 4} \right)\left( {x - 4} \right)}}{{\left( {x + 4} \right)\left( {x + 1} \right)}}
$$

---

## 碎片

Make content appear incrementally

```
{{</* fragment */>}} $\mathbf{y} =  $ {{</* /fragment */>}}
{{</* fragment */>}} $X\boldsymbol\beta$ {{</* /fragment */>}}
{{</* fragment */>}} $+ \boldsymbol\varepsilon$ {{</* /fragment */>}}
```

Press `Space` to play!

{{< fragment >}} $\mathbf{y} =  $ {{< /fragment >}}
{{< fragment >}} $X\boldsymbol\beta$ {{< /fragment >}}
{{< fragment >}} $+ \boldsymbol\varepsilon$ {{< /fragment >}}

---

A fragment can accept two optional parameters:

- `class`: use a custom style (requires definition in custom CSS)
- `weight`: sets the order in which a fragment appears

---

## Speaker Notes

Add speaker notes to your presentation

```markdown
{{%/* speaker_note */%}}

- Only the speaker can read these notes
- Press `S` key to view

{{%/* /speaker_note */%}}
```

Press the `S` key to view the speaker notes!

{{< speaker_note >}}

- Only the speaker can read these notes
- Press `S` key to view

{{< /speaker_note >}}

---

## Themes

- black: Black background, white text, blue links (default)
- white: White background, black text, blue links
- league: Gray background, white text, blue links
- beige: Beige background, dark text, brown links
- sky: Blue background, thin dark text, blue links

---

- night: Black background, thick white text, orange links
- serif: Cappuccino background, gray text, brown links
- simple: White background, black text, blue links
- solarized: Cream-colored background, dark green text, blue links

---

{{< slide background-image="boards.webp" >}}

## Custom Slide

Customize the slide style and background

```markdown
{{</* slide background-image="boards.webp" */>}}
{{</* slide background-color="#0000FF" */>}}
{{</* slide class="my-style" */>}}
```

---

## Custom CSS Example

Let's make headers navy colored.

Create `assets/css/reveal_custom.css` with:

```css
.reveal section h1,
.reveal section h2,
.reveal section h3 {
  color: navy;
}
```

---

# Questions?

[Ask](https://discord.gg/z8wNYzb)

[Documentation](https://wowchemy.com/docs/content/slides/)