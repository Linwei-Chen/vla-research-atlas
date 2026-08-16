# VLA 部署期在线适应与持续学习研究地图

<!-- generated-complete-readme:v1 -->
> 按更新信号与部署闭环强度，从即时上下文适应下钻到长期持续学习

**完整文字版综述：** 本 README 已直接收录领域全貌、综合报告、检索与证据审计，以及全部 12 项工作的逐篇解读。无需打开网页即可阅读全部研究内容；[在线地图](https://linwei-chen.github.io/vla-research-atlas/)仅提供可选的可视化筛选与机制图。

[在线地图](https://linwei-chen.github.io/vla-research-atlas/) · [结构化真源](https://github.com/Linwei-Chen/vla-research-atlas/blob/main/atlas.json) · [原始综合报告](docs/REPORT.md) · [原始检索审计](docs/SEARCH_AUDIT.md)

## 阅读导航

1. [研究全貌](#研究全貌)
2. [路线与层级](#路线与层级)
3. [综合报告](#综合报告)
4. [全部研究工作](#全部研究工作)
5. [检索与证据审计](#检索与证据审计)
6. [复现与使用边界](#复现与使用边界)

<a id="研究全貌"></a>
## 研究全貌

**领域概览：** 该领域的关键差异不是模型规模，而是部署时什么发生变化：上下文、语言提示、少量任务数据、交互轨迹、策略参数或可扩展模块。地图以决定性更新信号划分五条路线，并以更新发生的时间尺度划分四级闭环。直接 VLA 证据目前集中在少样本后训练、在线强化学习和适配器式持续学习；实体机器人、长期开放世界和安全触发的联合证据仍稀疏。

**研究领域：** 机器人视觉—语言—动作模型在部署期的在线适应与持续学习

**核心判断：** 部署期适应正在从批次式少样本微调走向由奖励、干预和记忆驱动的闭环更新，但稳定性、真实机器人交互成本和跨任务遗忘仍是决定可部署性的三条硬约束。

**阅读建议：** 先读 RICL、Sirius、VLA-RL、RoboCat 与 CLARE 建立五条路线，再用 ROAD-VLA 的负面结果和 OpenVLA-OFT 的部署工程证据校正直觉。

**范围与纳排边界：** L1 结构化范围扫描。纳入直接研究 VLA 部署期适应的工作，以及少量不可替代的在线机器人学习桥接证据；排除只有离线预训练或零样本泛化、没有部署期更新机制的工作。检索截至 2026-08-09，不声称穷尽。

**覆盖说明：** 已覆盖主要机制分支并核验核心一手入口，但未完成每个分支的双轮边际收敛、完整前后向引用链与独立复现审计。

**目标读者：** 机器人学习、具身智能与多模态模型研究人员

**内容语言：** zh-CN

| 维度 | 数值 |
|---|---|
| 纳入成果 | 12 项 |
| 年份范围 | 2021—2026 |
| 研究路线 | 5 条 |
| 分析层级 | 4 个 |
| 覆盖等级 | L1 |
| 资料截止 | 2026-08-09 |
| 第二轴 | 部署闭环强度 |

<a id="路线与层级"></a>
## 路线与层级

| 路线（ID） | 收录 | 判定问题 | 说明 |
|---|---:|---|---|
| 上下文、检索与语言转向 / 上下文/语言（`context-memory`） | 2 | 能否不改 VLA 参数，仅改变输入上下文或外部控制信号就适应新任务与失误？ | 冻结底层 VLA，通过示例检索、历史上下文或动态语言反馈改变当前行为。 |
| 少样本参数适配 / 少样本微调（`fewshot-parameter`） | 3 | 在进入稳定运行前，少量目标数据如何以可承受的算力和延迟完成策略适配？ | 用少量目标任务或部署数据更新全部参数、低秩参数或动作头，使通用策略贴合新任务、环境或具身。 |
| 人类介入与纠错学习 / 人类纠错（`human-intervention`） | 2 | 何时请求人类、如何吸收不完美纠正，并在继续部署时改进策略？ | 从部署中的接管、纠正和隐式信任信号学习，同时控制监督负担与劣质干预的影响。 |
| 奖励驱动在线后训练 / 在线强化（`reward-online`） | 3 | 稀疏且昂贵的机器人反馈如何转化为稳定、样本高效的在线 VLA 更新？ | 利用在线交互、过程奖励、价值估计或自蒸馏突破行为克隆上限。 |
| 持续积累与抗遗忘 / 持续学习（`continual-retention`） | 2 | 模型如何跨任务长期增长，同时控制灾难性遗忘、存储和任务标识依赖？ | 在任务序列中积累新技能，通过数据循环、模块扩展、路由或受控更新保持旧能力。 |

| 层级 | 说明 |
|---|---|
| 任务内即时适应 / 即时（`0`） | 推理期间改变上下文、检索结果或语言控制，底层 VLA 参数保持冻结。 |
| 少量数据批次更新 / 批次（`1`） | 收集少量目标任务或环境数据后再更新模型，尚未形成每次执行都在线优化的闭环。 |
| 部署交互闭环更新 / 在线（`2`） | 机器人在部署或任务训练阶段滚动收集反馈并多轮更新策略。 |
| 跨任务长期积累 / 长期（`3`） | 连续任务或具身序列中反复学习，显式关注旧技能保持、路由或自生成数据循环。 |

<a id="综合报告"></a>
## 综合报告

### VLA 部署期在线适应与持续学习：领域全貌与路线地图

> 完成等级：**L1 结构化范围扫描**；检索截止：2026-08-09。本文不声称穷尽，所有比较均受各论文任务、机器人与评测设置限制。

#### 范围合同

本地图回答：视觉与语言条件的机器人动作模型，在部署时如何利用新观测、示范、纠正或奖励改善当前任务，并在后续任务中保留旧能力？目标读者是机器人学习和具身智能研究人员。核心对象是输出实体机器人动作或动作块的 VLA；少量非 VLA 视觉机器人学习工作仅在提供不可替代的部署闭环机制时纳入，并标为桥接证据。

纳入部署期上下文变化、少量目标数据微调、多轮交互更新与跨任务持续积累。排除只有离线预训练或零样本泛化、纯感知测试时适应、纯语言智能体、营销材料和无法核验一手入口的成果。

#### 领域全貌

目前最重要的不是模型有多大，而是部署时到底更新什么、多久更新一次、用什么信号更新：

1. **即时上下文**改变输入，不动底层参数，适应快但受检索与提示可靠性限制。
2. **少样本参数适配**以任务示范换取具身或任务贴合，工程成熟度相对高，但通常仍是部署前批次操作。
3. **人类介入**把失败附近的接管变成高价值数据，同时带来监督负担和干预质量问题。
4. **奖励驱动在线后训练**突破行为克隆的离线数据上限，但受稀疏奖励、探索成本、价值偏差与安全约束限制。
5. **持续积累与抗遗忘**把单次适应扩展为任务序列，必须同时管理旧数据、模块增长、路由和稳定性—可塑性冲突。

证据结构很不均衡。[RICL](https://openreview.net/forum?id=6AASPlloSt) 与 [CLARE](https://doi.org/10.1109/LRA.2026.3693992) 提供了直接且已同行评议的 VLA 适应证据；[VLA-RL](https://arxiv.org/abs/2505.18719)、[ROAD-VLA](https://arxiv.org/abs/2606.25800)、[Agentic-VLA](https://arxiv.org/abs/2605.22896) 和 [ROVE](https://arxiv.org/abs/2606.17011) 更直接面向在线闭环，却仍以预印本和模拟为主。

#### 路线与第二轴

主要路线按一次适应循环中的决定性更新信号互斥归类；辅助机制通过 `routes` 连接，不重复计数。

| 路线 | 更新对象/信号 | 代表工作 | 典型优势 | 主要失败方式 |
|---|---|---|---|---|
| 上下文、检索与语言转向 | 示例上下文、语言反馈 | RICL、VLA Steering | 无测试时参数更新，响应快 | 检索错配、提示脆弱、动作语义鸿沟 |
| 少样本参数适配 | 全量/低秩参数、动作表示 | OpenVLA、OpenVLA-OFT | 接口清晰、工具链较成熟 | 仍需数据与停机训练，可能遗忘 |
| 人类介入与纠错 | 接管轨迹、信任或优势 | Sirius、ROVE | 直接覆盖失败附近状态 | 监督负担、犹豫或错误接管 |
| 奖励驱动在线后训练 | 稀疏/过程奖励、价值估计 | VLA-RL、ROAD-VLA、Agentic-VLA | 可超越示范上限 | 奖励投机、探索成本、不安全交互 |
| 持续积累与抗遗忘 | 自生成数据、适配器扩展与路由 | RoboCat、CLARE | 跨任务增长与保留 | 数据/模块增长、路由误判、长序列证据不足 |

第二轴是“部署闭环强度”，从任务内无参数适应、少量数据批次更新、部署交互闭环更新到跨任务长期积累。它描述时间尺度与闭环深度，不代表证据质量；证据质量另由 A/B/C 和 V/D/P/Q 记录。

#### 时间线

- **2021**：[Never Stop Learning](https://proceedings.mlr.press/v155/julian21a.html) 证明简单继续强化微调是视觉机器人持续适应的强基线，但不是 VLA。
- **2023**：[Sirius](https://roboticsproceedings.org/rss19/p005.html) 形成“部署—接管—加权学习”闭环；[RoboCat](https://openreview.net/forum?id=vsCpILiWHu) 展示“少量示范—自主生成—回灌训练”的阶段式自改进。
- **2025**：[OpenVLA](https://proceedings.mlr.press/v270/kim25c.html) 与 [OpenVLA-OFT](https://arxiv.org/abs/2502.19645) 降低开放 VLA 下游适配和高频部署门槛；RICL 把适应移到测试时上下文；VLA-RL 把在线交互与过程奖励带入自回归 VLA 后训练。
- **2026**：语言转向、ROVE、ROAD-VLA、Agentic-VLA 细分了语言反馈、人类干预、动作空间自蒸馏和系统级在线适应；CLARE 则给出正式同行评议的无样本回放、无任务标签持续路由方案。

#### 核心判断

**无参数适应和参数更新并非替代关系。** RICL 需要先通过专门训练获得上下文学习能力；语言转向也要额外训练反馈策略与门控。因此“冻结 VLA”只说明底层模型不更新，不代表系统没有适应成本。

**在线强化的瓶颈首先是监督和系统，而非单一优化器。** VLA-RL构造过程奖励，ROAD-VLA把优势转为动作 token 级教师，Agentic-VLA联合奖励合成、探索和记忆。三者分别回答“奖励太稀疏”“符号指导离动作太远”“系统反复冷启动”三个问题。

**长期持续学习必须显式处理旧能力。** RoboCat靠旧数据与新生成数据回灌，CLARE通过模块扩展和自动路由隔离更新。简单顺序微调或低秩微调是否已经足够强，仍需与更复杂抗遗忘方法在相同长任务序列中比较。

**真实部署证据不能由模拟成功替代。** Sirius、ROVE、RoboCat、OpenVLA-OFT 和 CLARE 含不同程度的实体机器人证据，但任务、硬件和反馈成本不统一；当前没有足以横向比较的长期开放世界基准。

#### 负面证据、争议与空白

- ROAD-VLA 报告：在其设置中，基于示范、检索经验或高层计划的文本特权教师不能有效适应低层 VLA 动作。这一结果反驳“更多语言上下文必然改善动作”的朴素假设，但不能外推到所有多模态教师设计。
- Agentic-VLA 的正文讨论承认奖励投机、经验记忆扩展和组件复杂度会阻碍实体机器人部署。
- 人类干预不是天然专家标签。ROVE 的出发点正是接管可能犹豫、低效或错误；直接行为克隆可能吸收这些缺陷。
- “少样本微调”“测试时适应”“在线学习”“持续学习”是不同闭环，不能按词面互换。
- 缺少统一报告：每小时人类监控、失败导致的物理风险、在线 GPU 能耗、恢复时间、旧技能遗忘、任务无标签路由错误和长期数据治理成本。

可证伪的下一步问题包括：动作空间教师是否在不同动作表示上稳定优于语言教师；参数高效顺序强化微调在 50 个以上真实任务序列中是否仍少遗忘；安全门控的漏报率随分布漂移如何变化；自生成数据何时导致错误自增强。

#### 推荐阅读路径

1. 先读 RICL，建立“适应不等于改参数”的接口视角。
2. 读 OpenVLA 与 OpenVLA-OFT，理解底座微调、动作表示和控制延迟的工程边界。
3. 读 Sirius 与 ROVE，对比信任加权行为克隆和价值加权干预学习。
4. 读 VLA-RL 与 ROAD-VLA，理解过程奖励、动作空间监督和负面消融。
5. 最后对照 RoboCat 与 CLARE，比较数据回灌式自改进和模块路由式抗遗忘。

#### 覆盖与限制

本次交付是限时 L1：已形成五条路线、四级第二轴、时间线、纳排日志和一手入口，12 条工作均有详情页。没有通过 L2 的边际收敛和完整引用链闸门；CRL-VLA、Simple Recipe Works、FORCE、ExToken、RFTF、AIM 等仍在更新队列。对预印本只陈述作者材料直接支持的机制与结果，不把其标成正式同行评议。

<a id="全部研究工作"></a>
## 全部研究工作（12 项）

以下条目严格保持 `atlas.json` 的策展顺序，并在 README 内直接列出问题、机制、证据、局限、启示、核验边界与全部可用来源。

<a id="paper-ricl-2025"></a>
**1. RICL：为预训练视觉—语言—动作模型加入上下文适应能力｜RICL: Adding In-Context Adaptability to Pre-Trained Vision-Language-Action Models（2025 · Conference on Robot Learning (CoRL 2025)）**

**作者：** Kaustubh Sridhar、Souradeep Dutta、Dinesh Jayaraman、Insup Lee

**书目：** 年份 2025；载体 Conference on Robot Learning (CoRL 2025)；状态 同行评议；来源类型 paper

**分类：** 主路线 上下文、检索与语言转向；相关路线 上下文、检索与语言转向、少样本参数适配；层级 任务内即时适应；阅读层级 核心；证据等级 A；简称 RICL；相关性排序 1

**核验：** 来源层级 T1；核验状态 abstract-checked；V/D/P/Q V=V2 / D=D2 / P=P2 / Q=Q2

**定位：** 先用小规模示范微调赋予 VLA 上下文学习接口，再在测试时通过检索示例适应新任务。

**问题：** 通用 VLA 对新任务常只能依赖零样本泛化，终端用户缺少无需再次更新参数的教学接口。

**机制：** 方法用少量机器人示范对预训练 VLA 做后置训练，使其能读取检索到的相关轨迹上下文，并据此输出当前动作。

**步骤：**

1. 收集小规模带任务变化的机器人示范
2. 后置微调使 VLA 学会利用上下文
3. 为当前任务检索相关示例
4. 冻结模型并基于示例上下文执行

**证据：**

- CoRL 2025 官方 OpenReview 条目明确将其描述为向预训练 VLA 注入上下文适应能力。
- 论文报告可通过检索增强与上下文学习在不做测试时参数微调的情况下执行新任务。

**局限：**

- 测试时虽然不更新参数，但能力依赖先前的专门微调配方和示范库。
- 检索失败、上下文长度与示范分布外泛化仍是部署边界。

**意义：**

- 证明‘部署适应’不必等同于参数更新。
- 为用户可教接口与外部记忆路线提供直接 VLA 证据。

**边界：** T1；CoRL 2025 官方 OpenReview 元数据与摘要核验。页面二次打开出现限流，因此未把未读取的正文细节写入证据。

**标识：** 工作族 ID ricl

**证据位置：**

- OpenReview 官方摘要与 TL;DR

**资源：** [一手入口](<https://openreview.net/forum?id=6AASPlloSt>)

**关联 ID：** `vla-steering-2026` · `openvla-2025`

---

<a id="paper-vla-steering-2026"></a>
**2. 学习如何对 VLA 说话：低伤害的视觉—语言—动作模型转向｜Learning What to Say to Your VLA: Mostly Harmless Vision Language Action Model Steering（2026 · arXiv）**

**作者：** Hyun Joe Jeong、Gokul Swamy、Andrea Bajcsy

**书目：** 年份 2026；载体 arXiv；状态 预印本；来源类型 paper

**分类：** 主路线 上下文、检索与语言转向；相关路线 上下文、检索与语言转向、人类介入与纠错学习；层级 任务内即时适应；阅读层级 核心；证据等级 C；简称 VLA Steering；相关性排序 6

**核验：** 来源层级 T1；核验状态 full-text-checked；V/D/P/Q V=V3 / D=D2 / P=P1 / Q=Q2

**定位：** 交互搜索有效语言序列，并用经保形校准的改进头决定何时向冻结 VLA 注入语言反馈。

**问题：** 语义相近的指令可能诱发差异很大的机器人行为，普通提示不能可靠触发已有能力。

**机制：** 系统搜索能改善闭环表现的语言序列，将其蒸馏为测试时语言反馈策略，并校准一个改进预测器来避免有害转向。

**步骤：**

1. 在闭环执行中搜索候选语言反馈
2. 将有效序列蒸馏为语言反馈策略
3. 用改进头预测当前转向是否有益
4. 仅在校准门控允许时作用于冻结 VLA

**证据：**

- 官方摘要明确说明底层 VLA 保持冻结，且不需要原始训练分布。
- 作者在模拟与硬件以及视觉、语义扰动下报告了改进与恢复行为。

**局限：**

- 当前为预印本，外部复现和正式评审尚不足。
- 保证针对‘不降低基线表现’的门控，不等同于通用物理安全保证。

**意义：**

- 把语言从静态任务描述升级为部署时反馈通道。
- 展示安全门控可与无参数适应结合。

**边界：** T1；arXiv 元数据、摘要及 HTML 正文方法说明核验；数值不作为本地图核心比较结论。

**标识：** 工作族 ID vla-language-steering

**证据位置：**

- arXiv 摘要
- 方法章节：语言反馈策略与保形改进头

**资源：** [一手入口](<https://arxiv.org/abs/2606.12299>)

**关联 ID：** `ricl-2025` · `sirius-2023`

---

<a id="paper-openvla-2025"></a>
**3. OpenVLA：开源视觉—语言—动作模型｜OpenVLA: An Open-Source Vision-Language-Action Model（2025 · Conference on Robot Learning, PMLR 270）**

**作者：** Moo Jin Kim、Karl Pertsch、Siddharth Karamcheti、Ted Xiao、Chelsea Finn

**书目：** 年份 2025；载体 Conference on Robot Learning, PMLR 270；状态 同行评议；来源类型 paper

**分类：** 主路线 少样本参数适配；相关路线 少样本参数适配；层级 少量数据批次更新；阅读层级 背景；证据等级 B；简称 OpenVLA；相关性排序 9

**核验：** 来源层级 T1；核验状态 abstract-checked；V/D/P/Q V=V2 / D=D1 / P=P2 / Q=Q2

**定位：** 提供可在消费级 GPU 上用低秩方法微调的开源通用 VLA，是后续部署适配研究的常用底座。

**问题：** 闭源或难微调的通用机器人策略阻碍对新任务、具身和部署约束的可重复适配。

**机制：** 在视觉语言骨干上训练动作输出，并提供低秩微调与量化路径，使研究者能以较低资源进行下游适配。

**步骤：**

1. 以多来源机器人示范预训练通用 VLA
2. 在目标任务数据上进行全量或低秩微调
3. 按部署硬件选择量化与推理配置
4. 在目标机器人上闭环执行

**证据：**

- PMLR 正式论文页确认 OpenVLA 可用现代低秩适配方法在消费级 GPU 上微调。
- 正式摘要将下游微调定位为从通用模型获得鲁棒视觉运动策略的路径。

**局限：**

- 论文主体是模型与离线下游微调，不是执行中的持续在线学习。
- 低秩微调可行性不能自动推出跨任务无遗忘。

**意义：**

- 构成许多在线强化与少样本适配工作的开放实验底座。
- 把部署适配的算力门槛纳入研究问题。

**边界：** T1/T2；PMLR 正式论文页与官方代码仓库核验。仅作为少样本参数适配底座，不把它表述为在线学习方法。

**标识：** 工作族 ID openvla

**证据位置：**

- PMLR 正式摘要与书目信息

**资源：** [一手入口](<https://proceedings.mlr.press/v270/kim25c.html>) · [代码](<https://github.com/openvla/openvla>)

**关联 ID：** `openvla-oft-2025` · `vla-rl-2025` · `ricl-2025`

---

<a id="paper-openvla-oft-2025"></a>
**4. 微调视觉—语言—动作模型：优化速度与成功率｜Fine-Tuning Vision-Language-Action Models: Optimizing Speed and Success（2025 · arXiv）**

**作者：** Moo Jin Kim、Chelsea Finn、Percy Liang

**书目：** 年份 2025；载体 arXiv；状态 预印本；来源类型 paper

**分类：** 主路线 少样本参数适配；相关路线 少样本参数适配；层级 少量数据批次更新；阅读层级 桥接；证据等级 C；简称 OpenVLA-OFT；相关性排序 8

**核验：** 来源层级 T1；核验状态 full-text-checked；V/D/P/Q V=V3 / D=D1 / P=P1 / Q=Q2

**定位：** 以并行解码、动作分块、连续动作和回归目标把 VLA 微调结果转化为高频可执行策略。

**问题：** 普通 VLA 微调后的动作生成速度、控制频率和任务成功率不足以满足真实机器人部署。

**机制：** OFT 联合改变动作表示、解码方式和训练目标；OFT+ 进一步用 FiLM 增强语言条件，从而兼顾控制效率与指令响应。

**步骤：**

1. 准备目标机器人示范
2. 用连续动作和回归目标微调
3. 通过并行解码与动作分块生成控制序列
4. 在高频真实机器人任务上执行

**证据：**

- 作者项目页明确列出并行解码、动作分块、连续动作表示和 L1 回归四个组成。
- 项目页报告了 LIBERO 与双臂 ALOHA 的模拟及真实机器人评测。

**局限：**

- 这是部署前批次微调配方，不包含运行中的在线数据选择或持续更新。
- 主要比较来自作者项目与预印本，需独立复现后再外推到其他机器人。

**意义：**

- 说明适应质量必须与控制延迟、动作接口共同评估。
- 为在线方法提供更可部署的初始化策略。

**边界：** T1/T2；arXiv 论文入口与作者项目页核验。避免把项目页数值写成跨设置通用结论。

**标识：** 工作族 ID openvla-oft

**证据位置：**

- 作者项目页 TLDR 与 Experimental Results
- 论文方法：OFT recipe

**资源：** [一手入口](<https://arxiv.org/abs/2502.19645>) · [项目页](<https://openvla-oft.github.io/>) · [代码](<https://github.com/moojink/openvla-oft>)

**关联 ID：** `openvla-2025` · `never-stop-learning-2021`

---

<a id="paper-never-stop-learning-2021"></a>
**5. 永不停止学习：机器人强化学习中微调的有效性｜Never Stop Learning: The Effectiveness of Fine-Tuning in Robotic Reinforcement Learning（2021 · Conference on Robot Learning, PMLR 155）**

**作者：** Ryan Julian、Benjamin Swanson、Gaurav Sukhatme、Sergey Levine、Chelsea Finn、Karol Hausman

**书目：** 年份 2021；载体 Conference on Robot Learning, PMLR 155；状态 同行评议；来源类型 paper

**分类：** 主路线 少样本参数适配；相关路线 少样本参数适配、持续积累与抗遗忘、奖励驱动在线后训练；层级 跨任务长期积累；阅读层级 桥接；证据等级 B；简称 Never Stop Learning；相关性排序 12

**核验：** 来源层级 T1；核验状态 abstract-checked；V/D/P/Q V=V2 / D=D1 / P=P2 / Q=Q2

**定位：** 在 VLA 之前证明视觉机器人策略可用离线数据启动的强化微调适应外观、形状、光照和机器人形态变化。

**问题：** 静态机器人策略在部署分布变化后通常不再更新，重新训练的数据代价很高。

**机制：** 从已有离线数据与预训练策略出发，对离策略强化学习策略继续微调，并在多种变化及分段持续设置中检验适应。

**步骤：**

1. 加载原任务离线数据与策略
2. 在目标变化下继续离策略强化微调
3. 评估新条件表现
4. 在后续变化中重复适配

**证据：**

- PMLR 正式摘要报告了背景、物体、光照和机器人形态变化下的适应。
- 正式摘要同时说明在 episodic continual learning 设置中检验了稳健性。

**局限：**

- 不是语言条件 VLA，属于机制桥接证据。
- 批次式适应与现代大模型的参数、延迟和遗忘行为可能不同。

**意义：**

- 为‘持续微调本身可能是强基线’提供历史依据。
- 提醒现代 VLA 工作必须与简单继续训练比较。

**边界：** T1；PMLR 正式论文页核验。明确标注为非 VLA 的视觉机器人强化学习桥接工作。

**标识：** 工作族 ID never-stop-learning

**证据位置：**

- PMLR 正式摘要

**资源：** [一手入口](<https://proceedings.mlr.press/v155/julian21a.html>)

**关联 ID：** `openvla-oft-2025` · `robocat-2023`

---

<a id="paper-sirius-2023"></a>
**6. 机器人在岗学习：部署期间的人机协作自主与学习｜Robot Learning on the Job: Human-in-the-Loop Autonomy and Learning During Deployment（2023 · Robotics: Science and Systems XIX）**

**作者：** Huihan Liu、Soroush Nasiriany、Lance Zhang、Zhiyao Bao、Yuke Zhu

**书目：** 年份 2023；载体 Robotics: Science and Systems XIX；状态 同行评议；来源类型 paper

**分类：** 主路线 人类介入与纠错学习；相关路线 人类介入与纠错学习、持续积累与抗遗忘；层级 部署交互闭环更新；阅读层级 核心；证据等级 B；简称 Sirius；相关性排序 4

**核验：** 来源层级 T1；核验状态 full-text-checked；V/D/P/Q V=V3 / D=D1 / P=P2 / Q=Q2

**定位：** 让机器人承担可靠片段、人类接管困难片段，并按近似人类信任对部署数据加权学习。

**问题：** 纯自主策略脆弱，而全程遥操作代价高；部署既要保持任务完成，也要积累能改进策略的数据。

**机制：** Sirius 在运行中由人类监控并按需干预，再以近似人类信任对收集样本加权，用加权行为克隆更新策略。

**步骤：**

1. 机器人自主执行可靠片段
2. 人类在困难状态接管
3. 记录机器人与干预轨迹及信任代理
4. 加权行为克隆更新后继续部署

**证据：**

- RSS 正式论文页明确说明部署期间的人类监控、按需干预和从任务执行数据继续学习。
- 作者在模拟和真实硬件接触丰富操控任务上与基线比较。

**局限：**

- 原方法不是大规模 VLA，迁移到 VLA 时人类信任代理与动作接口需重新验证。
- 持续人类监控仍可能成为规模化瓶颈。

**意义：**

- 给出完整的‘安全完成任务—收集纠正—策略更新’部署闭环。
- 为 VLA 人类干预后训练提供强机制桥接。

**边界：** T1/T2；RSS 正式论文页与 DOI 核验。非 VLA，但研究对象正是部署中的实体机器人在线协作学习。

**标识：** DOI 10.15607/RSS.2023.XIX.005；工作族 ID sirius

**证据位置：**

- RSS 官方摘要
- 方法：trust-weighted behavioral cloning

**资源：** [一手入口](<https://roboticsproceedings.org/rss19/p005.html>) · [项目页](<https://ut-austin-rpl.github.io/sirius/>)

**关联 ID：** `rove-2026` · `vla-steering-2026`

---

<a id="paper-rove-2026"></a>
**7. ROVE：通过强化学习释放人类干预对人形机器人操控的价值｜ROVE: Unlocking Human Interventions for Humanoid Manipulation via Reinforcement Learning（2026 · arXiv）**

**作者：** Wei Xiao、Weiliang Tang、Yuying Ge、Hui Zhou、Yao Mu、Li Zhang、Yixiao Ge

**书目：** 年份 2026；载体 arXiv；状态 预印本；来源类型 paper

**分类：** 主路线 人类介入与纠错学习；相关路线 人类介入与纠错学习、奖励驱动在线后训练；层级 部署交互闭环更新；阅读层级 核心；证据等级 C；简称 ROVE；相关性排序 5

**核验：** 来源层级 T1；核验状态 abstract-checked；V/D/P/Q V=V2 / D=D2 / P=P1 / Q=Q2

**定位：** 用乐观价值估计从质量参差的部署接管轨迹中筛出高价值行为，强化微调人形机器人 VLA。

**问题：** 高自由度人形操控的接管轨迹可能犹豫、低效或错误，直接模仿会把缺陷写入策略。

**机制：** 系统收集部署与干预数据，用跨具身人类视频辅助训练价值评估，再以优势信号选择性更新 VLA actor。

**步骤：**

1. 机器人执行并由人类无缝介入
2. 汇总自主与混合质量干预轨迹
3. 训练乐观价值估计器并融合人类视频
4. 按优势信号强化更新 VLA

**证据：**

- arXiv 官方摘要明确描述人形 VLA 部署—干预数据管线和价值驱动更新。
- 作者报告真实世界接触丰富任务中跨多轮 rollout—intervention 持续改进。

**局限：**

- 预印本且系统复杂，价值估计误差可能放大错误干预。
- 需要专门的人形遥操作和跨具身视频，成本与适用性尚未独立验证。

**意义：**

- 把人类纠正从纯专家示范改写为带质量估计的强化信号。
- 直接连接 VLA、人形机器人和多轮部署后训练。

**边界：** T1；arXiv 元数据与摘要核验。未获得独立复现，比较结果按作者报告处理。

**标识：** 工作族 ID rove

**证据位置：**

- arXiv 摘要

**资源：** [一手入口](<https://arxiv.org/abs/2606.17011>)

**关联 ID：** `sirius-2023` · `vla-rl-2025`

---

<a id="paper-vla-rl-2025"></a>
**8. VLA-RL：以可扩展强化学习迈向熟练且通用的机器人操控｜VLA-RL: Towards Masterful and General Robotic Manipulation with Scalable Reinforcement Learning（2025 · arXiv）**

**作者：** Guanxing Lu、Wenkai Guo、Chubin Zhang、Yuheng Zhou、Haonan Jiang、Zifeng Gao、Yansong Tang、Ziwei Wang

**书目：** 年份 2025；载体 arXiv；状态 预印本；来源类型 paper

**分类：** 主路线 奖励驱动在线后训练；相关路线 奖励驱动在线后训练、少样本参数适配；层级 部署交互闭环更新；阅读层级 核心；证据等级 C；简称 VLA-RL；相关性排序 2

**核验：** 来源层级 T1；核验状态 full-text-checked；V/D/P/Q V=V3 / D=D2 / P=P1 / Q=Q2

**定位：** 把自回归 VLA 轨迹写成多模态多轮序列，以过程奖励模型支撑在线强化后训练。

**问题：** 行为克隆只覆盖离线数据访问过的状态，部署遇到分布外状态时缺少探索和失败恢复机制。

**机制：** 框架用在线交互收集轨迹，以自动分段伪标签训练机器人过程奖励模型，并通过课程、并行环境和 critic warmup 稳定优化。

**步骤：**

1. 从预训练自回归 VLA 启动
2. 在目标任务中在线采样完整轨迹
3. 用过程奖励模型对任务片段赋予反馈
4. 强化更新并重复测试时优化

**证据：**

- arXiv 官方摘要明确说明使用在线强化学习改进预训练自回归 VLA。
- 作者在 LIBERO 多任务上与微调基线比较，并报告增加测试时优化可继续受益。

**局限：**

- 主要证据来自模拟基准，真实机器人交互成本和安全性没有同等强度验证。
- 预印本的过程奖励偏差与可复现性仍待审计。

**意义：**

- 把部署时计算从重复推理扩展为策略优化。
- 确立过程奖励、探索与系统吞吐是 VLA 在线强化的共同瓶颈。

**边界：** T1；arXiv 元数据、摘要与 HTML 方法部分核验。性能比较仅按论文设置陈述，不外推为真实部署结论。

**标识：** 工作族 ID vla-rl

**证据位置：**

- arXiv 摘要
- 方法：trajectory-level RL 与 process reward model

**资源：** [一手入口](<https://arxiv.org/abs/2505.18719>)

**关联 ID：** `road-vla-2026` · `agentic-vla-2026` · `openvla-2025`

---

<a id="paper-road-vla-2026"></a>
**9. ROAD-VLA：通过自蒸馏实现视觉—语言—动作模型的鲁棒在线适应｜ROAD-VLA: Robust Online Adaptation via Self-Distillation for Vision-Language-Action Models（2026 · arXiv）**

**作者：** Kejing Wang、Toan Nguyen、Minh Hoang Nguyen、Simon Khan、Flora D. Salim

**书目：** 年份 2026；载体 arXiv；状态 预印本；来源类型 paper

**分类：** 主路线 奖励驱动在线后训练；相关路线 奖励驱动在线后训练、上下文、检索与语言转向；层级 部署交互闭环更新；阅读层级 核心；证据等级 C；简称 ROAD-VLA；相关性排序 3

**核验：** 来源层级 T1；核验状态 full-text-checked；V/D/P/Q V=V3 / D=D2 / P=P1 / Q=Q2

**定位：** 用优势引导的动作空间近端教师把稀疏奖励转为动作 token 级监督，并给出符号教师无效的负面证据。

**问题：** 稀疏奖励难以直接训练高维自回归动作策略，而文本计划或检索经验与低层动作之间存在模态鸿沟。

**机制：** 以校准优势扰动动作 token logits 构造贴近当前策略的教师，再把教师分布自蒸馏回 VLA。

**步骤：**

1. 在线采样动作与稀疏奖励
2. 估计并校准动作优势
3. 在动作 logits 上构造近端教师
4. 以 token 级蒸馏更新学生策略

**证据：**

- 官方摘要明确报告基于示范、检索经验或高层计划的文本特权教师对 VLA 适应无效。
- 作者在七个操控环境的分布内与分布外变化上与 PPO 比较。

**局限：**

- 结论来自预印本且集中于所选模拟环境。
- 理论下界依赖优势校准和教师匹配准确，部署中不一定满足。

**意义：**

- 提供少见的负面结果：更多语言或检索信息不必然转化为低层动作改进。
- 提示在线适应的监督信号应尽量贴近动作空间。

**边界：** T1；arXiv 元数据、摘要与 HTML 正文核验。负面结果限定在作者测试的文本特权教师设计。

**标识：** 工作族 ID road-vla

**证据位置：**

- arXiv 摘要
- 方法：advantage-guided self-distillation
- 实验：privileged teacher ablations

**资源：** [一手入口](<https://arxiv.org/abs/2606.25800>)

**关联 ID：** `vla-rl-2025` · `agentic-vla-2026` · `ricl-2025`

---

<a id="paper-agentic-vla-2026"></a>
**10. Agentic-VLA：视觉—语言—动作模型的高效在线适应｜Agentic-VLA: Efficient Online Adaptation for Vision-Language-Action Models（2026 · arXiv）**

**作者：** Ruofan Jin、Zaixi Zhang

**书目：** 年份 2026；载体 arXiv；状态 预印本；来源类型 paper

**分类：** 主路线 奖励驱动在线后训练；相关路线 奖励驱动在线后训练、上下文、检索与语言转向、持续积累与抗遗忘；层级 跨任务长期积累；阅读层级 核心；证据等级 C；简称 Agentic-VLA；相关性排序 7

**核验：** 来源层级 T1；核验状态 full-text-checked；V/D/P/Q V=V3 / D=D2 / P=P1 / Q=Q1

**定位：** 把自适应奖励合成、语言引导探索和策略权重记忆组合成在线 VLA 适应系统。

**问题：** 在线 VLA 更新同时受制于新环境泛化、稀疏奖励、低效探索和重复任务冷启动。

**机制：** 系统动态合成任务奖励与课程，由语言 critic 引导探索，并检索相似任务的策略权重作为适应热启动。

**步骤：**

1. 根据任务与当前能力生成奖励和子目标
2. 语言 critic 引导结构化探索
3. 在线优化当前 VLA
4. 把权重写入经验记忆并为相似任务检索

**证据：**

- arXiv 官方摘要逐项给出奖励合成、语言引导探索和经验记忆三个模块。
- 作者在 LIBERO 与 RoboTwin 2.0 模拟基准上报告跨任务迁移与更快收敛。

**局限：**

- 论文正文自述存在奖励投机、记忆扩展和复杂系统落地问题。
- 没有同等规模的实体机器人长期部署验证，且尚未同行评议。

**意义：**

- 显示在线适应可能需要系统级协同，而不是单一优化算法。
- 经验记忆连接了单任务在线强化与跨任务持续学习。

**边界：** T1；arXiv 元数据、摘要及 HTML 正文的讨论章节核验；结果限于作者模拟设置。

**标识：** 工作族 ID agentic-vla

**证据位置：**

- arXiv 摘要
- 方法总览
- 讨论：reward hacking、memory scalability、physical deployment

**资源：** [一手入口](<https://arxiv.org/abs/2605.22896>)

**关联 ID：** `vla-rl-2025` · `road-vla-2026` · `clare-2026`

---

<a id="paper-robocat-2023"></a>
**11. RoboCat：面向机器人操控的自改进基础智能体｜RoboCat: A Self-Improving Foundation Agent for Robotic Manipulation（2023 · Transactions on Machine Learning Research）**

**作者：** Konstantinos Bousmalis、Giulia Vezzani、Dushyant Rao、Coline Devin、Alex X. Lee、Maria Bauza、Todor Davchev、Yuxiang Zhou

**书目：** 年份 2023；载体 Transactions on Machine Learning Research；状态 同行评议；来源类型 paper

**分类：** 主路线 持续积累与抗遗忘；相关路线 持续积累与抗遗忘、少样本参数适配；层级 跨任务长期积累；阅读层级 核心；证据等级 B；简称 RoboCat；相关性排序 10

**核验：** 来源层级 T1；核验状态 full-text-checked；V/D/P/Q V=V3 / D=D1 / P=P2 / Q=Q2

**定位：** 用少量新任务示范启动适配，再让当前策略生成数据并回灌总数据集形成自改进循环。

**问题：** 通用机器人需要跨新任务和新机械臂快速适应，而人工数据收集难以持续扩展。

**机制：** RoboCat 先从多具身视觉动作序列学习，对新任务用少量示例适配，随后自主生成更多轨迹并与原数据合并训练下一版本。

**步骤：**

1. 训练多任务多具身视觉动作策略
2. 以新任务少量示范适配
3. 让适配策略自主生成新轨迹
4. 筛选并回灌数据训练下一代模型

**证据：**

- TMLR 版本官方摘要报告了新任务与新机器人适应以及自生成数据的后续训练循环。
- 论文在模拟和三种真实机器人具身上做大规模评估。

**局限：**

- RoboCat 是视觉目标条件策略，不是以自然语言指令为核心接口的现代 VLA，属于近邻直接桥接。
- 自生成数据仍需要任务设置、筛选和阶段式再训练，不是完全自主的开放世界在线学习。

**意义：**

- 提供早期完整的通用机器人‘适应—生成—回灌’增长循环。
- 揭示数据治理与旧数据混合是抗遗忘的重要系统组件。

**边界：** T1/T2；arXiv 版本注明 TMLR 2023，且与 DeepMind 官方出版页交叉核验。标题在早期预印本中使用 Generalist Agent，正式版使用 Foundation Agent，归入同一版本族。

**版本：** 以 TMLR 正式版为主，arXiv:2306.11706 为同一工作公开版本。

**标识：** 工作族 ID robocat

**证据位置：**

- arXiv/TMLR 摘要
- 自改进数据循环说明

**资源：** [一手入口](<https://openreview.net/forum?id=vsCpILiWHu>) · [项目页](<https://deepmind.google/research/publications/35829/>)

**关联 ID：** `clare-2026` · `never-stop-learning-2021`

---

<a id="paper-clare-2026"></a>
**12. CLARE：通过自主适配器路由与扩展实现视觉—语言—动作模型持续学习｜CLARE: Continual Learning for Vision-Language-Action Models via Autonomous Adapter Routing and Expansion（2026 · IEEE Robotics and Automation Letters）**

**作者：** Ralf Römer、Yi Zhang、Yuming Li、Angela P. Schoellig

**书目：** 年份 2026；载体 IEEE Robotics and Automation Letters；状态 同行评议；来源类型 paper

**分类：** 主路线 持续积累与抗遗忘；相关路线 持续积累与抗遗忘、少样本参数适配、上下文、检索与语言转向；层级 跨任务长期积累；阅读层级 核心；证据等级 A；简称 CLARE；相关性排序 1

**核验：** 来源层级 T1；核验状态 full-text-checked；V/D/P/Q V=V3 / D=D2 / P=P2 / Q=Q2

**定位：** 按层级特征相似度选择复用或扩展轻量适配器，并在推理时自动路由，无需任务标签和旧样本。

**问题：** 顺序微调会改写旧表示；传统持续学习又常依赖旧样本、任务标识或随任务线性增长的模块。

**机制：** CLARE 在部分 VLA 模块中放置可扩展适配器，以特征相似度决定何处新增；各适配器配套自编码器式判别器，在部署时按重构误差自动路由。

**步骤：**

1. 冻结预训练骨干并为新任务提取层级特征
2. 按特征相似度决定复用或新增适配器
3. 训练新适配器及其分布判别器
4. 推理时按重构误差逐层自动选择适配器

**证据：**

- 官方条目确认论文已被 IEEE RA-L 2026 接收并给出正式 DOI。
- 论文在 LIBERO 与五个真实机器人任务上评估新任务学习与旧任务保持。

**局限：**

- 任务仍以阶段式数据到达和训练为主，不是每个控制步都更新。
- 模块持续扩展虽为次线性，长期存储、路由误判和极长任务序列仍需验证。

**意义：**

- 提供当前较直接且已同行评议的 VLA 抗遗忘证据。
- 把任务标签依赖转化为可学习的部署时自动路由问题。

**边界：** T1/T2；arXiv 元数据、HTML 正文、RA-L 接收说明与 DOI 核验。核心机制读到方法正文。

**标识：** DOI 10.1109/LRA.2026.3693992；工作族 ID clare

**证据位置：**

- 方法 IV-C：Autonomous Routing
- 方法 IV-D：Dynamic Expansion
- 评估 V：LIBERO 与真实任务

**资源：** [一手入口](<https://doi.org/10.1109/LRA.2026.3693992>) · [项目页](<https://tum-lsy.github.io/clare>)

**关联 ID：** `robocat-2023` · `agentic-vla-2026`

---

<a id="检索与证据审计"></a>
## 检索与证据审计

<details>
<summary><strong>展开完整检索、纳排、去重、证据分级与覆盖限制</strong></summary>

### VLA 部署期在线适应与持续学习：检索与证据审计

> 完成等级：**L1 结构化范围扫描**；截止日期：2026-08-09。

#### 范围与截止日期

- 领域同义词：vision-language-action、VLA、robot foundation policy、online adaptation、test-time adaptation、continual/lifelong robot learning、reinforcement fine-tuning、human intervention。
- 核心问题：部署时用什么新信号更新何种状态，能否持续改进且保留旧能力。
- 来源：arXiv 一手论文页、OpenReview 官方条目、PMLR、RSS、IEEE DOI、作者项目页与官方代码仓库。
- 语言与年份：英文一手来源为主；奠基工作至 2026-08-09。
- 成果类型：论文与少量作者项目/代码佐证；不以二手综述、聚合博客或搜索摘要独立支撑结论。
- 完整范围合同另见 `planning/research_contract.yaml`。

#### 查询日志

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

#### 纳入与排除

纳入必须满足：直接定义路线、关键机制或部署评测；存在稳定一手入口；对地图贡献不可替代信息；与截止日一致。最终从 18 个候选中纳入 12 个，排除 6 个。逐条结果见 `planning/screening.csv`。

主要排除情形：

- RT-2、π0：重要 VLA 基线，但没有本地图要求的部署期更新机制。
- ThriftyDAgger、AIM：人类干预重要近邻；限时 L1 中已有更接近完整部署学习闭环的 Sirius，故留入扩展队列。
- CRL-VLA：高度相关前沿预印本，但未完成正文审计。
- RFTF：OpenReview 撤回版本与后续 workshop 版本并存，版本状态尚未完全消解。

#### 去重与版本族

按 DOI、arXiv/OpenReview 稳定 ID、正式 URL、规范题名与第一作者依次去重。RoboCat 的预印本题名含“Generalist Agent”，TMLR 正式版含“Foundation Agent”，其方法与版本说明表明属于同一工作族，正式版为主记录。OpenVLA 与 OpenVLA-OFT 方法目标不同，未误合并。预印本的 arXiv DOI 不被当作正式同行评议 DOI。

#### 证据分级与主张审计

- A：直接且已同行评议的 VLA 适应/持续学习证据，如 RICL、CLARE。
- B：正式但存在任务或模型迁移距离，如 OpenVLA、Sirius、Never Stop Learning、RoboCat。
- C：直接但仍为预印本，或尚缺独立验证，如 2025–2026 在线强化工作。

每条核心主张的 V/D/P/Q 向量、证据位置与审计状态见 `planning/claim_ledger.csv`。具体数字没有在跨论文表格中直接比较，因为任务、动作表示、机器人、数据预算与成功率定义不一致。

#### 反证与负面结果检索

执行了 failure、limitation、negative result、robustness、human intervention、distribution shift 等组合。主要结果：ROAD-VLA 的文本特权教师负面消融；Agentic-VLA 的奖励投机、记忆扩展与物理部署复杂性；ROVE 对不完美干预的显式建模；Sirius 对人类监督负担的系统折中。没有发现足以支持“完全无人监督、长期真实部署且无遗忘”的一手证据。

#### L2 五道闸门

| 闸门 | 状态 | 说明 |
|---|---|---|
| 范围与来源 | 部分通过 | 范围冻结、七类查询已执行；部分入口限流 |
| 分支代表性 | 部分通过 | 五条主要路线有代表作，但非每条都有奠基、前沿、反证、真实部署四类位置 |
| 边际收敛 | 未通过 | 未完成两个独立来源的两轮低于 5% 边际新增审计，也未逐分支做前后向追踪 |
| 深读 | 部分通过 | 核心机制已读摘要或正文；RICL 受 OpenReview 限流，仅做到摘要级 |
| 证据审计 | 部分通过 | 12 条核心主张已登记，仍缺独立复现与更长任务序列审计 |

因此元数据、报告首页和本审计一致标为 L1。

#### 失败入口与覆盖限制

- OpenReview 对 RICL 与 RoboCat 的重复打开出现 429/浏览器验证；已使用首次官方条目、arXiv/TMLR 元数据和官方出版页交叉核验，但不声称读取了受限正文。
- 本次没有系统扫描 IEEE Xplore、ACM DL、Scopus、Web of Science 或引用数据库全量索引。
- 2026 年前沿更新快，预印本的正式状态、代码发布和后续修订可能变化。
- 未完成所有路线的前向/后向引用链与独立复现搜索；这正是 L1 而非 L2 的主要原因。
- 独立前向执行环境最初没有 Playwright，应用内浏览器又拒绝 `file://`，因此执行者当时只声明严格静态验证。公开发布前，维护者已在具备 Playwright 的环境用当前模板复跑：12 个详情、7 个非空聚合组、桌面悬停/选择/切换/取消、键盘、375px 手机与 `file://` 均通过。该补充 QA 不改变检索覆盖等级，地图仍为 L1。

</details>

<a id="复现与使用边界"></a>
## 复现与使用边界

- `atlas.json` 是人工维护的结构化研究真源；`data/`、网页与本 README 是确定性派生阅读层。
- 页面可离线打开；论文、代码、数据集与官方图表等一手外部入口需要联网。
- 机制步骤与网页机制图是依据一手文字证据形成的解释性整理，不替代原论文图表或独立复核。
- 出版状态、阅读优先级、证据等级与展示层级是不同维度，不能互相替代。
- 本综述有明确截止日期和纳入边界，不声称穷尽互联网中的全部长尾资料。

生成与验证工具：[`build-research-atlas`](https://github.com/Linwei-Chen/build-research-atlas)。
