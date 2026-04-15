---
title: "我如何理解 Harness：harness = Agent - LLM"
published: 2026-04-15
description: "Harness 是 Agent 中对模型行为施加约束并提供可达能力的全部非模型部分——即模型当前上下文及其可继续访问的工具、文件、流程与环境。本文提出 harness = Agent - LLM 的定义，重新审视 Agent 的工程边界。"
image: ""
tags: ["Agent 架构","Harness","协议设计","大模型"]
category: "AI Agent 工程实践"
draft: true
lang: ""
---

<!-- 写作指南（完成后删除此区块）

## 结构建议

1. 什么是 Harness？——一个减法定义
2. 为什么是 Agent - LLM？——从"补集"看 Harness
3. Harness 的三个层次：上下文、可达性、约束
4. Harness 的工程意义：为什么你需要关心它
5. 与 MCP/Skills 的关系（互引）

## 避免的陷阱

- ❌ 不要写成 Claude Code / Cursor 的功能介绍——你要定义的是概念，不是产品
- ❌ 不要把 Harness 和"工具"混为一谈——Harness 包含工具，但不等于工具集
- ❌ 不要一上来就列公式 `harness = Agent - LLM` 然后解释——先用直觉和例子建立理解，再形式化

## 写作风格

- ✅ 用减法思维切入："把 Agent 中的 LLM 拿掉，剩下什么？"
- ✅ 用类比：Harness 是舞台和道具，LLM 是演员——没有舞台的演员无法表演，没有演员的舞台没有意义
- ✅ 提问式推进："如果 Harness 不存在，LLM 还能做什么？"
- ✅ 与你之前的 Skills/MCP 文章互引，形成系列感

-->

## 迭代记录
| 日期       | 版本 | 更新说明 |
| ---------- | ---- | -------- |
| 2026-04-15 | v0.1 | 创建文章骨架 |