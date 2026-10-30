# ppt

## 把 markdown 变成一场演讲

长链接即入口 · 浏览器端 reveal.js 渲染

---

## 一个链接,一场演讲

```text
https://x-cmd.com/ppt?url=<markdown 链接>
```

贴进 README,别人点开就能讲。

---

## 它是 webapp,不是 action

| | draw | ppt |
|---|---|---|
| 输入 | 数据(参数) | **链接** |
| 输出 | 一张图 | **一场演讲** |
| 渲染 | 服务端 | **浏览器** |

---

## 三件事

1. **datalink** —— 输入是地址,不是内容
2. **浏览器渲染** —— 服务端只出 HTML 壳
3. **同源代理** —— 跨域由服务端代取

---

## 原理 · datalink

markdown 一般已经躺在仓库里。

```text
?url=https://raw.githubusercontent.com/o/r/main/talk.md
```

用户只想贴**它的地址**。

---

## 原理 · 浏览器渲染

服务端只出 HTML 壳:

1. 浏览器取 markdown(经同源代理)
2. reveal.js 切页、渲染

幻灯片是活的 —— 主题、翻页、备注、打印 PDF,全是原生能力。

---

## 原理 · 同源代理

源站大多**不发 CORS 头**,浏览器直接取会被拦。

服务端 fetch 不受同源策略约束 → 代取 → 以**同源**身份交给浏览器。

后台成了出口,所以要守边界:

- 只允许 `http/https`
- 拒绝内网 / 回环 / 云元数据
- 限体积、跳数、超时、频率

---

## 原理 · SSR 只做一页

reveal.js **没有**服务端渲染能力。

所以后台只把**指定的那一页**排成 SVG:

- 画布 960×700
- 字号 / 行高 / 间距 / 颜色 —— 取自主题 CSS
- 行盒模型照抄浏览器

于是封面图与浏览器里那一页**看着一样**。

---

## 原理 · 测量与渲染同源

折行点要跟浏览器一致,量宽就得用**同一份字体**。

- 内嵌字体子集进 SVG(`<img>` 引用时取不到字体)
- 同一份字体的**字宽表**用于排版

测量的字,就是渲染的字。

---

## 代码在哪

```draw
type=bar&labels=排版,取数,路由,页面,其它&values=615,272,263,327,431&w=560&h=300
```

各模块行数 —— 排版最重,因为要跟浏览器对齐。

---

## 图表:围栏里写参数

````markdown
```draw
type=bar&labels=Jan,Feb,Mar&values=3,5,4&w=560&h=300
```
````

服务端展开成**内联 SVG**,浏览器原生渲染 —— 矢量、可缩放,不是图片。

---

## 用法

```text
https://x-cmd.com/ppt?url=<markdown 链接>
https://x-cmd.com/ppt?data=<markdown 原文>
https://x-cmd.com/ppt/cover.svg?url=<链接>&slide=2
```

分页:`---` 横向 · `--` 纵向 · `Note:` 备注

---

## 边界

- reveal.js 无 SSR → 只保证"指定页"够像
- 远端图片不进 SVG,画占位框
- 主题字体只内嵌 Source Sans Pro
- 私有仓库的 deck 需另加 token 支持

---

## 后面

- 私有仓库的 deck
- 主题字体全内嵌
- 短链
- 更多图表类型
