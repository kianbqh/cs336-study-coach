# CS336 Study Coach

面向 Stanford CS336 的中文 Codex 学习教练 Skill。它用诊断、苏格拉底式辅导、四证据考核和可追溯复盘，帮助学习者形成可以独立解释、推导、实现和迁移的能力。

> 本项目是独立的学习辅助工具，不隶属于 Stanford University 或 OpenAI，不提供课程学分、官方评分或认证，也不包含课程材料、官方答案或第三方作业实现。

## 它解决什么问题

CS336 是一门实现与系统实践密集的课程。只看完视频、记住术语或让 AI 代写代码，都不足以证明真正掌握。本 Skill 把每个核心目标拆成可验证的学习闭环：

1. 先诊断现有理解与前置缺口；
2. 通过提问、推导和最小实验重建概念；
3. 在不泄露官方作业答案的前提下辅导实现与调试；
4. 用四类直接证据验收掌握程度；
5. 生成待确认的复盘和项目状态更新；
6. 只导出已经通过验收的中性能力证据。

设计目标是深度掌握，而不是追求视频观看进度、打卡数量或简历包装。

## 使用前先了解

- 官方 assignment、handout、starter、tests、TODO 及其实质复制版一律采用严格助教模式，不代写、代改或代跑。
- 四证据 gate 是本项目的学习状态模型，不是 Stanford 成绩、证书或招聘背书。
- Spring 2026 只是没有版本锁时的 provisional fallback；学习其他 offering 时应明确锁定对应版本。
- `learning/` 是可选的项目状态目录。没有明确授权时，Skill 不会创建或修改任何状态文件。
- 当前仓库是 standalone skill，不是 Marketplace plugin；v1 不包含脚本、MCP 或遥测代码。

## 核心特性

- 中文主讲，保留 English terminology、公式、符号和 API 名称。
- 苏格拉底式优先：先检查你的理解，再逐级增强提示。
- 同时支持概念学习、代码审阅、测试设计、错误分析和 profiler 调试。
- 官方作业执行严格助教边界，独立实验与 capstone 可正常协作实现。
- 每个核心目标都要通过四项独立证据，不能用平均分或背景经历替代。
- 支持可选的项目级 `learning/` 状态，但没有明确授权绝不自动写入。
- 不读取简历、经历事实库、联系方式或其他 PII 来进行个性化教学。
- 纯指令设计，没有第三方运行依赖。

## 六种模式

| 模式 | 用途 | 典型产出 |
|---|---|---|
| `diagnose` | 自适应检查数学、PyTorch、系统与实验基础 | 暂定能力画像、缺口与下一步 |
| `learn` | 学习概念、公式、术语或某一讲内容 | 解释、推导引导、迁移问题 |
| `coach` | 实现辅导、代码审阅、错误分析、测试与性能调试 | 不变量、检查策略、实验方向 |
| `assess` | 验收一个核心学习目标 | 四项 gate 的状态与证据 |
| `reflect` | 结束本次学习或进行周复盘 | 结论、缺口、下一步、待确认更新 |
| `evidence` | 导出已经通过验收的能力证据 | 中性、可追溯的能力记录 |

六种模式是自然语言路由标签，不是六个新的 slash command。如果没有显式指定模式，Skill 可以根据请求自动选择，但隐式匹配不保证每次触发。

## 四证据掌握标准

一个核心目标只有在以下四项全部为 `passed` 时才算掌握：

| Gate | 要求 |
|---|---|
| Closed-book explanation | 不依赖笔记，给出因果连贯的解释 |
| Key derivation | 写出关键步骤、假设、维度和极限情况 |
| Implementation and validation | 提供实现以及测试、对拍、梯度、过拟合或 profiler 等验证 |
| Transfer / boundary reasoning | 处理改变假设、反例、失败模式或设计权衡 |

每项只使用三种状态：

- `not_assessed`：没有直接证据；
- `in_progress`：只有部分、间接或尚未核验的证据；
- `passed`：存在满足该 gate 的直接、可追溯证据。

进度落后时只会调整范围或节奏，不会降低掌握标准。

## 安装

根据 [OpenAI 官方 Skill 文档](https://learn.chatgpt.com/docs/build-skills)，Codex 可以从用户目录或仓库目录发现本地 Skill，也可以让 `$skill-installer` 从其他 GitHub 仓库下载。安装时必须保留完整目录，不能只复制 `SKILL.md`，否则 `references/` 和 `assets/` 会缺失。

### 方法一：使用 `$skill-installer`（推荐）

在 Codex 中发送：

```text
$skill-installer 请从 https://github.com/kianbqh/cs336-study-coach 安装这个 skill
```

安装后可通过 Skills UI 或 `/skills` 检查。如果没有立即出现，重启 Codex。

### 方法二：安装到个人目录

个人目录中的 Skill 可用于不同项目。Windows PowerShell：

```powershell
$skillRoot = Join-Path $HOME '.agents\skills'
New-Item -ItemType Directory -Force -Path $skillRoot
git clone https://github.com/kianbqh/cs336-study-coach `
  (Join-Path $skillRoot 'cs336-study-coach')
```

macOS 或 Linux：

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/kianbqh/cs336-study-coach \
  "$HOME/.agents/skills/cs336-study-coach"
```

### 方法三：只在一个项目中启用

把仓库克隆到目标项目根目录的 `.agents/skills/`：

```bash
git clone https://github.com/kianbqh/cs336-study-coach \
  .agents/skills/cs336-study-coach
```

这种方式适合团队共享同一套 CS336 学习规则，而不影响其他项目。

## 调用方式

在 Codex CLI 或 IDE extension 中，可以通过 `/skills` 选择，或直接使用 `$` 显式调用：

```text
$cs336-study-coach diagnose：评估我学习 CS336 Lecture 1 和 Assignment 1 所需的基础。
```

在 ChatGPT desktop 中，可通过 Skills UI 或 `@` 选择 `CS336 Study Coach`。当前配置允许隐式调用，但更可控的学习会话建议显式选择 Skill 和模式：Codex CLI/IDE 使用 `$cs336-study-coach`，ChatGPT desktop 使用 `@` 或 Skills UI。

## 快速开始

### 1. 首次诊断

```text
$cs336-study-coach diagnose：评估我学习 CS336 Lecture 1 和 Assignment 1 所需的基础。
先逐题诊断，不要创建或修改项目文件。
```

Skill 会一次提出一个有区分度的问题，不会一开始就给你一份冗长问卷。

### 2. 学习一个概念

```text
$cs336-study-coach learn：我正在学习 byte-level BPE。
请先检查我对训练流程的理解，再根据我的回答逐级提示。
```

### 3. 辅导独立实验

```text
$cs336-study-coach coach：这是一个独立的 toy lab，不是官方作业或其改写。
请和我一起实现一个 causal attention reference，并设计与 PyTorch 对拍的测试。
```

### 4. 辅导官方作业

```text
$cs336-study-coach coach：这是 CS336 官方作业。
下面是我写的代码、预期行为和测试输出。请指出应该检查的不变量与最小反例，不要给出实现答案。
```

### 5. 验收掌握程度

```text
$cs336-study-coach assess：考核我是否真正掌握 Transformer resource accounting。
请依次检查闭卷解释、关键推导、实现验证和迁移能力。
```

### 6. 复盘并导出证据

```text
$cs336-study-coach reflect：总结本次学习，列出四项 gate 状态和下一步。
只展示拟议的状态更新，不要写文件。
```

```text
$cs336-study-coach evidence：只导出当前项目中已经四项通过、且有证据引用的能力。
不要生成简历话术。
```

## 推荐学习流程

```text
确认课程版本与 commit
        ↓
diagnose：定位真实前置缺口
        ↓
learn：重建概念与关键推导
        ↓
coach：实现、测试、调试或 profiling
        ↓
assess：逐项完成四证据验收
        ↓
reflect：确认结论、缺口与下一步
        ↓
用户明确授权后更新 learning/
        ↓
evidence：导出已通过的能力证据
```

建议一次只处理一个核心目标。对独立实验，先在 CPU 上完成 correctness 和 tiny deterministic tests，再根据任务需要进入 GPU benchmark 或分布式实验。

## 可选的项目学习状态

Skill 可以读取项目内的 `learning/` 目录，但不会自动创建它：

```text
learning/
├── profile.md
├── progress.md
├── evidence.md
└── sessions/
    └── YYYY-MM-DD-HHmm-topic.md
```

各文件用途：

- `profile.md`：脱敏的目标、优势、缺口和教学偏好；
- `progress.md`：课程版本锁、当前目标、四项 gate、误区与下一步；
- `sessions/`：经授权保存的简短学习记录；
- `evidence.md`：已经通过四项验收的中性能力证据。

初始化时可以这样请求：

```text
$cs336-study-coach diagnose：先完成诊断，然后依据 assets 中的模板展示 learning/ 初始化草案。
等我明确确认后再创建文件。
```

任何普通的辅导、考核或复盘请求，都不自动构成写入授权。`learning/` 可能包含个人学习状态；如果不准备公开，请把它加入学习项目的 `.gitignore`。

## 官方作业与学术诚信边界

对于 CS336 官方 assignment、handout、starter、tests、TODO，以及它们的复制版或实质等价改写，Skill 采用保守的严格助教模式。这是本项目的行为政策，不冒充 Stanford 官方 Honor Code。

可以做：

- 解释高层概念和必要前置知识；
- 指向锁定版本的讲义、课程材料、官方框架文档或原始论文；
- 审阅学习者自己写的代码，指出相关区域、不变量和边界条件；
- 解释学习者提供的错误信息或 profiler 输出；
- 建议 assertions、tiny inputs、reference comparison、gradient checks 和 profiling investigations；
- 通过问题让学习者自己完成关键推理和实现。

不会做：

- 编写 Python、伪代码、补丁或直接答案；
- 填写 TODO 或实现作业核心组件；
- 编辑、运行或重构官方作业及其实质复制版；
- 泄露题目要求学习者发现的决定性步骤；
- 查找、引用或引导到学生答案与第三方作业实现。

对于确认独立、且不构成作业绕行的 lab 或 capstone，可以在用户明确要求时共同设计、实现、测试和 profiling。分类依据是任务实质，而不是目录名或文件名。

## 课程版本与资料来源

项目中的 `learning/progress.md` 是课程 offering 和仓库 commit 的状态来源。没有项目锁时，Spring 2026 只作为临时默认值，不会被自动写成正式锁。学习 Spring 2025 等其他 offering 时，应先把对应版本与官方仓库 commit 写入锁定草案并确认。

资料优先级：

1. 本地锁定的 handout、lecture、starter metadata 与项目笔记；
2. [Stanford CS336 官方课程网站](https://cs336.stanford.edu/) 与 `stanford-cs336` 官方 GitHub 组织；
3. 官方框架或硬件文档；
4. 原始研究论文。

如果材料来自不同 offering 或 commit，Skill 会先报告冲突并停止实质辅导，不会静默混用。

## 隐私与状态隔离

- 本 Skill 管理的持久化项目状态只写入当前项目的可选 `learning/` 目录；
- 不跨项目继承另一位学习者的 profile、progress 或 evidence；
- 不把全局记忆当作项目学习状态；
- 不主动读取简历、经历事实库、联系方式、账号或精确位置；
- 只保存简短、脱敏、与学习目标直接相关的记录；
- 每次写入前先展示草案，并要求当前交互中的明确授权。

Skill 本身没有脚本或遥测代码，但这不代表宿主 Codex、模型服务或用户主动启用的网页检索必然离线；相关数据处理以宿主产品的政策和设置为准。

## 仓库结构

```text
cs336-study-coach/
├── .gitattributes
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── modes.md
│   ├── integrity-and-sources.md
│   └── state-contract.md
├── assets/
│   ├── learner-profile-template.md
│   ├── progress-template.md
│   ├── session-template.md
│   └── evidence-template.md
├── README.md
└── LICENSE
```

`SKILL.md` 是入口；`references/` 按需加载详细规则；`assets/` 只在用户授权初始化或更新学习状态时使用；`agents/openai.yaml` 提供显示名称、默认提示词和隐式调用策略。

## 已验证行为

v1 已进行结构校验、静态检查和隔离行为测试，覆盖：

- 拒绝直接填写官方 BPE TODO；
- 拒绝通过 `learn` 模式索取官方书面推导答案；
- 允许协作实现真正独立的 toy lab；
- 没有 learner profile 时正常诊断且不写文件；
- 发现 2025/2026 或 commit 冲突时停止并报告；
- 四项证据未齐时不标记掌握；
- `reflect` 只输出待确认更新；
- `evidence` 只导出有引用的已通过能力；
- 不跨项目泄漏或沿用另一位学习者的状态。

## 更新

个人目录安装的更新命令：

```bash
git -C "$HOME/.agents/skills/cs336-study-coach" pull --ff-only
```

项目级安装的更新命令（在项目根目录执行）：

```bash
git -C ".agents/skills/cs336-study-coach" pull --ff-only
```

如果修改后没有立即显示，请重启 Codex。Codex 的 Skill 发现位置和调用方式以 [OpenAI 官方文档](https://learn.chatgpt.com/docs/build-skills) 为准。若需要面向更广泛用户的一键分发，可在后续版本把该 standalone skill 封装为 plugin。

## License

[MIT](LICENSE)
