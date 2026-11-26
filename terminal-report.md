---
title: 终端
look: terminal
---

<!-- .slide: data-layout="t-title" -->

# 终端

agent 干活的样子:命令、日志、退出码 —— 一份能回放的编译记录。

---

<!-- .slide: data-layout="t-log" -->

# 一 · 装环境

runner 起来第一件事不是编译,是把该有的环境变量摆平 —— 少一个,后面的作业表全是红的。

--

<!-- .slide: data-layout="t-env" -->

# 环境变量:五个,一个都不能少

CI 跑批读的就是这几个变量。少一个 `--filter` 之类的必填项,runner 会直接退 2。

|  |  |  |
|---|---|---|
| <span class="dim">CI</span> | true | GITHUB_ACTIONS |
| <span class="dim">CI</span> | run 99812 | GITHUB_RUN_ID |
| <span class="dim">main</span> | a7f3c91 | GITHUB_SHA |
| <span class="dim">feat/queue-v2</span> | queue-v2 | GITHUB_HEAD_REF |
| <span class="dim">22.21.1</span> | node | NODE_VERSION |

<span class="t-ref">runner-07 · ubuntu-24.04 · 4 vCPU</span>

<span class="t-foot">$ x-cmd doctor → <span class="ok">all green</span></span>

--

<!-- .slide: data-layout="t-tree" -->

# 依赖树:装出来的东西长这样

`npm ci` 跑完,工作区多出来的是一棵固定的树 —— 每一层都能追到 `package.json` 里的哪一行。

```text
▸ node_modules/                            1 284 packages · 312 MB
├── @x-cmd/core @0.14.2                     2.1 MB
├── @x-cmd/sh @0.14.2                       1.4 MB
│ └── @x-cmd/lib @0.14.2                    640 KB
├── reveal.js @6.0.2                        3.8 MB
├── marked @16.4.1                          410 KB
└── .cache/               toolchain 4.155 · 已缓存
```

合计 1 284 个包 · 312 MB · lockfile v3 · 无 network fallback

<span class="t-ref">npm 11.4.0 · --prefer-offline</span>

<span class="t-foot">$ npm ci → <span class="ok">added 1284 packages in 47s</span></span>

--

<!-- .slide: data-layout="t-log" -->

# 一条命令装完,一条命令验完

装依赖没有交互式提示,只有一行输出。真正要盯的是最后那句 —— 它决定后面作业表是不是绿的。

```text
$ npm ci --prefer-offline --no-audit
added 1284 packages, and audited 1285 in 47s

$ npx x-cmd doctor
✓ node        v22.21.1 (linux-arm64)
✓ core        @0.14.2
✓ sh          @0.14.2
✓ toolchain   4.155
✓ git         2.51.0
✗ proxy       未配置(内网跑批,正常)
```

<span class="t-ref">03:12:41 → 03:13:28 · install.sh</span>

<span class="t-foot">exit <span class="ok">0</span> · 5 checks · 1 skipped</span>

---

<!-- .slide: data-layout="t-status" -->

# 二 · 跑测试

环境装完就开跑:五个作业并行,谁先红谁先说话。

|  |  |  |  |
|---|---|---|---|
| <span class="ok">✓</span> | build | passed | 1m 12s |
| <span class="ok">✓</span> | lint | passed | 0m 21s |
| <span class="err">✗</span> | test | failed | 2m 48s |
| <span class="warn">●</span> | e2e | skipped | — |
| <span class="dim">◷</span> | release | blocked by test | — |

<span class="t-ref">run 99812 · 2026-11-25 03:14</span>

<span class="t-foot">$ echo $? → <span class="err">1</span></span>

--

<!-- .slide: data-layout="t-log" -->

# test 的输出:12 个用例挂在同一处

不是随机失败 —— 12 个用例指向同一行代码。日志里那行 `lost frame` 就是全部线索。

```text
$ npm test -- --reporter=dot
  ✓ 40 passing (1.2s)
  ✗ 12 failing (2.1s)
  1) queue drains in order
     AssertionError: expected 3 frames, got 2
     at src/core/queue.ts:118:23
```

|  |  |  |
|---|---|---|
| <span class="err">✗</span> | queue drains in order | queue.ts:118 |
| <span class="err">✗</span> | drain is atomic | queue.ts:118 |
| <span class="dim">···</span> | 其余 10 个用例 | 同一条栈 |

<span class="t-ref">test/queue.test.ts · 12 failing</span>

<span class="t-foot">exit <span class="err">1</span> · 3 retries</span>

--

<!-- .slide: data-layout="t-args" -->

# 这条跑批命令自己有哪些参数

CI 里那条命令不是死的 —— 参数表就这么多,写错了 runner 会直接退 2。

```text
$ x ci run --jobs 4 --timeout 900 --retry 3 --artifact --filter queue
```

|  |  |  |
|---|---|---|
| --jobs -j | 并行作业数,上限受 runner CPU 限制 | 4 |
| --timeout -t | 单个作业超时秒数,超了判 failed | 900 |
| --retry -r | 失败重试次数,重试用例结果不覆盖首跑 | 3 |
| --artifact -a | 上传日志与产物到制品库 | true |
| --filter -f | 只跑匹配的名字,逗号分隔 | <span class="req">required</span> |
| --branch -b | 跑批分支,默认取当前 HEAD | HEAD |

<span class="t-ref">x ci run --help · v0.14.2</span>

<span class="t-foot">usage 错误 → exit <span class="err">2</span></span>

---

<!-- .slide: data-layout="t-log" -->

# 三 · 看失败

红灯不是结论,栈才是。这一页只看一件事:它是不是 flaky。

```text
$ x ci run 99812 --trace --filter queue
replaying 1 failed job …
  [test] attempt 2/3 … failed
  [test] attempt 3/3 … failed
  captured trace → artifacts/run-99812/queue.trace
```

|  |  |  |
|---|---|---|
| <span class="err">✗</span> | 3 次重试,3 次同样失败 | 不是 flaky |
| <span class="dim">◷</span> | 首跑到重试间隔 | 间隔 2.1s |
| <span class="dim">◷</span> | trace 文件 | 182 KB |

<span class="t-ref">artifacts/run-99812/queue.trace</span>

<span class="t-foot">replay exit <span class="err">1</span> · flaky 概率 <span class="ok">排除</span></span>

--

<!-- .slide: data-layout="t-stack" -->

# 栈:错在 drain 里的第 118 行

从最外层往里读,第一帧是我们自己的代码,最后一行才是真正出问题的那一帧。

```text
src/node/cli.ts:44          await run(argv)
src/ci/runner.ts:96         await job.test()
src/core/worker.ts:71       await queue.drain()
src/core/queue.ts:118       await frame.commit()    ← 出错
src/core/frame.ts:52        await store.write()
```

> 队列在并发 push 下丢了一帧 —— **读-改-写没有串行化**,两个 worker 同时拿到了同一个 head。

<span class="t-ref">trace · 5 frames · 1 error</span>

<span class="t-foot">at src/core/queue.ts:118:23 → <span class="err">E_LOST_FRAME</span></span>

--

<!-- .slide: data-layout="t-diff" -->

# 定位:这三条改动把队列改坏了

不是环境问题 —— diff 一摊开就看见了:锁只加在了写的那一半。

|  |  |  |
|---|---|---|
| <span class="dim">M</span> | src/core/queue.ts | +120 −12 |
| <span class="dim">M</span> | src/core/frame.ts | +64 −18 |
| <span class="dim">M</span> | src/core/worker.ts | +31 −7 |
| <span class="dim">A</span> | test/queue.test.ts | +88 −0 |

|  |  |  |
|---|---|---|
| <span class="warn">●</span> | queue.ts:118 | 锁只覆盖 write,没覆盖 read |
| <span class="dim">◷</span> | 首次出现 | a7f3c91^ |

<span class="t-ref">9 files changed, 303 insertions(+), 37 deletions(−)</span>

<span class="t-foot">branch feat/queue-v2 · base main · 3 commits</span>

---

<!-- .slide: data-layout="t-status" -->

# 四 · 发版

修完重跑,五个作业全绿,release 这一格才亮起来。

|  |  |  |  |
|---|---|---|---|
| <span class="ok">✓</span> | build | passed | 1m 09s |
| <span class="ok">✓</span> | lint | passed | 0m 19s |
| <span class="ok">✓</span> | test | passed | 2m 41s |
| <span class="ok">✓</span> | e2e | passed | 3m 02s |
| <span class="ok">✓</span> | release | published | 0m 44s |

<span class="t-ref">run 99813 · 2026-11-25 04:06</span>

<span class="t-foot">$ echo $? → <span class="ok">0</span></span>

--

<!-- .slide: data-layout="t-env" -->

# 版本:这次发出去的东西

发版产物就是一份版本清单 —— 版本号、构建号、装了哪些依赖,一行一行对齐。

|  |  |  |
|---|---|---|
| <span class="dim">pkg</span> | @x-cmd/ppt | 0.14.3 |
| <span class="dim">build</span> | 20261125.0406 | linux-arm64 |
| <span class="dim">core</span> | @0.14.3 | core\@0.14.3 |
| <span class="dim">tool</span> | 4.155.0 | compat 2026-09-01 |
| <span class="dim">deps</span> | reveal 6.0.2 | marked 16.4.1 |
| <span class="dim">sbom</span> | 1 284 pkgs | cyclonedx 1.6 |

<span class="t-ref">registry · @x-cmd/ppt@0.14.3</span>

<span class="t-foot">$ x-cmd doctor → <span class="ok">all green</span></span>

--

<!-- .slide: data-layout="t-exit" -->

<span class="code">exit 0</span>

# 收尾:跑批结束,终端回到提示符

从装环境到发版,一共 41 分钟。跑批最重要的产物不是包,是那条能复现的日志。

<div class="links">
<a href="https://github.com/x-cmd/ppt/pull/42">PR #42</a>
<a href="https://github.com/x-cmd/office/issues/7">issue #7</a>
<a href="https://x-cmd.com/ppt">线上</a>
</div>

<span class="t-ref">run 99812 → 99813 · feat/queue-v2</span>

<span class="t-foot">look: terminal · agent 的工作痕迹</span>
