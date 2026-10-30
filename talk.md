# ppt

## 把 markdown 变成一场演讲

**一个长链接就是入口** · 浏览器端 reveal.js 渲染 · 封面图由服务端排版

`https://x-cmd.com/ppt`

---

# 一 · 为什么

## markdown 早就写好了,演讲还没准备好

AI 十分钟写完一份 deck,然后呢?

- 装工具、导 PDF、改样式 —— 一遍遍重来
- 分享出去的是**文件**,不是**内容**

--

## 换个问法

> markdown 已经躺在仓库里 —— 能不能**只把它的地址贴出来**,别人点开就能讲?

把渲染搬到**浏览器**,把输入缩成**一个地址**。

---

# 二 · 先看效果

## 一个链接,一场演讲

```text
https://x-cmd.com/ppt?url=<markdown 链接>
```

贴进 README,别人点开就能讲。

--

## 封面就是一个 SVG

<a href="https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md"><img src="https://po6.sh/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md" width="420" alt="本 deck 的封面"></a>

上面这张图**就是这份 deck 的封面** —— 服务端把封面那页排成了 SVG(矢量、可缩放)。

点它 → 打开这份演示。图片显示尺寸用 HTML 的 `width` 属性控制。

--

## 三个现成的案例

- **本 deck** —— 把 markdown 变成一场演讲
  [开讲](https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md)
- **五分钟** —— 写 deck 的语法速查
  [开讲](https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/quickstart.md)
- **图表** —— 封面图与内联图表的玩法
  [开讲](https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/charts.md)

---

# 三 · 它是什么

## 一个 webapp,不是一个 action

输入是**地址**,输出是**一场演讲**;幻灯片在浏览器里渲染。

--

## draw vs ppt

| | draw | ppt |
|---|---|---|
| 输入 | 数据(参数) | **链接** |
| 输出 | 一张图 | **一场演讲** |
| 渲染 | 服务端 | **浏览器** |

--

## datalink:输入是地址

内容通常**已经在仓库里**了。用户只想贴它的地址。

于是接口只认一样东西:

```text
/ppt?url=<markdown 的地址>
```

不传内容,只传**指向内容的指针**。

---

# 四 · 原理

## 渲染在浏览器

服务端只出 HTML 壳:

1. 浏览器取 markdown(经同源代理)
2. reveal.js 切页、渲染

幻灯片是**活的** —— 主题、翻页、备注、打印 PDF,全是 reveal.js 原生能力。

我们不重写一个 PPT 系统。

--

## 同源代理

源站大多**不发 CORS 头**,浏览器直接取会被拦。

服务端 fetch 不受同源策略约束 → 代取 → 以**同源**身份交给浏览器。

后台成了出口,所以要守边界:

- 只允许 `http/https`
- 拒绝内网 / 回环 / 云元数据地址
- 限体积、跳数、超时、频率

--

## 取过一次就够了

备注窗口(`S`)会再开一个接收端页面,它本会**再取一次** markdown。

所以前端把取到的内容存进 `localStorage`(同源共享),之后一律用缓存 —— 不再回源。

---

# 五 · 封面图

## SSR 只做一页

reveal.js **没有**服务端渲染能力。

所以后台只把**指定的那一页**排成 SVG:

- 画布 960×700
- 字号 / 行高 / 间距 / 颜色 —— 取自主题 CSS
- 行盒模型照抄浏览器

于是封面图与浏览器里那一页**看着一样**。

--

## 测量与渲染同源

折行点要跟浏览器一致,量宽就得用**同一份字体**。

- 内嵌字体子集进 SVG(`<img>` 引用时取不到外部字体)
- 同一份字体的**字宽表**用于排版

测量的字,就是渲染的字。

--

## 也能是一段动画

依次播几页,最后定格:

```text
/ppt/cover.svg?url=…&anim=0,2,5&freeze=5
```

SVG 内嵌 **SMIL** 动画(HTML 标准在 `<img>` 上下文明确允许)。

不支持动画时,看到的就是**定格的那一页**。

---

# 六 · 图表

图表是**内联 SVG** —— 矢量、可缩放,不是图片。

--

## 围栏里写参数

服务端把围栏展开成内联 SVG,浏览器原生渲染:

```draw
type=bar&labels=Jan,Feb,Mar&values=3,5,4&w=560&h=300
```

--

## 写法就一句

围栏的语言标成 `draw`,内容是图表服务的参数:

````markdown
```draw
type=bar&labels=Jan,Feb,Mar&values=3,5,4&w=560&h=300
```
````

--

## 或者直接贴 draw 的链接

[![各模块行数](https://x-cmd.com/draw?type=bar&labels=排版,取数,路由,页面&values=615,272,263,327&w=560&h=300)](https://x-cmd.com/draw/explore?type=bar&labels=排版,取数,路由,页面&values=615,272,263,327)

指向图表服务的图片,同样会被内联成原生 SVG。

外面套一层链接 → **点图跳到别处**(这里是 draw 的 explore:悬停看数、改参数)。

---

# 七 · 用法

## 怎么翻

- `← →` 换主题 · `↑ ↓` 换主题内的页
- `ESC` 看全部幻灯片 · `S` 演讲者备注
- `?print-pdf` 直接打印成 PDF

--

## 三条链接

```text
/ppt?url=<markdown 链接>            # 演讲
/ppt?data=<markdown 原文>            # 演讲(内联)
/pt/cover.svg?url=<链接>&slide=1.2  # 指定页
```

分页:`---` 横向 · `--` 纵向 · `Note:` 备注

---

# 收尾

## 现在就去讲一场

把地址贴出来,别人点开就能讲。

**https://x-cmd.com/ppt**
