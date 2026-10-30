---
template: deck
theme: black
cover:
  title: 把 markdown 变成一场演讲
  subtitle: 一个长链接就是入口
  author: x-cmd
  date: 2026-10-31
---

<!-- .slide: data-layout="title" -->

# 把 markdown 变成一场演讲

**一个长链接就是入口** —— 贴进 README,别人点开就能讲。

`https://x-cmd.com/ppt`

---

# markdown 早就写好了,演讲还没准备好

AI 十分钟写完一份 deck,然后呢?

- 装工具、导 PDF、改样式 —— 一遍遍重来
- 分享出去的是**文件**,不是**内容**

--

## 换个问法

> markdown 已经躺在仓库里 —— 能不能**只把它的地址贴出来**,别人点开就能讲?

把渲染搬到**浏览器**,把输入缩成**一个地址**。

---

# 一个链接,一场演讲

```text
https://x-cmd.com/ppt?url=<markdown 链接>
```

贴进 README,别人点开就能讲。

--

## 封面就是一张 SVG

<a href="https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md"><img src="https://po6.sh/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md" width="300" alt="本 deck 的封面"></a>

服务端把封面那页排成 SVG —— 矢量、可缩放、能放进 README。

点它 → 打开这份演示。尺寸用 HTML 的 `width` 属性控制。

--

## 三个现成的案例

- **本 deck** —— 把 markdown 变成一场演讲
- **五分钟** —— 写 deck 的语法速查
- **图表** —— 封面图与内联图表的玩法

---

# 它是一个 webapp,不是一个 action

| | draw | ppt |
|---|---|---|
| 输入 | 数据(参数) | **链接** |
| 输出 | 一张图 | **一场演讲** |
| 渲染 | 服务端 | **浏览器** |

--

## datalink:输入是地址

内容通常**已经在仓库里**了 —— 用户只想贴它的地址。

接口只认一样东西:

```text
/ppt?url=<markdown 的地址>
```

---

# 原理

服务端只出 HTML 壳:

1. 浏览器取 markdown(经同源代理)
2. reveal.js 切页、渲染

幻灯片是**活的** —— 主题、翻页、备注、打印 PDF,全是 reveal.js 原生能力。

--

## 同源代理

源站大多**不发 CORS 头**,浏览器直接取会被拦。

服务端 fetch 不受同源策略约束 → 代取 → 以**同源**身份交给浏览器。

后台成了出口,所以要守边界:

- 只允许 `http/https`
- 拒绝内网 / 回环 / 云元数据
- 限体积、跳数、超时、频率

--

## 取过一次就够了

备注窗口(`S`)会再开一个接收端页面,它本会**再取一次** markdown。

前端把取到的内容存进 `localStorage`(同源共享),之后一律用缓存 —— 不再回源。

---

# 封面图

reveal.js **没有**服务端渲染能力 —— 后台只把**指定的那一页**排成 SVG:

- 画布 960×700
- 字号 / 行高 / 间距 / 颜色 —— 取自主题 CSS
- 行盒模型照抄浏览器

于是封面图与浏览器里那一页**看着一样**。

--

## 测量与渲染同源

折行点要跟浏览器一致,量宽就得用**同一份字体**:

- 内嵌字体子集进 SVG(`<img>` 引用时取不到外部字体)
- 同一份字体的**字宽表**用于排版

测量的字,就是渲染的字。

--

## 也能是一段动画

```text
/ppt/cover.svg?url=…&anim=0,2,5&freeze=5
```

SVG 内嵌 **SMIL** 动画;不支持动画时,看到的就是**定格的那一页**。

---

# 图表

服务端把围栏展开成**内联 SVG** —— 矢量、可缩放,不是图片:

```draw
type=bar&t=xcmd&labels=Jan,Feb,Mar,Apr&values=12,19,14,23&w=560&h=300&title=月度活跃
```

--

## 或者贴 draw 的链接

[![各模块行数](https://x-cmd.com/draw?type=bar&t=xcmd&labels=排版,取数,路由,页面&values=615,272,263,327&w=560&h=300)](https://x-cmd.com/draw/explore?type=bar&t=xcmd&labels=排版,取数,路由,页面&values=615,272,263,327)

指向图表服务的图片,同样会被内联成原生 SVG。

外面套一层链接 → **点图跳到别处**(这里是 draw 的 explore:悬停看数、改参数)。

---

# 版面模板

| 模板 | 版面 |
|---|---|
| `deck` | 经典左对齐,列表不挂圆点(默认) |
| `center` | 一切居中,列表不挂圆点 |
| `plain` | reveal.js 原样 |

```text
/ppt?url=<链接>&template=center
```

---

<!-- .slide: data-layout="end" -->

# 现在就去讲一场

把地址贴出来,别人点开就能讲。

**https://x-cmd.com/ppt**
