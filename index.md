---
cover: auto
title: ppt
subtitle: 把 markdown 变成一场演讲
author: x-cmd
date: 2026-10-31
---

<!-- .slide: data-layout="gallery" -->

# 演示

一份 markdown = 一场演讲。下面每一张都是真 deck 的封面,**点一下就开讲**。

<div class="ppt-gallery">
<a href="https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md"><img src="https://po6.sh/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md" alt="把 markdown 变成一场演讲"></a>
<a href="https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/quickstart.md"><img src="https://po6.sh/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/quickstart.md" alt="五分钟:写 deck 的语法速查"></a>
<a href="https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/charts.md"><img src="https://po6.sh/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/charts.md" alt="封面图与内联图表的玩法"></a>
<a href="https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/draw.md"><img src="https://po6.sh/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/draw.md" alt="draw:把数据变成一张图"></a>
<a href="https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/dbnomics.md"><img src="https://po6.sh/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/dbnomics.md" alt="dbnomics:经济学,就是一条条链接"></a>
</div>

---

# 这个项目在做什么

- **输入**:一个 markdown 链接(`?url=`),或一段原文(`?data=`)
- **输出**:一场 reveal.js 演讲,外加一页页的 SVG 封面图
- **服务端只解决跨域**:markdown 由服务端代取,幻灯片在浏览器里现场渲染
- **图表内联**:markdown 里的 ```draw 围栏或 draw 链接,服务端展开成原生 SVG(可点)

```text
https://x-cmd.com/ppt?url=<markdown 链接>
https://x-cmd.com/ppt/cover.svg?url=<markdown 链接>
```

---

# 怎么开始写

```markdown
---
cover: auto
title: 我的演讲
subtitle: 一句话说明
author: 我
date: 2026-10-31
---

# 第一页

正文。
```

`---` 横向分页 · `--` 纵向分页 · `Note:` 演讲者备注 · `<!-- .slide: data-layout="section" -->` 每页版式。
