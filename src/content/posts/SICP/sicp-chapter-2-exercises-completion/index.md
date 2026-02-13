---
title: "SICP 第 2 章练习完成情况记录"
published: 2026-02-10
description: ""
image: ""
tags: ["SICP","数据结构","数据抽象","学习记录"]
category: "SICP"
draft: true
lang: ""
---

## 2.1 数据抽象导引

## 2.2 层次化数据和闭包性质
### 2.2.1 序列的表示

#### 练习 2.17
定义一个过程 `last-pair`，它返回仅包含给定（非空）列表的最后一个元素的列表。

解答：
```scheme
(define (last-pair list1)
  (if (null? (cdr list1))
      list1
      (last-pair (cdr list1))))

(last-pair (list 23 72 149 34))
; (34)
```

#### 练习 2.18
定义一个过程 `reverse`，它接受一个列表作为参数并返回包含相同元素但顺序相反的列表。

解答：
```scheme
(define (reverse-append items)
  (if (null? items)
      ()
      (append (reverse-append (cdr items)) 
              (list (car items)))))
(define (reverse-iter list1)
  (define (iter remaining result)
    (if (null? remaining)
        result
        (iter (cdr remaining) 
              (cons (car remaining) result))))
  (iter list1 ()))
(define reverse reverse-iter)
(reverse (list 1 4 9 16 25))
; (25 16 9 4 1)
```

#### 练习 2.19
考虑第 1.2.2 节的零钱计数程序。如果我们能够轻松地更改程序使用的货币，以便计算兑换英镑的方法数，那就太好了。按照程序的编写方式，货币的知识部分分布在过程 `first-denomination` 中，部分分布在过程 `count-change` 中（已知有五种美国硬币）。如果能够显式地使用要找零的硬币列表，那就更好了。我们希望重写过程 `cc`，使其第二个参数是要使用的货币值列表，而不是指定要使用哪些硬币的整数。然后我们可以定义各种货币的列表：

```scheme
(define us-coins (list 50 25 10 5 1))
(define uk-coins (list 100 50 20 10 5 2 1 0.5))
```

然后我们可以这样调用 `cc`：

```scheme
(cc 100 us-coins)
; 292
```

为此需要稍微更改程序 `cc`。它仍将具有相同的形式，但它将以不同方式访问其第二个参数，如下所示：

```scheme
(define (cc amount coin-values)
  (cond ((= amount 0) 1)
        ((or (< amount 0) (no-more? coin-values)) 0)
        (else
         (+ (cc amount
                (except-first-denomination coin-values))
            (cc (- amount
                   (first-denomination coin-values))
                coin-values)))))
```

根据列表结构的基本操作定义过程 `first-denomination`、`except-first-denomination` 和 `no-more?`。列表 `coin-values` 的顺序是否会影响 `cc` 产生的答案？为什么或为什么不？

解答：暂无。

#### 练习 2.20
过程 `+`、`*` 和 `list` 接受任意数量的参数。定义此类过程的一种方法是使用带点尾记法（dotted-tail notation）的 `define`。在过程定义中，在最后一个参数名称之前有一个点的参数列表表示，当调用过程时，初始参数（如果有）将像正常一样具有初始参数的值，但最后一个参数的值将是任何剩余参数的列表。例如，给定定义：

```scheme
(define (f x y . z) <body>)
```

过程 `f` 可以用两个或更多参数调用。如果我们求值：

```scheme
(f 1 2 3 4 5 6)
```

那么在 `f` 的主体中，`x` 将是 1，`y` 将是 2，`z` 将是列表 `(3 4 5 6)`。给定定义：

```scheme
(define (g . w) <body>)
```

过程 `g` 可以用零个或更多参数调用。如果我们求值：

```scheme
(g 1 2 3 4 5 6)
```

那么在 `g` 的主体中，`w` 将是列表 `(1 2 3 4 5 6)`。

使用这种记法编写一个过程 `same-parity`，它接受一个或多个整数并返回与第一个参数具有相同奇偶性的所有参数的列表。

**解答：**
```scheme
(define (same-parity x . y)
  '(your Code Here))

(same-parity 1 2 3 4 5 6 7)
(same-parity 2 3 4 5 6 7)
```


## 发布记录
| 日期       | 版本  | 更新说明                    |
| ---------- | ----- | --------------------------- |
| 2026-02-11 | 0.1.1 | 添加 2.2.1 节中的练习 2.17-2.20 |
| 2026-02-10 | 0.1.0 | 骨架创建                    |
