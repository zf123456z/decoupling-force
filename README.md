# 解耦力框架（Decoupling Force Framework）

> **面对任何复杂问题，先问"天然裂缝在哪"，沿裂缝切割，再设计桥接。**
>
> **Before solving any complex problem, first ask "where is the natural seam."**

---

## 🧭 这是什么 / What Is This

解耦力框架是一个**元认知工具**——不是教你"怎么做"，而是教你**先想清楚"怎么拆"**。

Decoupling Force is a metacognitive tool — not about "how to solve", but about **"how to decompose before solving."**

它的核心洞察来自一个反直觉的事实：
> **大多数人在资源不够时，第一反应是"要更多资源"。但真正的高手在资源不够时，会重新思考"这个问题我有没有切对"。**

The core insight: most people, when short on resources, ask for more resources. The best ask a different question: "Did I cut this problem correctly?"

---

## 📦 安装 / Installation

### WorkBuddy（推荐）

```bash
# 从 SkillHub 安装（国内）
skillhub install decoupling-force

# 或从 GitHub 仓库导入
```

### Claude Code / Cursor / 其他 26 个 AI Agent

兼容 [Agent Skills 开放标准](https://skillkit.io/zh/skills/claude-code/task-planner)，支持：
`~/.agents/skills/` → 自动覆盖 26 个平台

```bash
mkdir -p ~/.agents/skills/decoupling-force
# 将 SKILL.md 复制到该目录
```

### 手动安装

将本项目克隆或下载到对应 Agent 的 skills 目录。

---

## 🚀 快速开始 / Quick Start

### 场景 1：代码重构

```
用户：这个支付模块有 2000 行，改一个支付方式要改 5 个文件。
解耦力：这条裂缝在哪？
→ 支付方式（微信/支付宝/银联）属于"接入层"
→ 支付核心逻辑（下单/退款/对账）属于"业务层"
→ 切割：每种支付方式一个文件，共享同一接口契约
→ 桥接：一个 PaymentGateway 接口，N 个实现
```

### 场景 2：架构设计

```
用户：我要做一个 AI 助手，该用什么架构？
解耦力：裂缝在哪？
→ "听懂问题" vs "找到答案" vs "说出答案" 是不同的维度
→ 语义理解层（NLU）+ 知识检索层（KG/RAG）+ 表达层（NLG）
→ 每层独立演进，通过事件总线桥接
```

### 场景 3：创业策略

```
用户：我们 3 个人，怎么跟大公司竞争？
解耦力：裂缝在哪？
→ 大公司的问题是他们"什么都要做"
→ 他们的效率缝隙在哪？（"覆盖所有" vs "某个子问题做到极致"）
→ HRT 案例：11人团队不做交易所，只做做市商，干翻币安 3000人
```

---

## ⚙️ 工作流 / Workflow

```
[问题] → Step 1: 找裂缝 → Step 2: 切割 → Step 3: 桥接 → [解决方案]
           │                  │              │
           ├─ 维度差异        ├─ 内聚性     ├─ 信息不减
           ├─ 时间尺度差异    ├─ 独立性     ├─ 格式独立
           ├─ 资源差异        ├─ 可复用     ├─ 可替换
           ├─ 驱动差异        └─ 可测试     └─
           └─ 职责差异
```

---

## 📊 成熟度评估 / Maturity Assessment

使用这个表格评估你的系统当前处于哪个级别：

| 级别 | 名称 | 特征 | 判断标准 |
|:---:|:-----|:-----|:---------|
| L0 | 混沌 | 没有分解，都在一个文件/模块 | 改一行可能坏一片 |
| L1 | 功能切割 | 按功能分了文件，但耦合还在 | 类似功能改了要改多个地方 |
| L2 | 维度切割 | 按问题维度切分 | 每个维度可独立修改 |
| L3 | 桥接优化 | 有精巧的接口设计 | 替换实现不影响其他模块 |
| L4 | 自适应 | 系统自动调整切割 | 不太需要人工干预 |

**目标：系统达到 L2 或以上。**

---

## 📁 项目结构 / Structure

```
decoupling-force/
├── SKILL.md              # 主技能文件（兼容 26 个 Agent）
├── README.md             # 本文件
├── LICENSE               # Apache-2.0
├── examples/
│   ├── code-refactor.md  # 代码重构示例
│   ├── architecture.md   # 架构设计示例
│   └── strategy.md       # 战略示例
└── references/
    └── theory.md         # 完整理论文档（中文）
```

---

## 🧠 原理 / Theory

解耦力框架从 VoxCPM2（OpenBMB 开源的 TTS 系统）的架构创新中提炼升华：

- **具体观察**：VoxCPM2 用 2B 参数+8GB显存+30语言部署，不是堆资源而是重新切分问题
- **架构模式**：复杂问题不硬扛，沿天然裂缝分解
- **通用原理**：约束是创新的编译器（Constraint-Driven Design）
- **元原则**：解耦力是系统智能的终极度量

四层抽象，从具体到普适。

---

## 🔗 关联资源 / Related

- [公众号文章系列](https://mp.weixin.qq.com/) — 搜索"解耦力系列"
- 作者：**张俊峰（Vita X）**
- 构建时间：2026-06-16

---

## 📄 许可证 / License

Apache License 2.0 — 可商用、可修改、可再分发。
