---
title: "我如何理解 Sub-Agent：Sub-Agents as high-level Tools"
published: 2026-04-15
description: "Sub-Agent 是具有独立上下文、专门提示词、明确输入输出契约的 LM 执行单元。从主 Agent 视角，它可以被视为一种高阶工具。本文探讨 Sub-Agent 的定义、边界与工程实践意义。"
image: ""
tags: ["Agent 架构","Sub-Agent","工作流","大模型"]
category: "AI Agent 工程实践"
draft: true
lang: ""
---

<!-- 写作指南（完成后删除此区块）

## 结构建议

1. Sub-Agent 是什么？——一个工具视角的定义
2. 为什么是"高阶工具"而非"子模型"？——与普通工具的本质区别
3. Sub-Agent 的三个契约：独立上下文、专门提示词、明确 I/O
4. 从主 Agent 视角看委托：何时拆出 Sub-Agent？
5. 与 Harness 的关系（互引）

## 避免的陷阱

- ❌ 不要把 Sub-Agent 和函数调用/工具调用等同——关键是"独立上下文"这个属性
- ❌ 不要陷入实现细节（怎么创建 Sub-Agent）——聚焦概念边界
- ❌ 不要过度类比面向对象的继承——Sub-Agent 不是继承关系，是委托关系

## 写作风格

- ✅ 用"高阶函数"类比：普通工具是值，Sub-Agent 是函数——它接收输入，在独立作用域中执行，返回输出
- ✅ 用你参与 Claude Code / Codex 的实际体验作为直觉来源
- ✅ 诚实面对边界模糊的情况："什么样的工具调用算 Sub-Agent？这里确实有灰色地带"
- ✅ 与 Harness 文章互引，构成 Agent 工程的概念三角

-->

## 迭代记录
| 日期       | 版本 | 更新说明 |
| ---------- | ---- | -------- |
| 2026-04-15 | v0.1 | 创建文章骨架 |