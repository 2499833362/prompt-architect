# 安装与跨设备使用

本仓库提供独立的本地 Codex Skill，核心文件是 `skills/prompt-architect/SKILL.md`。它不是已经发布或安装到 ChatGPT/Work 账户的插件，也不包含插件安装所需的包装。运行本技能本身不需要 API 密钥、额外脚本或外部账号连接。

实际验证范围见 [验证说明](../tests/verification.md)。以下安装路线依据 2026-10-14 实际读取的官方文档与审查环境随附安装器说明核对；文档描述不等于该设备已经安装成功。

## 路线一：手动安装本地 Codex Skill

1. 从实际公开仓库下载源文件 ZIP 并解压。仓库发布前，可使用经过审查的本地文件包。
2. 找到 `skills/prompt-architect/`，确认其中包含 `SKILL.md` 和 `agents/openai.yaml`。
3. 将整个 `prompt-architect` 文件夹复制到目标 Codex 支持的发现目录。先检查是否已有同名技能，避免覆盖或保留多个同名副本。
4. 打开新的 Codex 会话，检查技能清单中是否出现 `prompt-architect`。未出现时检查目录、元数据及客户端版本；必要时重启 Codex。

当前官方文档列出的用户和仓库发现目录如下。[官方本地技能说明](https://learn.chatgpt.com/docs/build-skills)

| 范围 | 安装后的位置 | 用途 |
| --- | --- | --- |
| 用户 | `~/.agents/skills/prompt-architect/` | 在该用户的多个工作仓库使用 |
| 仓库 | `.agents/skills/prompt-architect/` | 相对于目标工作仓库；Codex 从工作目录向上扫描至仓库根目录 |

仓库中的 `skills/prompt-architect/` 是分发源文件位置；仅下载到这里，不等于已进入上述发现目录。`~` 表示当前用户的个人目录；这些路径是位置说明，不是需要在所有终端原样执行的命令。

## 路线二：使用 Skill Installer

如果当前 Codex 提供 `skill-installer`，官方支持用它从其他仓库下载技能。[官方安装器使用说明](https://learn.chatgpt.com/docs/build-skills#install-curated-skills-for-local-use)

在公开仓库实际存在后，复制真实仓库链接，连同以下要求交给安装器：

```text
$skill-installer 请从我提供的真实公开仓库链接，安装 skills/prompt-architect。
先阅读当前安装器说明并核对目标 Codex 的技能发现目录。
先检查是否已有同名技能，已有时不要直接覆盖。
若安装器默认目的地与客户端发现目录不同，使用当前安装器支持的目标目录选项。
安装后请分别检查文件存在、客户端发现及显式调用，不要仅凭复制完成声称可用。
```

本次审查环境随附的安装器默认写入 `$CODEX_HOME/skills/`；未设置时为 `~/.codex/skills/`，并提供 `--dest` 选项。这是该安装器版本的行为，与上文当前官方发现目录不同。不要把 `~/.codex/skills/` 宣称为所有当前客户端的统一默认目录，也不要同时在两套目录放置同名副本。目标目录应根据实际客户端与安装器版本核实。

本仓库未填入尚不存在的公开下载 URL。通过安装器下载公开文件需要网络；本技能的需求澄清流程本身不依赖 GitHub 连接。

## 安装后的基本检查

在支持本技能的 Codex 中，用独立会话检查以下行为：

| 检查 | 输入 | 预期 |
| --- | --- | --- |
| 明确需求 | `$prompt-architect 请生成给 ChatGPT 的任务指令：把稍后提供的笔记整理成五条复习要点，每条不超过两句话，只依据原文。` | 直接生成指令，保留数量、长度和来源限制，不重复追问 |
| 模糊需求 | `请帮我澄清需求，再生成给 AI 的任务指令：我想改善学习效率，但不知道从哪里开始。` | 若宿主自动选择本技能，先问少量关键问题，不擅自确定方案 |
| 普通问答 | `Repository 是什么意思？用一句话解释。` | 直接回答，不自动开启需求访谈 |

Codex CLI/IDE 官方支持通过 `$技能名` 或 `/skills` 显式选择技能。桌面界面应以实际技能选择器为准。自动选择是否成功，需要宿主选择或读取本技能的证据；答案风格相似不足以证明已经加载。[官方调用说明](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills)

## ChatGPT / Work 插件路线

官方区分本地独立 Skill 与插件：桌面版可使用独立 Skill；要在网页、手机的 Chat/Work 中分发和使用技能，官方提供插件包装与安装路线。本仓库没有完成这项包装、目录发布或账户安装，也未验证这些客户端调用。[官方技能与分发说明](https://learn.chatgpt.com/docs/build-skills)

后续如需插件版本，应单独制作、测试与发布插件。在支持的 ChatGPT 界面通过 Plugins 安装，开始新会话后，在 `@` 菜单中选择实际可见的插件或技能。这属于另一条安装路线，不能用本地复制结果代替。[官方插件安装说明](https://learn.chatgpt.com/docs/plugins)

用户账户是否具备插件创建权限、Plugin Creator 是否可用，以及工作区是否允许安装，仍需在实际账户确认。本地文件无法证明这些权限。正式制作插件前应核对权限与官方流程。[官方插件制作前提](https://learn.chatgpt.com/docs/build-plugins#before-you-start)

如果目标环境无法原生加载，可以向 AI 提供 `SKILL.md`，明确要求按它的流程工作。这属于手动指令使用，不是原生安装或插件调用成功。

## 换设备与记录结果

每台设备分别安装与验收。GitHub 保存技能源文件，不会自动为其他设备或 ChatGPT 账户启用技能。macOS/Linux 的安装位置说明来自官方规则，本项目尚未在这些系统实测；具体范围统一见 [验证说明](../tests/verification.md)。

分别记录文件复制、宿主发现、显式调用、自动选择和目标客户端调用。公开记录只保留必要结论；不要附带个人路径、账号、凭据、私人会话或原始运行日志。
