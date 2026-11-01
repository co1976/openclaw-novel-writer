# Novel Writer · 网文创作引擎

一个面向**长篇网络小说创作**的 Agent 技能（OpenClaw / Claude Code Skill），把「大纲 → 节拍卡 → 正文 → 验收 → 设定回写」跑成一条闭环流水线，专治长篇写作最常见的三个死穴：**前后矛盾、节奏塌陷、AI 味**。

> A production-oriented skill for writing long-form web novels with an LLM agent. Focuses on continuity, pacing and removing machine-sounding prose.

## 它能解决什么

| 痛点 | 对应机制 |
|---|---|
| 写到 50 章人物崩、设定打架 | 人物 Codex + 角色状态机（`character_states.json`）逐章增量回写 |
| 中段乏力、追读掉 | 写前三问 + 六节点节拍卡，写不出爽点不许动笔 |
| 伏笔埋了收不回来 | 伏笔/债务双台账，三态操作（埋 / 推 / 掀） |
| 一眼 AI 味 | 写后验收「AI 痕迹检测」硬闸门，人味评分 < 7 退回精修 |
| 批量写就崩 | 批量模式统一情绪曲线、爽点分布、钩子链 |

## 核心主张

1. **一致性高于一切** — 长篇最大的敌人是前后矛盾
2. **节奏为王** — 短句、口语化、快节奏、每 500 字一个起伏
3. **大纲是权威** — 正文向大纲看齐，有价值的正文设定反向补进大纲
4. **追踪表是记忆** — 结构化追踪，不靠印象
5. **写前严审 > 写后修补**
6. **验收是硬闸门** — 不通过就是不过，不降级放行
7. **四种模式不混用** — 写新章时不讨论，讨论时不产出

## 四种运行模式

| 模式 | 触发 | 做什么 |
|---|---|---|
| 写新章 | 作者下指令 / 自行推进 | 写前 → 节拍卡 → 正文 → 验收 → Codex 更新 |
| 局部修改 | 指定段落需求 | 只改目标范围，改完通知 |
| 开放讨论 | 直接对话 | 剧情/设定碰撞，不产出正文 |
| 自动巡检 | 每 5/10 章或按需 | 只读分析，出漂移与节奏报告 |

## 安装

**OpenClaw**

```bash
git clone https://github.com/<your-name>/novel-writer-skills.git \
  ~/.openclaw/workspace/skills/novel-writer
```

**Claude Code / 其他宿主**

把仓库内容放进宿主的 skills 目录，或将 `SKILL.md` 作为项目级 skill 引入。

依赖：Python 3.8+（检测脚本）；无第三方包强制依赖。

## 目录结构

```
.
├── SKILL.md                 # 技能主入口：原则、流程、模式、验收
├── VERSION
├── references/              # 按需加载的方法论文档
│   ├── 写前检查卡.md
│   ├── 写后验收卡.md
│   ├── 伏笔债务台账.md
│   ├── 世界状态机.md
│   ├── 批量写作.md
│   ├── 情绪曲线模板.md
│   ├── 平台合规细则.md
│   ├── 卡文破局.md
│   ├── 大纲设计.md
│   ├── 角色弧线.md
│   ├── 钩子设计.md
│   ├── 对话质量.md
│   ├── 伏笔管理.md
│   ├── 写作技巧.md
│   ├── 深度审读指南.md
│   ├── 分发台账规范.md
│   └── usage_examples.md
└── scripts/                 # 一致性 / 节奏 / 钩子 / 伏笔检测
```

## 检测脚本

```bash
python scripts/cli.py all        --novel-dir chapters/   # 一键全检
python scripts/cli.py rhythm     --novel-dir chapters/   # 节奏分析
python scripts/cli.py drift      --outline 大纲.md --chapters chapters/
python scripts/cli.py foreshadow --novel-dir chapters/
python scripts/cli.py hook       --novel-dir chapters/
python scripts/cli.py report     --novel-dir chapters/ --title "书名"
```

## 配套生态（可选，非本仓库）

以下为社区同类技能，按需单独安装，本仓库不包含其代码：

- 榜单扫描 / 拆文 / 去 AI 味 / 封面 / 审查：[oh-story-claudecode](https://github.com/worldwonderer/oh-story-claudecode)

## 许可

MIT，见 [LICENSE](./LICENSE)。
