---
template: deck
theme: black
cover:
  title: datalink
  subtitle: 数据在链接里,不在截图里
  author: datalink.ac
  date: 2026-11-14
---

<!-- .slide: data-layout="statement" -->

# 链接里装的是数据本身

**不是数据的截图。**

---

# 一个链接,两种读者

<!-- .slide: data-layout="section" data-background-color="#1d1a14" -->

## 人看渲染,agent 读结构

同一个 URL:

| 读者 | 打开方式 | 看到 |
|---|---|---|
| 人 | `/draw?...` | 一张渲染好的 SVG |
| agent | `/draw.json?...` | 机器可读的 JSON 规格 |

双方操作的,是**同一串字符** —— 没有导出、没有同步、没有版本对不上。

--

## URL 即 API

```text
https://datalink.ac/draw?type=bar&labels=Jan,Feb&values=3,5
https://datalink.ac/draw.json?type=bar&labels=Jan,Feb&values=3,5
```

不用注册,不用 key,不用等编译 —— 链接就是全部状态。

参数改一个,图就换一张;**可拼、可存、可转述**。

---

# 一套理念,三件东西

## draw —— 图

数据在 URL 里,打开就是矢量 SVG;每张图自带 `<metadata>`,
机器顺手就能读。

--

## ppt —— 讲台

markdown 进,演讲出。渲染在浏览器,服务端只出壳;
封面是 SVG,README 里点图开讲。

--

## datalink.ac —— 门

`/draw` `/draw.json` `/ppt` 的转发入口,
外加四篇理念文章:*data in the link* · *one link, two audiences* ·
*the URL is the API* · *what a URL reveals*。

---

# 链接的另一面

<!-- .slide: data-layout="section" data-background-color="#241418" -->

## 一个 URL 会泄露什么

把链接当公开物来对待 —— 它至少会出现在这六个地方:

- 聊天与 issue 里的粘贴
- 下一站的 `Referrer` 头
- 浏览器跨设备同步
- CDN 与代理的缓存
- 截图与录屏
- 错误追踪日志

--

> 把 URL 当 API,就要把 URL 当**公开物**。

敏感的部分,放在链接之外。

---

# 为什么值得

- **零依赖的合作**:人和 agent 各取所需,不需要约定文件格式
- **永久可复现**:链接在,数据和图就在
- **极简到可以审计**:datalink.ac 的 devDependencies 只有一个 `marked`

一次表达,处处可用 —— 这就是 data in the link。

---

<!-- .slide: data-layout="end" -->

# 数据在链接里

**https://datalink.ac**
