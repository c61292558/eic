---
# 一个用Portfolio widget创建的页面集。
# This section displays content from `content/project/`.
# 查阅 https://wowchemy.com/docs/widget/portfolio/
widget: portfolio

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 20

title: '我是一名deepiner，这是我的博客'
subtitle: ''

content:
  # Page type to display. E.g. project.
  page_type: project

  # Default filter index (e.g. 0 corresponds to the first `filter_button` instance below).
  filter_default: 0

  # Filter toolbar (optional).
  # Add or remove as many filters (`filter_button` instances) as you like.
  # To show all items, set `tag` to "*".
  # To filter by a specific tag, set `tag` to an existing tag name.
  # To remove the toolbar, delete the entire `filter_button` block.
  filter_button:
    - name: 全部
      tag: '*'
    - name: Deepin
      tag: deepin
    - name: GUI
      tag: GUI
    - name: CAD
      tag: CAD 
    - name: 其他
      tag: Others

design:
  columns: '1'
  view: cards #除了showcase，还有basic（好丑），carousel（以轮播的形式展示内容），mosaic（以瀑布流的形式展示内容）
  flip_alt_rows: true
  background: {}
  spacing: {padding: [0, 0, 0, 0]}
---
