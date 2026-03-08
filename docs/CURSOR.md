# 在 Cursor 中使用 Impeccable

本文档说明如何在 [Cursor](https://cursor.com) 中安装和使用 Impeccable 的设计技能与命令。

## 简介

Impeccable 为 Cursor 提供：

- **一套设计技能（Agent Skills）**：包含前端设计主技能及多个可单独调用的技能
- **可调用的斜杠命令**：如 `/audit`、`/polish`、`/normalize` 等，对应「用户可调用」的技能
- **设计参考与反模式**：排版、色彩、动效、响应式等参考文件，以及明确告知 AI「不要做什么」的指引

在 Cursor 中，这些内容都以 **Agent Skills** 形式安装在项目的 `.cursor/skills/` 目录下；其中标记为「用户可调用」的技能会作为聊天中的斜杠命令出现。

## 前置要求

1. **Cursor 版本**：需使用 **Nightly 渠道**  
   - 打开 **Settings → Beta**，切换到 Nightly 渠道并更新

2. **启用 Agent Skills**  
   - 打开 **Settings → Rules**（或 **Cursor Settings → General** 中与 Rules/Skills 相关的选项）  
   - 启用 **Agent Skills**，以便 Cursor 加载项目中的 `.cursor/skills/` 并暴露斜杠命令

若未满足以上两点，技能与命令可能无法出现或无法被调用。

- 官方说明：[Cursor Skills 文档](https://cursor.com/docs/context/skills)

## 安装方式

### 方式一：从网站下载（推荐）

1. 打开 [impeccable.style](https://impeccable.style)
2. 选择 **Cursor**，下载对应的 ZIP
3. 解压到你的**项目根目录**，确保解压后项目根目录下存在 `.cursor` 文件夹（即 ZIP 内应包含 `.cursor/` 或解压得到 `.cursor/`）

### 方式二：从本仓库复制

若你已克隆 Impeccable 仓库，可先构建再复制：

```bash
# 在 Impeccable 仓库根目录执行构建
bun run build

# 将 Cursor 输出复制到你的项目根目录
cp -r dist/cursor/.cursor /path/to/your-project/
```

将 `/path/to/your-project/` 替换为你的项目实际路径。复制后，你的项目根目录下应有 `.cursor/` 文件夹。

## 安装后的目录结构

安装完成后，项目中大致结构如下（仅列出与 Impeccable 相关部分）：

```
your-project/
└── .cursor/
    └── skills/
        ├── frontend-design/     # 主设计技能（含参考文件）
        │   ├── SKILL.md
        │   └── reference/
        │       ├── typography.md
        │       ├── color-and-contrast.md
        │       ├── spatial-design.md
        │       ├── motion-design.md
        │       ├── interaction-design.md
        │       ├── responsive-design.md
        │       └── ux-writing.md
        ├── audit/               # 可调用：/audit
        ├── critique/            # 可调用：/critique
        ├── normalize/           # 可调用：/normalize
        ├── polish/              # 可调用：/polish
        ├── distill/
        ├── clarify/
        ├── optimize/
        ├── harden/
        ├── animate/
        ├── colorize/
        ├── bolder/
        ├── quieter/
        ├── delight/
        ├── extract/
        ├── adapt/
        ├── onboard/
        └── teach-impeccable/
```

每个技能一个目录，内含 `SKILL.md`；`frontend-design` 还带有 `reference/` 下的参考文档。

## 使用方法

### 在聊天中使用斜杠命令

在 Cursor 的 AI 聊天中输入 `/`，即可看到已安装的 Impeccable 命令（即「用户可调用」技能），例如：

- `/audit` — 对界面做质量审计（可访问性、性能、主题、响应式等），生成问题与建议报告
- `/normalize` — 按设计系统做规范化
- `/polish` — 上线前最后打磨
- `/distill` — 做减法，保留核心
- `/clarify` — 改进不清楚的文案与说明
- `/optimize` — 性能优化
- `/harden` — 错误处理、国际化、边界情况
- `/animate` — 增加有意义的动效
- `/colorize` — 引入有策略的颜色
- `/bolder` — 让平淡设计更鲜明
- `/quieter` — 让过于强烈的设计更克制
- `/delight` — 增加小惊喜与愉悦感
- `/extract` — 抽成可复用组件
- `/adapt` — 适配不同设备/场景
- `/onboard` — 设计引导与空状态
- `/teach-impeccable` — 一次性收集项目设计上下文并写入配置

部分命令支持在输入时附带「范围」或「区域」，例如：

- `/audit header` — 只审计 header 相关部分
- `/polish checkout-form` — 只打磨结账表单

具体是否支持参数以及如何传参，以 Cursor 当前对 Agent Skills 的展示为准（Cursor 对 frontmatter/参数支持有限，可能以追加说明的方式传递）。

### 设计技能如何参与

- **frontend-design** 作为主设计技能，会被其他技能引用；AI 在做设计相关任务时会遵循其中的原则与参考文件。
- 调用 `/audit`、`/polish` 等命令时，对应技能的说明会指导 AI 先运用 frontend-design 的规范，再执行具体任务。

## 技能与命令一览

| 命令 / 技能 | 作用 |
|-------------|------|
| `/teach-impeccable` | 一次性设置：收集设计上下文并写入配置 |
| `/audit` | 质量审计：可访问性、性能、主题、响应式等，输出报告 |
| `/critique` | 设计评审：层次、清晰度、情感共鸣等 |
| `/normalize` | 与设计系统对齐 |
| `/polish` | 上线前收尾 |
| `/distill` | 精简到本质 |
| `/clarify` | 改进不清晰的文案与说明 |
| `/optimize` | 性能优化 |
| `/harden` | 错误处理、i18n、边界情况 |
| `/animate` | 增加有目的的动效 |
| `/colorize` | 引入有策略的颜色 |
| `/bolder` | 让设计更鲜明 |
| `/quieter` | 让设计更克制 |
| `/delight` | 增加愉悦与记忆点 |
| `/extract` | 抽成可复用组件 |
| `/adapt` | 适配不同设备/场景 |
| `/onboard` | 设计引导与空状态 |

**frontend-design** 技能（无斜杠命令）提供排版、色彩、空间、动效、交互、响应式、UX 文案等参考，以及 DO / DON'T 反模式，供其他命令和对话使用。

## 注意事项

1. **Cursor 的能力限制**  
   Impeccable 的源格式支持 YAML 前端与参数；为兼容 Cursor，构建时会做降级处理（例如去掉或简化 frontmatter、用追加说明代替参数）。若某命令在 Cursor 中无法传参，可在命令后直接输入要针对的区域或文件名。

2. **仅对当前项目生效**  
   安装到某项目的 `.cursor/` 只对该项目生效。若要在多个项目使用，需在每个项目根目录分别安装一次，或使用 Cursor 的全局/工作区配置（若支持）。

3. **更新**  
   从 [impeccable.style](https://impeccable.style) 重新下载 Cursor 包并覆盖 `.cursor/`，或从本仓库重新执行 `bun run build` 后再次 `cp -r dist/cursor/.cursor your-project/` 即可更新。

## 相关链接

- 官网与下载：[impeccable.style](https://impeccable.style)
- Cursor 技能说明：[cursor.com/docs/context/skills](https://cursor.com/docs/context/skills)
- Cursor 命令说明：[cursor.com/docs/agent/chat/commands](https://cursor.com/docs/agent/chat/commands)
- Impeccable 项目 README：[README.md](../README.md)
