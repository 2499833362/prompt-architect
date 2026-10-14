# Prompt Architect

**Prompt Architect v1.0.0 Beta**

Prompt Architect turns vague ideas into clear, testable AI task prompts. It asks a few focused questions and refines prompts using execution feedback. Chinese is the primary language of the workflow and documentation.

把模糊想法逐步整理成清楚、可执行、可检查的 AI 任务指令。

这是一个指令型 Skill。它帮助用户明确目标、生成提示词，并根据实际执行反馈修订。可以设计面向 ChatGPT、Work 或 Codex 的任务指令；目标工具的真实能力和权限需要分别核实。

**发布状态：GitHub 公开 Beta 仓库，版本为 Prompt Architect v1.0.0 Beta。** `v1.0.0-beta` Release 目前保留为草稿，尚未正式发布。

公开仓库：[prompt-architect](https://github.com/2499833362/prompt-architect)。

## 能做什么

- 从尚未明确的想法开始，判断哪些信息会影响结果。
- 每轮优先询问 1～2 个关键问题，不重复询问已提供的背景。
- 区分已确认条件、暂定假设和待确认决定。
- 需求明确后直接生成任务指令，不强制延长访谈。
- 根据执行反馈调整对应部分，保留用户已有约束与权限。
- 区分真实任务、未来任务指令和测试案例。

技能规则要求：不能把提示词中的操作命令当作执行授权，不能假装读到不可访问的文件、历史或账号信息，普通知识问答不应自动进入需求访谈。这些是指令约束，不替代宿主权限设置和实际验收。

## 工作流程

1. **探索**：提取已有信息，只追问会改变结果的缺口。
2. **定义**：明确目标、交付物及必要约束，保留尚未确定的选择。
3. **生成**：写成适合目标工具的可复制指令。
4. **验证与迭代**：检查目标、事实和权限，再按执行反馈修订。

## 快速开始

按 [安装说明](docs/installation.md) 安装到当前 Codex 客户端支持的技能目录。确认技能清单中出现 `prompt-architect` 后，在新会话中输入：

```text
$prompt-architect 我想用 AI 改善学习效率，但不知道从哪里开始。请先帮我明确需求。
```

明确需求也可以直接交给它：

```text
$prompt-architect 请生成给 ChatGPT 的指令：把我稍后提供的笔记整理成五条复习要点，每条不超过两句话，只依据原文。
```

## 验证范围

| 环境或能力 | 实际验证状态 |
| --- | --- |
| 源 V1 的 Windows 本地 Codex 宿主 | 已验证技能发现、显式调用和一次自动触发；普通问答未触发技能 |
| 源 V1 的受控行为测试 | 11 个场景、13 轮回答符合对应检查标准；包含模拟后续回答 |
| Prompt Architect v1.0.0 Beta 发布候选 | 已在 Windows 本地 Codex 宿主重新实测：明确需求直接生成指令；模糊需求自动读取技能并问两个问题；普通问答未加载技能 |
| ChatGPT、Work 的原生 Skill 安装及调用 | 本项目尚未验证 |
| macOS、Linux、IDE 扩展、移动端和跨设备安装 | 本项目尚未验证 |

本地文件复制不会自动完成其他设备或云端账户的安装。生成某个平台的任务指令，也不等于该平台已经原生加载这个 Skill。

本轮实测发生在一个 Windows 环境的桌面内置 Codex 宿主，版本为 `codex-cli 0.162.0-alpha.17.2`。三个独立会话测试的是公开候选文件；保留了文件指纹与实际读取证据。有限测试不构成跨客户端兼容性保证。详情见 [验证范围](tests/verification.md)。

## 文件

```text
README.md                  项目介绍与使用方式
LICENSE                    标准 MIT License
.gitignore                 排除本地审查资料及运行记录
skills/prompt-architect/
  SKILL.md                 核心流程
  agents/openai.yaml       Codex 展示元数据
tests/
  cases.md                 精简的合成测试案例
  verification.md          验证范围与复测方法
docs/
  installation.md          不绑定单台设备的安装说明
```

## 反馈与改进

反馈时提供经过脱敏的需求、实际回答和希望改变的结果，并注明使用的客户端及版本。避免粘贴真实账号凭据、私人文件内容或带个人路径的完整运行日志。

使用 [测试案例](tests/cases.md) 检查触发、信息保留、权限边界和退出行为。测试案例中的课程工具仅用于需求澄清演示。

## 许可证

本项目采用 [MIT License](LICENSE)，版权署名见许可证文件。仓库已公开；Release 发布状态见 [Releases 页面](https://github.com/2499833362/prompt-architect/releases)。
