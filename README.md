# project-memory

**一次启用，持续维护。对话可以重新开始，项目记忆继续保留。**

Project memory for AI agents: keep project state, decisions, and next steps in Markdown files across sessions. Enable it once per project, then continue working without repeatedly invoking the skill.

## 为什么需要它

一个项目还没做完，对话已经太长了。需求、排障和反复修改交织在一起，agent 可能忽略早期约定、重复做过的调查，或把旧方案当成当前决定。直接新开对话，又缺少之前的上下文，需要重新解释项目背景、当前进度和下一步。

project-memory 将继续工作所需的信息整理成项目文件：目标、当前状态、重要决定及理由、验证结果、未完成事项和恢复入口。新的对话先读概览，再按需读取相关专题，从已有进度接着推进。

例如，网站的登录功能已完成、部署故障已解决，支付接口还没做完。项目记忆保存这些状态后，新对话可以直接围绕支付接口继续工作，减少重新交代和重复排查。

## 安装

通过 [skills CLI](https://github.com/vercel-labs/skills) 安装，需要 Node.js 及对应 CLI 要求的运行环境：

```sh
npx skills add plutoxoxoK/project-memory --skill project-memory
```

按提示选择目标 agent。仅安装到当前项目的 Codex：

```sh
npx skills add plutoxoxoK/project-memory --skill project-memory -a codex
```

也可以下载 [Releases](https://github.com/plutoxoxoK/project-memory/releases) 中的技能 ZIP，将其中的 `project-memory` 文件夹放入所用 agent 支持的技能目录；保留文件夹里的 `LICENSE`。具体目录与指引加载方式以客户端为准。

## 第一次启用

在目标项目中对 agent 说：

> 使用 project-memory 为这个项目启用项目记忆，后续持续维护。

支持显式技能调用的客户端也可使用 `$project-memory` 或其技能选择器。

agent 会确认项目和记忆位置，合并已有资料，建立核心记忆，并在项目的 `AGENTS.md` 中留下长期维护约定和读取入口。安装技能与为某个项目启用记忆是两步；安装不会替所有项目自动建档。

**启用后，日常工作和同一项目的新对话都无需反复 @ 技能。** 直接说“继续处理未完成的支付接口”即可。agent 按项目约定读取相关记忆，在重要进展后更新记录。换对话前也可以说“整理一下当前进度和下一步”，作为可选的交接提醒。

持续生效依赖客户端加载该项目的指引、能访问记忆文件，并遵循其中的维护约定。请在对应项目中开启新对话；不同客户端可能需要将入口接入其支持的项目规则。

## 怎么组织记忆

核心文件放在选定的项目记忆根目录：

| 文件 | 保存什么 |
| --- | --- |
| `AGENTS.md` | 长期协作约定、已启用状态、记忆入口与维护要求 |
| `PLAN.md` | 整体目标、主线计划、跨专题待办和完成标准 |
| `PROJECT.md` | 项目背景、当前状态、重要决策、必要历史和专题概览 |

- **连续推进的主线**：围绕同一交付目标，状态和决策直接积累在核心文件中。
- **可独立维护的专题**：例如一台 VPS 上的网站、备份和组网服务，各自保存详细记录，总览只保留摘要、入口和共同影响。
- **混合项目**：主线与专题可以并存。沿用已有合理目录，避免每次操作都新建一套记忆。

完整信息只维护一处，关联内容通过链接引用。接手工作先读概览和计划，再按需加载相关专题。

## 它会记录什么

记录会影响后续工作的状态、约束、决定及理由、验证结果、阻塞、下一步和恢复线索。区分当前状态与历史，也区分实际验证、用户反馈和待确认事项。

在重要要求变化、关键工作完成、出现实质阻塞或交接时更新；普通对话和没有长期影响的小操作不必记流水。已有记录可以逐步整理，修正过时状态、合并重复内容，并整合旧版 `STATE.md`。

## 示例

这里的项目和状态都是虚构示例，可按自己的项目调整：

- [连续开发一个小工具](examples/sequential/PROJECT.md)：一个目标、一条主线。
- [维护多个独立专题](examples/parallel/PROJECT.md)：总览加专题记忆。

示例中的 `AGENTS.md` 展示了“一次启用后如何让新对话继续维护”的项目约定，无需每次重新调用技能。已有项目应合并相关内容，保留自己的有效指引。

## 停用和卸载

对 agent 说“停用这个项目的 project-memory，保留现有记录”，让它更新项目指引中的启用约定。也可以自行移除对应的记忆维护段落；保留 `AGENTS.md` 中其他协作要求。

需要卸载技能时，使用所用客户端的管理功能，或运行：

```sh
npx skills remove project-memory
```

仅卸载技能不会自动清除各项目里已经写入的维护约定。历史记忆可以保留；删除记录需要另外明确决定。

## 使用边界

- 本技能是 Markdown 工作流指引，记忆保存在你可管理的项目文件中。
- 尚未保存到文件的旧聊天内容，需要在原对话整理，或提供必要线索。
- 它帮助 agent 找到和维护上下文；执行效果取决于模型、客户端的规则加载及实际维护。历史记录仍需核实。
- 记忆不扩大操作授权。只记录凭据位置或引用，不写入密码、token、私钥等秘密。
- 可以用于没有代码仓库的长期项目；普通临时任务不会因安装技能而自动建档。

## 作者与许可证

Maintained by [plutoxoxo](https://github.com/plutoxoxoK).

Copyright (c) 2026 plutoxoxo. Licensed under [MIT](LICENSE).
