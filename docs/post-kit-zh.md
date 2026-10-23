# 发帖文案包（四平台）

> 用法：复制对应平台的一段，配图用 `发布\B站配图\` 里的四张。
> 哈希/链接以 `SHA256.txt` 为准。

---

## 一、小黑盒（已发过一版，这是精简新版）

**标题**
> 我花了半个月，测了 5 款游戏的服务器 tick，有几个数挺意外

**正文**

先说结论：三角洲烽火 60、绝密 120、CS2 64、卡拉彼丘 30、无畏契约约 128（多路复用，工具判不可判）。

怎么测的：不注入、不读内存、不改游戏，只用 Windows 自带抓包看时间戳。一段时间的包如果等间隔，频谱上会出现一根尖峰，峰的位置就是频率。为了不靠单一方法，我用四种算法互相对，对不上就写「不可判」。

怎么证明没测错：自造 60/50/128 Hz 的流，误差 0.0%；故意丢 10%/20% 的包，估出 10.2%/20.9%；6 种伪造节奏的陷阱全被识破；误判登记簿记了 16 条自己犯过的错。

哪里测不准：批 ≠ 引擎 tick；多路复用测不了；10 秒以内的变化看不见；「缺包」偏高。

工具叫鲸歌，解压就能用，不联网、不会偷偷上传。
下载：<蓝奏云链接> 密码：<提取码>
SHA-256：<哈希>

所有数字都可以复现：抓包和脚本都给，谁都能算出一样的结果。

---

## 二、B站专栏（长文，已有一版可直接用）

用 `发布\B站专栏-发布版.md`，标题：

> 我测了 4 款游戏的服务器 tick，说几个可能没人告诉你的数

配图顺序：封面 → 四款对比 → 闭环验证 → 缺包真值。

---

## 三、贴吧（短帖试水，先不发链接）

**标题**
> 用抓包测了几款游戏的服务器 tick，数据放这，轻喷

**正文**

不注入不改游戏，纯抓包看时间戳算的。测了一周多：

- 三角洲 烽火约 60 / 绝密约 120
- CS2 约 64
- 卡拉彼丘 约 30
- 无畏契约 约 128（多路复用，只能给参考）

方法：频谱找峰 + 四种算法互验，对不上就标「不可判」。

验证：自造已知频率误差 0.0%；丢包 10%/20% 估出 10.2%/20.9%。

想自己测可以搜「鲸歌」，解压即用。**有问题评论区问，数据我都留着。**

---

## 四、Reddit（英文，r/GlobalOffensive / r/VALORANT 慎发版规）

**Title**
> I measured server tick rates for 4 games with passive packet capture — here are the numbers

**Body**

No injection, no memory reading, no game modification. Just Windows built-in packet capture and timestamps.

- Delta Force: ~60 (Warfare) / ~120 (Space City)
- CS2: ~64
- Strinova: ~30
- VALORANT: ~128 by inter-arrival peak, but the flow is multiplexed so the tool reports it as undecidable

Method: if packets arrive periodically, the spectrum shows a sharp peak; four estimators cross-check, and anything inconsistent is labeled undecidable.

Validation: synthetic 60/50/128 Hz streams (0.0% error), 10%/20% induced loss (estimated 10.2%/20.9%), 6 adversarial cadence traps rejected.

Limits: batches ≠ engine tick; multiplexed flows are undecidable; changes under 10s are invisible; loss is over-reported.

Tool (Windows, portable, offline): github.com/86dfj/whale-song

All numbers are reproducible — capture + scripts, anyone gets the same result.

---

## 发布注意

1. 先发小黑盒/贴吧试水，看有没有人问
2. 有人问再给链接，**别一上来贴链接**
3. 遇到「你这是外挂吧」：回「不注入、不读内存、不改游戏，只抓时间戳」，别吵
4. 遇到要数据的：让对方点「反馈（只报告）」
