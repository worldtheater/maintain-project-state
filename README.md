# Maintain Project State

<img src="assets/icon.png" alt="Maintain Project State" width="128" height="128">

为 Codex 跨会话继续工作维护简洁、有证据支持的项目快照。这是独立 skill 仓库，不包含插件清单、MCP 或 hooks。

状态文件是导航和交接材料；源码、测试、日志及已接受的设计文档仍是权威依据。

## 安装

仓库地址：[worldtheater/maintain-project-state](https://github.com/worldtheater/maintain-project-state)。版本：`v0.1.1`。

在 Codex 中请求：

```text
$skill-installer 从 https://github.com/worldtheater/maintain-project-state 安装仓库根目录的 maintain-project-state skill
```

也可手动安装：克隆仓库，将包含 `SKILL.md` 的目录复制到 `~/.agents/skills/maintain-project-state/`（个人使用），或目标项目的 `.agents/skills/maintain-project-state/`（项目使用）。复制 `SKILL.md`、`agents/`、`assets/` 和 `LICENSE`，不要复制 `.git`。`agents/openai.yaml` 提供名称、图标和起始提示词；技能正文保持在根目录 `SKILL.md`。

安装后开始新的 Codex 会话；客户端未显示时重启。通过 `/skills` 或 `$maintain-project-state` 查找和调用。

## 使用

- “查看项目进展并核对相关证据，不修改文件。”
- “初始化当前仓库的项目状态。”
- “更新项目状态，为换会话继续工作做交接。”

默认状态路径为项目根目录的 `.codex/project-state.md`；用户或项目指定的路径优先。

查询只读；初始化和维护需要用户或仓库指令授权。实现、验证和未提交工作分别记录。skill 不授权自动提交、推送或修改仓库指令文件，也不会解除沙箱写入限制。

也可从 [v0.1.1 源码 ZIP](https://github.com/worldtheater/maintain-project-state/archive/refs/tags/v0.1.1.zip) 下载，解压后按上面的手动安装方式复制文件。

## 更新

维护者修改 `SKILL.md` 并测试后提交、推送到 GitHub。已安装的 skill 是本地副本，不保证自动同步；使用者需要重新安装或明确更新本地副本。覆盖前请保留自己的修改。

## 验证

见 [TESTING.md](TESTING.md)，其中记录当前独立 skill 布局的安装与行为验证，以及尚未覆盖的范围。

## 许可

作者：**worldtheater**。

采用 [MIT License](LICENSE)，允许使用、修改和再分发；需保留版权与许可声明。
