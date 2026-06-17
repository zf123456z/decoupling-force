---
name: decoupling-force
description: >
  [中文] 解耦力框架——面对任何复杂问题（代码重构、架构设计、流程优化、战略规划），先问"天然裂缝在哪"，沿裂缝切割，再设计桥接。
  [English] Decoupling Force Framework — before solving any complex problem (refactoring, architecture, process, strategy), first ask "where is the natural seam", cut along it, then bridge.
  触发词 / Trigger: 解耦 / decouple / 分解 / seam carving / 重构 / refactor / 架构设计 / architecture / 复杂度管理 / complexity / 系统设计 / system design / separation of concerns
---

# 解耦力框架（Decoupling Force Framework）

Fork of [zhangjunfeng/decoupling-force](https://github.com/zhangjunfeng/decoupling-force)

## Overview

面对复杂问题时，第一反应不是"怎么解决"，而是：**"这个问题的天然裂缝在哪？"**

Decoupling Force is a metacognitive tool — not a specific methodology, but a way of thinking that applies before any decision.

Core belief: **Constraints are not limitations; they are compilers for innovation.**

## When to Use

Use when the user says ANY of:

- "This code is a mess / 代码太乱了要重构"
- "How should I design the architecture / 架构设计该怎么做"
- "The system is too complex / 系统复杂度太高"
- "I need to build a new feature / 要做一个新功能"
- "How do I optimize this / 怎么优化现有系统"
- "What's our strategy / 创业/产品策略怎么定"

Do NOT use for simple Q&A or factual lookups.

## The Three-Step Method

### Step 1: Detect — Find the Seam

Ask: **Where is the natural seam?**

Five criteria for detecting seams:

| Criterion | Question | Signal |
|:----------|:---------|:-------|
| Dimensional gap | Do different aspects belong to different dimensions? | Semantics vs acoustics; function vs data |
| Time-scale gap | Do parts change at different rates? | Long-term stable vs temporary fluctuation |
| Resource gap | Do parts consume different types of resources? | CPU-bound vs I/O-bound vs memory-bound |
| Driver gap | Are parts driven by different forces? | User behavior vs system state vs external events |
| Responsibility gap | Do parts serve different "whats"? | "What" vs "How" vs "Why" |

### Step 2: Cut — Slice Along the Seam

Each resulting sub-problem MUST satisfy:

- **Cohesion**: Internally highly related
- **Isolation**: Externally low-coupled (clear interface, independent internals)
- **Reusability**: Solvable with an existing best-fit approach
- **Testability**: Independently verifiable

> One line of code / one module should serve ONE "what." If it serves two or more, it sits on a seam — cut it.

### Step 3: Bridge — Design the Interface

How sub-problems reconnect matters more than how they were cut.

Three bridge principles:

- **No information loss**: The interface must pass at least as much information as the upstream produces
- **Format independence**: Upstream and downstream use their own internal formats; the bridge adapts
- **Replaceability**: Swapping any sub-problem's implementation does not affect others

## Four Domains of Projection

### 1. Code Level
- **Problem**: Coupled modules; change in one breaks another
- **Decouple**: Trace data flow → find data-shape change points → cut along them → each module transforms once

### 2. Architecture Level
- **Problem**: One engine does everything; all cognitive tasks share the same mechanism
- **Decouple**: Skeleton (stable, fast retrieval) + Cortex (temporary, on-demand reasoning) + Bridge (injection)

### 3. Process Level
- **Problem**: See requirement → write code directly (vertical slicing); high rework cost
- **Decouple**: Requirement enters → ask "where is the seam" → design sub-problem system + interface contracts → build bridges first, fill content later

### 4. Strategy Level
- **Problem**: Competing head-on with larger players; resource asymmetry
- **Decouple**: Find the efficiency gaps where covering-all creates seams → go deep into that gap → 11 people beat 3000

## Maturity Assessment

| Level | Name | Characteristics |
|:-----:|:-----|:----------------|
| L0 | Chaos | No visible decomposition; everything mixed |
| L1 | Functional | Cut by function; coupling remains |
| L2 | Dimensional | Cut by dimension; each evolves independently |
| L3 | Bridged | Cut + elegant bridge; sub-problems swappable |
| L4 | Adaptive | System auto-adjusts cutting strategy |

Target: Systems at L2 or above.

## Real-World Example

**VoxCPM2** (OpenBMB, 2026): A text-to-speech system with 2B parameters and 30 languages running on 8GB VRAM.

Traditional approach: "Text-to-audio is complex → need bigger model + more data."
Decoupling approach: "Text-to-audio = semantic planning (autoregressive LM for stability) + acoustic rendering (diffusion for richness) + quality enhancement."

By cutting the problem differently, VoxCPM2 achieved near-closed-source quality with 1/10th the compute. The FSQ quantization trick (stabilizing semantic skeleton while letting acoustic details remain flexible) is a textbook example of Step 2 + Step 3 done right.

## References

- Full theory document: `references/Vita X 解耦力框架.md` (Chinese)
- Theory origin: Derived from VoxCPM2 deep-dive, June 2026
- Author: 张俊峰（Vita X）

## License

Apache License 2.0
