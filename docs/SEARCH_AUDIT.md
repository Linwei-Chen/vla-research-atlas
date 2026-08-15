# VLA 部署期在线适应与持续学习：检索与证据审计

> 完成等级：**L1 结构化范围扫描**；截止日期：2026-08-09。

## 范围与截止日期

- 领域同义词：vision-language-action、VLA、robot foundation policy、online adaptation、test-time adaptation、continual/lifelong robot learning、reinforcement fine-tuning、human intervention。
- 核心问题：部署时用什么新信号更新何种状态，能否持续改进且保留旧能力。
- 来源：arXiv 一手论文页、OpenReview 官方条目、PMLR、RSS、IEEE DOI、作者项目页与官方代码仓库。
- 语言与年份：英文一手来源为主；奠基工作至 2026-08-09。
- 成果类型：论文与少量作者项目/代码佐证；不以二手综述、聚合博客或搜索摘要独立支撑结论。
- 完整范围合同另见 `planning/research_contract.yaml`。

## 查询日志

完整机器日志见 `planning/search_ledger.jsonl`。本次执行了协议规定的七类查询家族，并补充一个桥接查询；“命中”指限时检索界面实际展示并进入候选池的记录，不伪称数据库总命中量。

| 日期 | 来源 | 精确查询式 | 可见命中 | 纳入 | 备注 |
|---|---|---|---:|---:|---|
| 2026-08-09 | arXiv | `site:arxiv.org vision language action continual learning robot deployment online adaptation VLA` | 4 | 3 | 发现在线与持续 VLA 前沿；一项留队列 |
| 2026-08-09 | OpenReview | `site:openreview.net vision language action online adaptation robot continual learning` | 8 | 1 | 核验 RICL 正式状态 |
| 2026-08-09 | PMLR/RSS | `site:roboticsproceedings.org robot human intervention online learning deployment policy` | 5 | 1 | 纳入 Sirius 桥接闭环 |
| 2026-08-09 | arXiv/OpenReview | `site:arxiv.org "reinforcement fine-tuning" "vision-language-action" robot` | 6 | 3 | 纳入三类在线强化设计 |
| 2026-08-09 | 作者项目/PMLR | `OpenVLA-OFT official paper CoRL 2025 fine tuning real robot adaptation` | 5 | 2 | 区分适配底座与在线学习 |
| 2026-08-09 | arXiv/RSS | `site:arxiv.org VLA robot human intervention online learning corrective feedback vision language action` | 4 | 2 | 人类纠错与语言安全门控 |
| 2026-08-09 | TMLR/官方出版页 | `RoboCat self improving robotic agent official paper continual learning` | 6 | 1 | 完成版本族去重 |

## 纳入与排除

纳入必须满足：直接定义路线、关键机制或部署评测；存在稳定一手入口；对地图贡献不可替代信息；与截止日一致。最终从 18 个候选中纳入 12 个，排除 6 个。逐条结果见 `planning/screening.csv`。

主要排除情形：

- RT-2、π0：重要 VLA 基线，但没有本地图要求的部署期更新机制。
- ThriftyDAgger、AIM：人类干预重要近邻；限时 L1 中已有更接近完整部署学习闭环的 Sirius，故留入扩展队列。
- CRL-VLA：高度相关前沿预印本，但未完成正文审计。
- RFTF：OpenReview 撤回版本与后续 workshop 版本并存，版本状态尚未完全消解。

## 去重与版本族

按 DOI、arXiv/OpenReview 稳定 ID、正式 URL、规范题名与第一作者依次去重。RoboCat 的预印本题名含“Generalist Agent”，TMLR 正式版含“Foundation Agent”，其方法与版本说明表明属于同一工作族，正式版为主记录。OpenVLA 与 OpenVLA-OFT 方法目标不同，未误合并。预印本的 arXiv DOI 不被当作正式同行评议 DOI。

## 证据分级与主张审计

- A：直接且已同行评议的 VLA 适应/持续学习证据，如 RICL、CLARE。
- B：正式但存在任务或模型迁移距离，如 OpenVLA、Sirius、Never Stop Learning、RoboCat。
- C：直接但仍为预印本，或尚缺独立验证，如 2025–2026 在线强化工作。

每条核心主张的 V/D/P/Q 向量、证据位置与审计状态见 `planning/claim_ledger.csv`。具体数字没有在跨论文表格中直接比较，因为任务、动作表示、机器人、数据预算与成功率定义不一致。

## 反证与负面结果检索

执行了 failure、limitation、negative result、robustness、human intervention、distribution shift 等组合。主要结果：ROAD-VLA 的文本特权教师负面消融；Agentic-VLA 的奖励投机、记忆扩展与物理部署复杂性；ROVE 对不完美干预的显式建模；Sirius 对人类监督负担的系统折中。没有发现足以支持“完全无人监督、长期真实部署且无遗忘”的一手证据。

## L2 五道闸门

| 闸门 | 状态 | 说明 |
|---|---|---|
| 范围与来源 | 部分通过 | 范围冻结、七类查询已执行；部分入口限流 |
| 分支代表性 | 部分通过 | 五条主要路线有代表作，但非每条都有奠基、前沿、反证、真实部署四类位置 |
| 边际收敛 | 未通过 | 未完成两个独立来源的两轮低于 5% 边际新增审计，也未逐分支做前后向追踪 |
| 深读 | 部分通过 | 核心机制已读摘要或正文；RICL 受 OpenReview 限流，仅做到摘要级 |
| 证据审计 | 部分通过 | 12 条核心主张已登记，仍缺独立复现与更长任务序列审计 |

因此元数据、报告首页和本审计一致标为 L1。

## 失败入口与覆盖限制

- OpenReview 对 RICL 与 RoboCat 的重复打开出现 429/浏览器验证；已使用首次官方条目、arXiv/TMLR 元数据和官方出版页交叉核验，但不声称读取了受限正文。
- 本次没有系统扫描 IEEE Xplore、ACM DL、Scopus、Web of Science 或引用数据库全量索引。
- 2026 年前沿更新快，预印本的正式状态、代码发布和后续修订可能变化。
- 未完成所有路线的前向/后向引用链与独立复现搜索；这正是 L1 而非 L2 的主要原因。
- 独立前向执行环境最初没有 Playwright，应用内浏览器又拒绝 `file://`，因此执行者当时只声明严格静态验证。公开发布前，维护者已在具备 Playwright 的环境用当前模板复跑：12 个详情、7 个非空聚合组、桌面悬停/选择/切换/取消、键盘、375px 手机与 `file://` 均通过。该补充 QA 不改变检索覆盖等级，地图仍为 L1。
