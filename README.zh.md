# dsh-space-cognition-suite

[English](README.md) | 中文

J-Space 认知套件，以 DeepSeek Harness（DSH）插件形式交付。

一个推理时的认知控制层：它为 agent 提供一个可自主支配的内部工作区，以及使用它的一套纪律——一条前提、一道任务闸门（fast/full/loop）、基于模块的按需加载、基于接缝的审计，以及跨接缝与回合携带状态的持久账本。

## 它做什么

- **激活** —— 向每个 agent 会话注入一段紧凑的 J-Space 激活头（每会话一次）：前提、闸门、模块索引与不变量。无需手动加载技能。
- **账本工具** —— 注册一个 `jspace` 工具，封装内置的 `jspace.py` 控制器。模型在循环回 合中使用它在任务工作区内维护带标签的状态（`.jspace/WORKSPACE.md`）：`seam`、`resume`、`note`（`--goal/--next/--core/--core-slot/--check/--by/--open/--settled-by/--close`）、`ship`。
- **发现** —— 把内置的 `j-space/` 技能树同步到 agent 技能目录（默认 `~/.agents/skills/j-space`），让具备技能感知能力的主机零配置发现 `j-space`。同步是内容感知且幂等的。

## 安装

需要带 Node 18+ 与 Python 3 的 DSH desktop/web profile。

在 profile 的 `cordis.patch.yml` 中加入：

```yaml
- insert:
    - id: dsh-space-cognition-suite
      name: 'dsh-space-cognition-suite'
      config:
        python: 'C:\Python314\python.exe'  # 你的 python3 路径
```

然后把包安装进 profile 的 `node_modules` 并重启 harness。

## 目录结构

```
lib/index.js          插件入口（激活 + 工具 + 同步）
j-space/SKILL.md      J-Space 技能入口
j-space/modules/      由闸门按需加载的模块
j-space/references/   证据库、技巧、实战范例
j-space/scripts/      jspace.py 账本控制器 + verify_suite.py
cordis.patch.yml      加载器补丁清单
```

## 许可证

Apache-2.0