# make.fun 参赛核查报告 — news-image-20261121

- 核查时间：2026-11-22 02:21–02:35 AWST（2026-11-21 18:21–18:35 UTC）
- 比赛：`news-image-20261121` — “Sum up 21 November's world news in one image”
- 截止：**2026-11-23 00:00:00Z = 2026-11-23 08:00 AWST**（requirements `deadlines.entries_close`；escrow 另有 `entries_deadline 2026-11-23T00:10:00Z`，以 08:00 AWST 为硬截止）
- 奖金：**$100 USDC，共 50 个名额**（第 1 名 $20、第 2 名 $12、第 3 名 $6、第 4–10 名 $2、第 11–50 名 $1.20），USDC on Solana，escrow 已全额锁定（100,000,000 base units，mint EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v，escrow 地址 Av1x98MLcLptDzQER5hbiLZd9j41459GjAehAdEgLTVL，状态 open）
- 结果预计：**2026-12-07 08:00 UTC** 公布（`result_due`）
- 已参赛作品数（核查时）：**0**（escrow `entries_count: 0`）
- 参赛仓库（待建）：https://github.com/135479sun-glitch/news-image-20261121（公开，尚未创建）
- 收款钱包：代理钱包 `AZSkkVwJm9g5x25sHymZUZRU4fWcuDxA8bKqio3cgtqx`（提交用 agent keypair 签署；**不用 Sun 的 Phantom 签名**，Phantom `Fc7NfAV7RAr7Z8o1jVoZF9cwnKkjoQELMzt3e8JDK2wC` 只是奖金最终转入的目标钱包）
- 本报告只做核查和准备：**未修改任何参赛文件，未生成图片，未提交任何东西，未创建钱包，未索取任何密钥。**

要求来源：直接读取 `GET https://make.fun/api/competitions/news-image-20261121/requirements`（2026-11-21 18:21 UTC 抓取，原始 JSON 在 `/tmp/req-20261121.json`）及 `https://make.fun/skill.md`（v1.5.234，与昨天同一版）。

**重要时间说明**：2026-11-21 是星期六。本比赛是“11 月 21 日的新闻”：美国时间 11 月 20 日（周五）发生的事件，在澳大利亚/亚洲时间就是 11 月 21 日见报——第 1、2、3、6 条都属于这种情况，属“11 月 21 日的新闻”是合理的（与昨天核查第 1、2、4、5 条的逻辑一致）；第 4、5 条是 11 月 21 日当天（周六）发生的事件。报告中已注明事件日与报道日。

---

## 一、参赛硬性要求清单

### 1.1 比赛本身的要求

| # | 要求 | 状态 |
|---|------|------|
| 1 | 作品是一个程序，输出一张图片到 `/output/entry.png` | 待建（沿用昨天的 `main.py` 结构，改日期） |
| 2 | 图片为完整 PNG 或 JPEG，**≤ 1 MiB 且 1024×1024 像素** | 待建（1024×1024，2 列 × 3 行） |
| 3 | 无网络；程序跑两次，两次必须写出**完全相同的字节**（确定性） | 待验证（纯 Pillow、无网络、无随机数、无时间戳） |
| 4 | 每天最多 10 次提交，总共最多 40 次（`max_entries_per_account: 40`）；截止前最后一次提交为最终作品 | ✅ 尚未提交，额度未用 |
| 5 | 评判：AI 评委看图、两两对比，选出最能概括当日世界新闻的一张；按胜率排名，前 50 名分奖。评委没有新闻源，只按图片本身内容判断 | ⚠️ 提示：图片必须**自带全部信息**（标题、地点、关键数字写在图上），不能依赖外部说明；字要够大、够清晰 |
| 6 | 无报名费（`entry_fee: null`） | ✅ |

### 1.2 提交表单的硬性 deliverables

| 字段 | 必填 | 状态 |
|------|------|------|
| `repo_url` | 是 | ❌ 仓库尚未创建（`news-image-20261121`，待建，须公开） |
| `commit_sha` | 是 | ❌ 待仓库创建并推送后取完整 40 字符 sha |
| `bundle`（transcript bundle `.tar.gz`，由 kit 的 `node cli/makefun.mjs bundle` 生成；或用 loose `transcripts` 文件代替） | 是 | ❌ 未做 |
| `transcripts`（loose 文件，可代替 bundle） | 否（与 bundle 二选一） | ❌ 未做 |
| `title`（作品公开名，≤200 字符；不要放 handle、仓库名、密钥） | 否 | ⚠️ 建议：`The World in One Image — 21 November 2026` |
| `entry_message`（`make.fun entry v1` 模板，注明仓库/commit/transcript sha256/钱包，**签署时距提交不到 10 分钟**） | 是 | ❌ 提交时现签（用 agent keypair 代签，见 1.5） |
| `entry_signature`（entry_message 的 Ed25519 签名，签名钱包即收款钱包） | 是 | ❌ 提交时现签（agent 钱包 `AZSkkVwJm9g5x25sHymZUZRU4fWcuDxA8bKqio3cgtqx`） |
| `LICENSE`（OSI 批准许可证，须含 `SPDX-License-Identifier:` 行） | 是 | 待建（MIT，含 SPDX 行） |
| `main.ts` 或 `main.py`（评委运行的入口，位于仓库根目录） | 是 | 待建（`main.py`，Python 3.13） |
| `.makefun/owner.json` | 否 | 不需要——仓库 owner（135479sun-glitch）就是账号的 GitHub 登录名 |

### 1.3 仓库层面的硬性检查（`checks`，applies: true）

| 检查 | 要求 | 状态 |
|------|------|------|
| `repo_public` | 仓库提交时必须公开可读 | ❌ 待建 |
| `repo_created_after_open` | 仓库必须在比赛开赛（2026-11-21 00:00 UTC）之后创建 | ⚠️ **注意**：比赛开赛是 2026-11-21 00:00 UTC，仓库必须在那之后创建（今天建即可，符合） |
| `license_osi` | LICENSE 须为 OSI 批准许可且含 SPDX 行 | 待建 |
| `repo_readme` | README 必须展示 make.fun 的 **3 个 live 徽章**：`badge/news-image-20261121.svg`、`badge/news-image-20261121/{owner}/{repo}/rank.svg`、`badge/news-image-20261121/{owner}/{repo}/reward.svg`（owner/repo 填实），并链接到 make.fun | 待建 |
| `repo_about` | GitHub About 必须设置：website = 比赛页 https://make.fun/bounty/news-image-20261121，topics 含 `makefun`（推荐再加 `ai-agents`、`bounties`、`growth`），描述含 make.fun 与比赛名 | ❌ 未设置 |
| `commit_in_repo` | commit_sha 必须是仓库里可取到的完整 40 字符 sha | 待推送后取 |
| `duplicate_snapshot` | 作品文件不得与他人已提交的快照完全相同 | ⚠️ 本作品代码沿用昨天自己写的生成器（news.json、README、标题不同，快照不同），不要复制别人的文案/版式 |
| `account_wallet` | 账号必须有 Solana 钱包（奖金链上支付给签名钱包） | ✅ 代理钱包已链接到账号（昨天提交时已验证，API key 有效期到 2026-12-21） |
| `competition_open` / `quota` | 比赛开放期内提交；每账号每天 ≤10 次、总共 ≤40 次 | ✅ 比赛 open，额度未用 |
| `security_audit` / `committed_secret` | 代码通过安全审计；仓库历史中不得含提交过的密钥 / provider API key | ⚠️ 提交前须扫一遍 |
| `source_bundle` | applies: true（本次新增检查项，本地 check 时留意） | 待验证 |
| `entry_size` | 本比赛 `applies: false` | — |

### 1.4 Transcript（会话记录）——与昨天相同的规则

- `transcripts_present` / `thinking_reproduces` / `thinking_revised` 等检查均为 applies: true：
  - 至少一个 agent 会话必须能被解析；会话必须证明 agent **自己写了代码**（authored 行数 ≥ 30%，含入口文件；文件最终内容须来自 **≥2 次**写/编辑该文件的 assistant 消息）。
  - 会话时间戳必须落在比赛开赛（2026-11-21 00:00 UTC）至提交之间；须附 run record。
- **`handed_over_places: none`**：如果会话是“handed over”（事后自写导出的会话文件，而非 harness 记录的日志），作品可以排名，**但拿不到任何付费名次**。昨天用 Muse 会话 bundle 验证为 recorded，可以拿奖——今天沿用同一做法（Muse app 会话 + kit bundle），提交前用 `bundle --dry-run` 再验证一次。
- bundle 会自动收集 instruction 文件和系统提示并做脱敏；提交前须检查脱敏项（邮箱、Gemini key 前缀 `AQ.Ab8RN6` 用 `--redact` 再清一次）。

### 1.5 提交方式（与昨天不同：不用 Sun 签名）

- `POST /api/competitions/news-image-20261121/submissions`（multipart/form-data），或用 kit 命令：
  `node cli/makefun.mjs submit --competition news-image-20261121 --repo-url <url> --commit <sha> --title <name> --bundle <file> --keypair /home/hatch/.makefun/keypairs/https_make.fun.json`
- 需 API key（`x-api-key: af_...`，已存在 `~/.makefun/credentials`，有效期到 2026-12-21）。
- **签名钱包 = 代理钱包 `AZSkkVwJm9g5x25sHymZUZRU4fWcuDxA8bKqio3cgtqx`**（昨天提交时已验证可用）。奖金进代理钱包，之后再转 Sun 的 Phantom。**不要用 Sun 的 Phantom 签名，不要向 Sun 要任何 keypair/助记词。**
- 结果预计 2026-12-07 08:00 UTC 公布；领取窗口 30 天（`claim_seconds: 2592000`）。

---

## 二、6 条新闻逐条核实

核查标准：以 Reuters / AP / BBC / CNN / WSJ / Al Jazeera / NHK 等主流来源、2026-11-21 前后（以 11 月 21 日当日报道为准）的报道为准。

### 第 1 条 — AI 股大跌，美股进入修正区间

- **结论：✅ 属实**
- 事实：美国时间 2026-11-20（周五），AI 股抛售加剧：**标普 500 跌 3.7% 至 6,910.39 点**（跌 265.44 点），为 18 个月来最差一周，连续第 7 个交易日下跌，**自 10 月 6 日历史高点跌超 10%，进入修正区间**；**纳斯达克跌 5.28% 至 22,617.73 点**，2026 年内转负，为 2020 年 3 月以来最差一周、史上最大单周点数跌幅（-2,518.54 点）；道指跌 1.93% 至 48,147.33 点。亚洲跟跌：**日经跌 5.06%（-5.1%）**、韩国 Kospi 跌超 5%、台湾加权跌 6.2%。英伟达单日跌约 14%（一周跌 22.9%）；Anthropic 上市次日跌约 8.5%–9.2%。诱因：市场担忧 AI 投入规模与回报、估值过高。
- 来源：
  - AP（via AsiaOne / New Indian Express)，“S&P 500 sinks 3.7% and Nasdaq composite goes negative for the year as tech sell-off worsens” — https://www.asiaone.com/money/sp-500-sinks-37-and-nasdaq-composite-goes-negative-year-tech-sell-worsens
  - WSJ, “The selloff in technology stocks spilled over today…” — https://www.wsj.com/livecoverage/stock-market-today-dow-sp-500-nasdaq-11-20-2026
  - The Times, “Anthropic shares tumble as Wall Street enters correction territory” — https://www.thetimes.com/business/technology/article/anthropic-pulls-back-6-percent-in-global-tech-sell-off-fss0m0hcr
  - Times of India, “AI sell-off batters Wall Street; S&P 500 enters correction, Nasdaq turns negative for year” — https://timesofindia.indiatimes.com/business/international-business/ai-sell-off-batters-wall-street-sp-500-enters-correction-nasdaq-turns-negative-for-year/articleshow/136041935.cms
- 注意：交易日是 11 月 20 日（周五），报道日是 11 月 21 日——按昨天同一口径，属 11 月 21 日的新闻。图上写“Friday”或只写数字即可，不要写成“11 月 21 日暴跌”。

### 第 2 条 — 墨西哥抓获 FBI 通缉毒枭“矮子伊西德罗”

- **结论：✅ 属实**
- 事实：墨西哥军方 2026-11-20（周五）深夜在锡那罗亚州瓜萨维突袭抓获 **Fausto Isidro Meza Flores（44 岁），绰号“El Chapo Isidro”**，同时抓获另外两名头目；2026-11-21（周六）上午由墨西哥国防部/安全负责人宣布。他是 **FBI 十大通缉犯之一**（2025 年 2 月上榜）、美方悬赏 **500 万美元**、贝尔特兰·莱瓦集团头目、锡那罗亚集团“马约派”盟友，涉嫌向美国走私海洛因、冰毒、可卡因、芬太尼、大麻 20 多年。行动由美军情报协助，特种部队“隐秘突袭”；抓捕后引发枪战、路障，瓜萨维一场棒球赛观众疏散；三人已押往墨西哥城。
- 来源：
  - Reuters, “Mexico captures top drug lord ‘El Chapo Isidro,’ latest in string of captures” — https://www.reuters.com/world/americas/mexico-captures-top-drug-lord-el-chapo-isidro-latest-string-captures-2026-11-21/
  - WSJ, “Mexico Captures Top Drug Boss in Fierce Gunfight” — https://www.wsj.com/world/americas/mexico-captures-top-drug-boss-in-fierce-gunfight-b16709ce
  - Al Jazeera, “Who is El Chapo Isidro, the alleged cartel boss arrested in Mexico?” — https://www.aljazeera.com/news/2026/11/21/who-is-el-chapo-isidro-the-alleged-cartel-boss-arrested-in-mexico
  - CNN, “Cartel kingpin on FBI’s most wanted list captured in dramatic Mexican military operation” — https://www.cnn.com/2026/11/21/americas/el-chapo-isidro-mexico-fbi-wanted-hnk-intl
- 注意：他与已入狱的“矮子”古斯曼（Joaquín “El Chapo” Guzmán）**没有亲属关系**，图上不要写错；抓捕是 11 月 20 日深夜、宣布是 11 月 21 日上午。

### 第 3 条 — 俄罗斯导弹袭击泽连斯基家乡克里沃罗格

- **结论：✅ 属实**
- 事实：2026-11-20（周五）深夜，俄罗斯导弹袭击乌克兰中部城市 **克里沃罗格（总统泽连斯基的家乡）**市中心：先是两枚弹道导弹，随后救援展开时又有三枚击中救援人员；**2 人死亡（一名 7 岁男孩和一名 20 岁女子），60 人受伤（含 6 名儿童）**。地方官员 2026-11-21（周六）公布。同一天，俄军无人机还袭击了哈尔科夫地区一栋公寓楼，11 人受伤。
- 来源：
  - AP（via Arab News / The Hindu), “Ballistic missile attack on Zelenskyy’s hometown in central Ukraine kills 2 and wounds scores” — https://www.arabnews.com/world/ballistic-missile-attack-on-zelenskys-hometown-in-central-ukraine-kills-2-and-wounds-scores-3013401
  - Al Jazeera, “Russian strike kills two, wounds 60, in Zelenskyy’s hometown” — https://www.aljazeera.com/news/2026/11/21/russian-strike-kills-two-wounds-60-in-zelenskyys-hometown
  - The Hindu, “Ballistic missile attack on Zelenskyy's hometown kills 2” — https://www.thehindu.com/news/international/ballistic-missile-attack-on-zelenskyys-hometown-kills-2/article71729235.ece
- 注意：这是 11 月 21 日的新袭击（不同城市、不同于昨天图里的 11 月 20 日基辅大空袭），不要与昨天那条混淆；图上写“Zelensky's hometown”即可。

### 第 4 条 — COP31 气候谈判因化石燃料僵局拖过截止期

- **结论：✅ 属实**
- 事实：联合国气候大会 **COP31 在土耳其安塔利亚**原定 2026-11-20（周五）晚闭幕，但因近 200 个国家对最终协议文本无法达成一致而**拖入加时（11 月 21 日周六仍在谈）**。争议核心：初稿要求加快淘汰化石燃料，周四的精简版在沙特等产油国反对后**删掉了所有化石燃料表述**，同时删掉了每年 1,200 亿美元适应资金目标；欧盟警告草案可能让峰会变成“化石峰会”；第三版草案预计周六出台，若谈崩则议题推给明年埃塞俄比亚主办的 COP32。
- 来源：
  - Al Jazeera, “Fossil fuel talks deadlock pushes COP31 climate summit into overtime” — https://www.aljazeera.com/amp/news/2026/11/20/fossil-fuel-talks-deadlock-pushes-cop31-climate-summit-into-overtime
  - AP（via The Wire), “Climate Talks in Overtime as Countries Wrestle With Response to Worsening Global Warming” — https://thewire.in/environment/climate-talks-in-overtime-as-countries-wrestle-with-response-to-worsening-global-warming
  - AAJ News, “Fossil fuel dispute threatens to scupper climate deal” — https://english.aaj.tv/news/330481608
- 注意：这是 11 月 21 日当天仍在发生的新闻，图上写“talks run past deadline”最准确；不要写“谈判破裂”（尚未破裂，只是加时）。

### 第 5 条 — 霍尔木兹海峡油轮遇袭，伊朗称击落美军无人机

- **结论：✅ 属实（油轮遇袭已证实；无人机击落是伊朗单方面说法，须注明“称”）**
- 事实：2026-11-21（周六）上午，英国海上贸易行动办公室（UKMTO）通报：**两艘油轮在阿曼哈萨布附近的霍尔木兹海峡被“不明投射物”击中**（一艘在哈萨布以北 11 海里处船尾中弹，一艘在以东 17 海里处机舱中弹），**无人伤亡**。同日，伊朗革命卫队称其防空部队在霍尔木兹海峡上空击落一架美军 **MQ-9“死神”无人机**（伊方称是第 58 架），随后又称在格什姆岛上空击落一架 MQ-1；伊方还称打伤一架美军 F-16，**美军中央司令部已否认 F-16 的说法**。背景：美伊战争 2026 年 2 月 28 日爆发以来已持续约 9 个月，UKMTO 已将该海峡威胁等级列为“严重”。
- 来源：
  - Al Jazeera, “Iran says it downed US drones over Hormuz as bid to end war remains stalled” — https://www.aljazeera.com/news/2026/11/21/irans-irgc-downs-us-drone-over-hormuz-as-efforts-to-end-war-remain-stalled
  - Al Jazeera liveblog, “Iran war live: US denies Iranian army’s claim it struck an F-16 over Gulf” — https://www.aljazeera.com/news/liveblog/2026/11/21/iran-war-live-saudi-led-coalition-repels-houthi-missiles
  - ANI（via Tribune India), “Tanker hit by unknown projectile in Strait of Hormuz near Oman, no casualties reported: UKMTO” — https://www.tribuneindia.com/news/world/tanker-hit-by-unknown-projectile-in-strait-of-hormuz-near-oman-no-casualties-reported-ukmto/
  - Tehran Times, “Iran downs 58th US MQ-9 drone, damages F-16” — https://www.tehrantimes.com/news/532395/Iran-downs-58th-US-MQ-9-drone-damages-F-16
- 注意：**无人机击落只是伊朗的说法，未经独立证实；F-16 的说法已被美方否认，图上不要写。** 图上写“Two tankers hit near Hormuz; Iran claims it downed a US drone”最稳妥。

### 第 6 条 — 胰腺癌新药试验：肿瘤在一成患者体内消失

- **结论：✅ 属实（早期试验，须注明是试验结果、非治愈）**
- 事实：2026-11-20（周五）在巴塞罗那 EORTC-NCI-AACR 研讨会上公布的一项 1/2 期试验（61 名晚期胰腺癌患者，口服药 **daraxonrasib** 每日一片 + 吉西他滨/白蛋白紫杉醇化疗）：**60.7% 的患者肿瘤缩小或消失，其中 8.2%（约十二分之一，5 人）扫描显示肿瘤完全消失**；90.2% 的患者病情得到控制；中位无进展生存 12.8 个月；一年生存率 76.6%。首席研究员、纪念斯隆-凯特琳癌症中心的 Wungki Park 博士称之为“重大突破”。**注意：试验仅 61 人、无对照组，不能证明延长总生存、更不是治愈；** 更大型的 3 期随机试验（RASolute-303）已启动。
- 来源：
  - The Guardian（via Indian Express), “A pill that makes pancreatic cancer disappear? What the daraxonrasib trial found” — https://indianexpress.com/article/lifestyle/health/a-pill-that-makes-pancreatic-cancer-disappear-what-the-daraxonrasib-trial-found-10972765/
  - Gulf News, “Breakthrough Pancreatic Cancer Pill Shows Tumour Disappearance in Clinical Trials” — https://gulfnews.com/amp/story/uae%2Fhealth%2Fnew-pancreatic-cancer-pill-makes-tumours-disappear-in-some-patients-1.500754850
  - NY Post, “‘Massive breakthrough’ as new pancreatic cancer treatment can make tumors disappear” — https://nypost.com/2026/11/20/health/pancreatic-cancer-combo-made-tumors-disappear-massive-breakthrough/
  - Human Progress, “Drug Combo Shrinks Some Advanced Pancreatic Tumors” — https://humanprogress.org/drug-combo-shrinks-some-advanced-pancreatic-tumors/
- 注意：公布日是 11 月 20 日（周五），多家媒体 11 月 21 日报道——按同一口径属 11 月 21 日新闻。图上写“in a trial”或“trial finds”，不要写成“治愈胰腺癌”。

---

## 三、备选（未入选，但已核实）

### 备选 1：FBI 与美国农业部遭黑客入侵

- 事实：美国媒体 2026-11-20（周五）报道：FBI 正在调查其**全国犯罪信息中心（NCIC）数据库遭入侵**（9 月以来第二次被黑）；美国农业部一个用于向农民付款的系统也遭网络攻击。NBC、CNN 首报；**尚不清楚两次事件是否相关、谁是幕后黑手**。来源：AFP（via Dawn / Straits Times) — https://www.dawn.com/news/2046105/fbi-us-agriculture-department-breached-by-hackers-reports ；CNN/NBC 原报。未入选原因：归属不明、“据报道”成分较重，信息量不如第 6 条的硬数字。

### 备选 2：英欧达成“脱欧重置”协议

- 事实：2026-11-20（周五）布鲁塞尔欧英峰会，英国首相 Andy Burnham 与欧盟达成三项协议：食品农产品检查互免、碳排放交易体系挂钩、青年流动计划（每边 10 万名 30 岁以下青年可居留最长 3 年）；英方称可提振 GDP 0.5%（约 170 亿英镑）。来源：Al Jazeera — https://www.aljazeera.com/news/2026/11/20/eu-and-uk-seal-reset-deal 。未入选原因：这是 **11 月 20 日的事件**（且昨天那单的落选草稿里已有类似条目），放进 11 月 21 日的图里日期上吃亏；留作备选。

### 其他已排除

- 丹麦驱逐俄外交官（涉刺杀说唱歌手阴谋）：真实，但影响面小于入选的 6 条。
- 法国生活成本抗议（8.25 万人）：真实，但属国内新闻、国际分量不足。
- 特朗普称欧洲应停止资助乌克兰 / 考虑再打伊朗：多为表态与筹划，无已发生的新事实。

---

## 四、最终 6 条清单（给模型跑 10 遍用的事实稿）

| # | 标题（草稿） | 摘要（事实稿，模型据此改写，勿编造） | 标签 |
|---|------|------|------|
| 1 | AI Sell-Off Drags Markets Into Correction | The S&P 500 fell 3.7% and the Nasdaq 5.3% on Friday, both entering correction territory, as the AI rout spread worldwide; Japan's Nikkei fell 5.1%. | MARKETS · NEW YORK |
| 2 | Mexico Captures FBI Most-Wanted Cartel Boss | Mexican forces captured Fausto Isidro Meza Flores, known as "El Chapo Isidro," in Sinaloa; the US had offered a $5 million reward. | JUSTICE · SINALOA |
| 3 | Russian Strike Hits Zelensky's Hometown | A Russian missile strike on Kryvyi Rih killed two people, a 7-year-old boy and a 20-year-old woman, and wounded 60. | WAR · KRYVYI RIH |
| 4 | COP31 Climate Talks Run Past Deadline | UN climate talks in Antalya ran into overtime as nearly 200 countries deadlocked over a draft deal with no mention of fossil fuels. | CLIMATE · ANTALYA |
| 5 | Tankers Hit Near Hormuz as Iran Claims US Drone Down | Two tankers were hit by unknown projectiles near Oman, and Iran claimed it shot down a US MQ-9 drone over the Strait of Hormuz. | CONFLICT · HORMUZ |
| 6 | Pancreatic Cancer Pill Makes Tumours Vanish in Trial | A daily pill with chemotherapy made tumours undetectable in one in 12 advanced pancreatic cancer patients in a 61-person trial. | HEALTH · BARCELONA |

`sources` 字段用：Al Jazeera, Associated Press, Reuters, The Wall Street Journal, The Times, CNN, NBC News, Agence France-Presse — 21 Nov 2026.

---

## 五、提交前必须做好的事（按优先级）

1. **模型跑 10 遍**：用 Kaggle Gemma 模型对上表 6 条事实各生成 10 个版本（标题+一句话摘要），挑最好的一套组合；**不发给 Sun 看**，由负责的人自己挑。注意当前 Kaggle 会话 12 小时上限约到 2026-11-22 10:45 AWST，须在那之前跑完；若会话停了，重启（重装 Ollama、重拉 18GB 模型、中文测试）再跑。
2. **建仓库**：`news-image-20261121`，公开；仓库须在 2026-11-21 00:00 UTC 之后创建（今天建即符合）。集成建仓库之前报过 403，优先用已登录 135479sun-glitch 的云浏览器在网页上建。
3. **入口与图片**：仓库根目录 `main.py`（沿用昨天的生成器，改日期/标题），默认输出 `/output/entry.png`；**1024×1024 PNG，≤ 1 MiB，两次运行字节完全相同**。
4. **LICENSE**：MIT，含 `SPDX-License-Identifier: MIT` 行，Copyright 2026 135479sun-glitch。
5. **README 徽章**：按模板加 3 个 make.fun live 徽章（比赛徽章 + 本仓库 rank/reward 徽章，owner/repo 填 `135479sun-glitch/news-image-20261121`）及比赛页链接。
6. **GitHub About**：website = https://make.fun/bounty/news-image-20261121；topics 至少含 `makefun`，推荐再加 `ai-agents`、`bounties`、`growth`。
7. **news.json**：按第四节 6 条 + 模型挑出的最佳文案写；`sources` 用上面真实引用的媒体名单。
8. **Transcript bundle**：提交前重取 usage、重建 bundle、本地 check 全过（`failed: []`），entry_message 里填新 bundle 的 sha256；脱敏复核（邮箱 0 次、Gemini key 前缀加 `--redact "AQ.Ab8RN6"`）。
9. **提交**：用 agent keypair 提交（`--keypair /home/hatch/.makefun/keypairs/https_make.fun.json`），**不用 Sun 的 Phantom 签名**；提交后记录 submission id。每天最多 10 次、总共最多 40 次。
10. **时间**：以上全部须在 **2026-11-23 08:00 AWST** 前完成并提交；建议 2026-11-22 20:00 前提交（按周计划），留出重试余量。
11. **收尾纪律**：提交确认成功后，删除标志文件 `~/workspace/make-fun/.work-block-active`，并停掉 Kaggle 笔记本会话，省额度；没提交成功之前不许停会话。

## 六、其他核查发现

- 昨天那单的 6 条（ICJ、深圳峰会、基辅空袭、Anthropic 上市、胡塞袭击利雅得、波兰导弹）是 11 月 20 日的新闻，**今天不能重复用**——今天的 6 条全部是 11 月 21 日的新进展（其中第 1 条的 Anthropic 跌 9% 是昨天的后续，但本条主角是整个市场暴跌，不是 Anthropic 本身，不重复）。
- 比赛目前 0 个参赛作品（刚开赛不久），但 11 月 20 日那场已有 16,286 个作品，同题材竞争会很激烈；图片的**可读性与视觉冲击**（大标题、关键数字、清晰分区）比多堆一条新闻更重要。
- 第 5 条的无人机说法、第 6 条的“消失”表述，模型改写时必须保留“claims / in a trial”的限定，删掉限定会变成假新闻，宁可换备选也不要写错。
