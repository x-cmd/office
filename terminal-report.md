---
look: terminal
---

<!-- .slide: data-layout="t-log" -->

# 一 · 装环境

runner 起来第一件事不是编译,是把该有的环境变量摆平 —— 少一个,后面的作业表全是红的。

--

<!-- .slide: data-layout="t-env" -->

# 环境变量:五个,一个都不能少

CI 跑批读的就是这几个变量。少一个 `--filter` 之类的必填项,runner 会直接退 2。

<div class="row"><span class="dim">CI</span><span class="k">true</span><span class="v">GITHUB_ACTIONS</span></div>
<div class="row"><span class="dim">CI</span><span class="k">run 99812</span><span class="v">GITHUB_RUN_ID</span></div>
<div class="row"><span class="dim">main</span><span class="k">a7f3c91</span><span class="v">GITHUB_SHA</span></div>
<div class="row"><span class="dim">feat/queue-v2</span><span class="k">queue-v2</span><span class="v">GITHUB_HEAD_REF</span></div>
<div class="row"><span class="dim">22.21.1</span><span class="k">node</span><span class="v">NODE_VERSION</span></div>

<span class="t-ref">runner-07 · ubuntu-24.04 · 4 vCPU</span>

<span class="t-foot">$ x-cmd doctor → <span class="ok">all green</span></span>

--

<!-- .slide: data-layout="t-tree" -->

# 依赖树:装出来的东西长这样

`npm ci` 跑完,工作区多出来的是一棵固定的树 —— 每一层都能追到 `package.json` 里的哪一行。

<div class="tree">
<div class="line"><span class="b">▸</span><span class="d">node_modules/</span><span class="m">1 284 packages · 312 MB</span></div>
<div class="line"><span class="b">├──</span><span class="d">@x-cmd/core</span><span class="f">@0.14.2</span><span class="m">2.1 MB</span></div>
<div class="line"><span class="b">├──</span><span class="d">@x-cmd/sh</span><span class="f">@0.14.2</span><span class="m">1.4 MB</span></div>
<div class="line"><span class="b">│</span><span class="b">└──</span><span class="d">@x-cmd/lib</span><span class="f">@0.14.2</span><span class="m">640 KB</span></div>
<div class="line"><span class="b">├──</span><span class="f">reveal.js</span><span class="f">@6.0.2</span><span class="m">3.8 MB</span></div>
<div class="line"><span class="b">├──</span><span class="f">marked</span><span class="f">@16.4.1</span><span class="m">410 KB</span></div>
<div class="line"><span class="b">└──</span><span class="d">.cache/</span><span class="m">toolchain 4.155 · 已缓存</span></div>
</div>

<p class="tree-sum">合计 1 284 个包 · 312 MB · lockfile v3 · 无 network fallback</p>

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

<div class="row"><span class="ok">✓</span><span class="k">build</span><span class="v">passed</span><span class="n">1m 12s</span></div>
<div class="row"><span class="ok">✓</span><span class="k">lint</span><span class="v">passed</span><span class="n">0m 21s</span></div>
<div class="row"><span class="err">✗</span><span class="k">test</span><span class="v">failed</span><span class="n">2m 48s</span></div>
<div class="row"><span class="warn">●</span><span class="k">e2e</span><span class="v">skipped</span><span class="n">—</span></div>
<div class="row"><span class="dim">◷</span><span class="k">release</span><span class="v">blocked by test</span><span class="n">—</span></div>

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

<div class="row"><span class="err">✗</span><span class="k">queue drains in order</span><span class="v">queue.ts:118</span></div>
<div class="row"><span class="err">✗</span><span class="k">drain is atomic</span><span class="v">queue.ts:118</span></div>
<div class="row"><span class="dim">···</span><span class="k">其余 10 个用例</span><span class="v">同一条栈</span></div>

<span class="t-ref">test/queue.test.ts · 12 failing</span>

<span class="t-foot">exit <span class="err">1</span> · 3 retries</span>

--

<!-- .slide: data-layout="t-args" -->

# 这条跑批命令自己有哪些参数

CI 里那条命令不是死的 —— 参数表就这么多,写错了 runner 会直接退 2。

<div class="usage"><span class="p">$</span> x ci run <span class="q">--jobs 4 --timeout 900 --retry 3 --artifact --filter queue</span></div>

<div class="arg"><span class="k">--jobs</span><span class="s">-j</span><span class="v">并行作业数,上限受 runner CPU 限制</span><span class="n">4</span></div>
<div class="arg"><span class="k">--timeout</span><span class="s">-t</span><span class="v">单个作业超时秒数,超了判 failed</span><span class="n">900</span></div>
<div class="arg"><span class="k">--retry</span><span class="s">-r</span><span class="v">失败重试次数,重试用例结果不覆盖首跑</span><span class="n">3</span></div>
<div class="arg"><span class="k">--artifact</span><span class="s">-a</span><span class="v">上传日志与产物到制品库</span><span class="n">true</span></div>
<div class="arg"><span class="k">--filter</span><span class="s">-f</span><span class="v">只跑匹配的名字,逗号分隔</span><span class="n req">required</span></div>
<div class="arg"><span class="k">--branch</span><span class="s">-b</span><span class="v">跑批分支,默认取当前 HEAD</span><span class="n">HEAD</span></div>

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

<div class="row"><span class="err">✗</span><span class="k">3 次重试,3 次同样失败</span><span class="v">不是 flaky</span></div>
<div class="row"><span class="dim">◷</span><span class="k">首跑到重试间隔</span><span class="v">间隔 2.1s</span></div>
<div class="row"><span class="dim">◷</span><span class="k">trace 文件</span><span class="v">182 KB</span></div>

<span class="t-ref">artifacts/run-99812/queue.trace</span>

<span class="t-foot">replay exit <span class="err">1</span> · flaky 概率 <span class="ok">排除</span></span>

--

<!-- .slide: data-layout="t-stack" -->

# 栈:错在 drain 里的第 118 行

从最外层往里读,第一帧是我们自己的代码,最后一行才是真正出问题的那一帧。

<div class="stack">
<div class="frame"><span class="n">src/node/cli.ts:44</span><span class="m">await run(argv)</span></div>
<div class="frame"><span class="n">src/ci/runner.ts:96</span><span class="m">await job.test()</span></div>
<div class="frame"><span class="n">src/core/worker.ts:71</span><span class="m">await queue.drain()</span></div>
<div class="frame err"><span class="n">src/core/queue.ts:118</span><span class="m">await frame.commit()</span><span class="at">← 出错</span></div>
<div class="frame"><span class="n">src/core/frame.ts:52</span><span class="m">await store.write()</span></div>
</div>

<p class="why">队列在并发 push 下丢了一帧 —— <b>读-改-写没有串行化</b>,两个 worker 同时拿到了同一个 head。</p>

<span class="t-ref">trace · 5 frames · 1 error</span>

<span class="t-foot">at src/core/queue.ts:118:23 → <span class="err">E_LOST_FRAME</span></span>

--

<!-- .slide: data-layout="t-diff" -->

# 定位:这三条改动把队列改坏了

不是环境问题 —— diff 一摊开就看见了:锁只加在了写的那一半。

<div class="row"><span class="dim">M</span><span class="k">src/core/queue.ts</span><span class="v">+120 −12</span></div>
<div class="row"><span class="dim">M</span><span class="k">src/core/frame.ts</span><span class="v">+64 −18</span></div>
<div class="row"><span class="dim">M</span><span class="k">src/core/worker.ts</span><span class="v">+31 −7</span></div>
<div class="row"><span class="dim">A</span><span class="k">test/queue.test.ts</span><span class="v">+88 −0</span></div>

<div class="row"><span class="warn">●</span><span class="k">queue.ts:118</span><span class="v">锁只覆盖 write,没覆盖 read</span></div>
<div class="row"><span class="dim">◷</span><span class="k">首次出现</span><span class="v">a7f3c91^</span></div>

<span class="t-ref">9 files changed, 303 insertions(+), 37 deletions(−)</span>

<span class="t-foot">branch feat/queue-v2 · base main · 3 commits</span>

---

<!-- .slide: data-layout="t-status" -->

# 四 · 发版

修完重跑,五个作业全绿,release 这一格才亮起来。

<div class="row"><span class="ok">✓</span><span class="k">build</span><span class="v">passed</span><span class="n">1m 09s</span></div>
<div class="row"><span class="ok">✓</span><span class="k">lint</span><span class="v">passed</span><span class="n">0m 19s</span></div>
<div class="row"><span class="ok">✓</span><span class="k">test</span><span class="v">passed</span><span class="n">2m 41s</span></div>
<div class="row"><span class="ok">✓</span><span class="k">e2e</span><span class="v">passed</span><span class="n">3m 02s</span></div>
<div class="row"><span class="ok">✓</span><span class="k">release</span><span class="v">published</span><span class="n">0m 44s</span></div>

<span class="t-ref">run 99813 · 2026-11-25 04:06</span>

<span class="t-foot">$ echo $? → <span class="ok">0</span></span>

--

<!-- .slide: data-layout="t-env" -->

# 版本:这次发出去的东西

发版产物就是一份版本清单 —— 版本号、构建号、装了哪些依赖,一行一行对齐。

<div class="row"><span class="dim">pkg</span><span class="k">@x-cmd/ppt</span><span class="v">0.14.3</span></div>
<div class="row"><span class="dim">build</span><span class="k">20261125.0406</span><span class="v">linux-arm64</span></div>
<div class="row"><span class="dim">core</span><span class="k">@0.14.3</span><span class="v">core@0.14.3</span></div>
<div class="row"><span class="dim">tool</span><span class="k">4.155.0</span><span class="v">compat 2026-09-01</span></div>
<div class="row"><span class="dim">deps</span><span class="k">reveal 6.0.2</span><span class="v">marked 16.4.1</span></div>
<div class="row"><span class="dim">sbom</span><span class="k">1 284 pkgs</span><span class="v">cyclonedx 1.6</span></div>

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
