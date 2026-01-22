---
title: "C++ auto vs Rust let：类型推导行为差异"
published: 2026-01-23
description: "本文记录了 C++ auto 关键字与 Rust 类型推导机制的关键差异，重点讨论引用处理、类型推导规则以及 let 与 auto 的区别。通过代码示例对比，帮助理解两种语言在类型系统上的设计差异。"
image: ""
tags: ["C++","Rust","类型推导"]
category: "编程语言"
draft: true
lang: ""
---

## 引言
- 简述为什么要对比 C++ auto 和 Rust let
- 说明文章的目标（建立清晰的知识体系）

## C++ auto 的类型推导行为
### auto 默认推导什么？
- 值类型、引用、const 等的推导规则
### auto 默认去除引用的问题
- 代码示例：展示陷阱
- 如何使用 auto& 和 const auto&

## Rust let 的类型推导行为
### let 的基本推导
- 与 auto 的相似之处
### 引用声明与 ref 关键字
- & 和 ref 的使用场景
- 模式匹配中的类型推导

## 对比总结
- 设计哲学的差异
- 实战中的注意事项
