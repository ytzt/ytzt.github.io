---
layout: post
title: "轨迹规划系统理解：从状态空间到可执行轨迹"
subtitle: "一个包含公式与图片的 Markdown 博客示例"
date: 2026-09-20
author: "YTZT"
header-img: "img/post-bg-rwd.jpg"
header-mask: 0.25
catalog: true
mathjax: true
tags:
  - 机器人
  - 轨迹规划
---

这是一篇用于验证博客发布流程的示例文章。它演示了如何在 Markdown 中写公式、引用仓库内图片，以及通过首页打开完整文章。

## 1. 问题定义

给定机器人当前状态 $x_0$、目标状态 $x_g$ 和环境约束，轨迹规划器需要生成一条满足动力学约束的状态轨迹：

$$
\mathbf{x}(t) = [\mathbf{q}(t),\dot{\mathbf{q}}(t)], \qquad t \in [0, T]
$$

常见的优化目标可以写成：

$$
\min_{\mathbf{x}(t),\mathbf{u}(t),T}
\int_0^T \left(\|\mathbf{u}(t)\|_R^2 + \|\mathbf{x}(t)-\mathbf{x}_g\|_Q^2\right)\,dt
$$

同时满足系统动力学和边界条件：

$$
\dot{\mathbf{x}} = f(\mathbf{x}, \mathbf{u}),\quad
\mathbf{x}(0)=\mathbf{x}_0,\quad
\mathbf{x}(T)=\mathbf{x}_g.
$$

## 2. 一个最小系统结构

```text
传感器/定位 ──> 状态估计 ──> 轨迹规划 ──> 轨迹跟踪 ──> 执行器
                    ↑             │
                    └── 环境地图 ─┘
```

下面的示意图放在仓库中，并用相对博客根目录的 URL 引用：

![轨迹规划系统数据流](/img/in-post/trajectory-planning/pipeline.svg)

图中的规划模块通常先生成几何路径，再进行时间参数化，最后交给控制器执行。每一步都可以独立替换，便于逐步演进自己的系统。

## 3. 如何验证文章

提交后访问 `https://<用户名>.github.io/<仓库名>/2026/09/20/trajectory-planning-system/`（用户主页仓库通常没有 `<仓库名>`），应当看到：

- 首页列出这篇文章，点击标题进入详情页；
- 行内公式和独立公式由 MathJax 渲染；
- SVG 图片正常显示；
- 代码块带有 Rouge 语法高亮和行号。

这篇文章可以直接复制为新文章模板，再替换 front matter、正文和图片路径。
