# Skill Collector (技能库) 🚀

这是一个个人调试并使用的 AI 专家协议与 MCP (Model Context Protocol) 技能集合，旨在提升开发效率，相关内容仅供参考。

---

## 📂 技能列表 (Skill List)

<details>
<summary><b>JetBrains IDE 全维度集成技能</b> (jetbrains-ide-skill)</summary>

针对 JetBrains 系列 IDE 的深度 MCP 适配，支持语义内省、精准重构与实时诊断。

| 文件 | 语言 | 说明 |
| :--- | :---: | :--- |
| [jetbrains-ide.md](./skills/jetbrains-ide-skill/jetbrains-ide.md) | 中文 | OpenCode Agent 标准格式 |
| [jetbrains-ide-en.md](./skills/jetbrains-ide-skill/jetbrains-ide-en.md) | English | OpenCode Agent standard format |

### 🔧 安装方式（OpenCode）

```bash
# 全局安装（选择你偏好的语言版本）
cp skills/jetbrains-ide-skill/jetbrains-ide.md ~/.config/opencode/agents/
# 或
cp skills/jetbrains-ide-skill/jetbrains-ide-en.md ~/.config/opencode/agents/

# 项目级安装
cp skills/jetbrains-ide-skill/jetbrains-ide.md .opencode/agents/
```

安装后可通过 `@jetbrains-ide` 或 `@jetbrains-ide-en` 手动调用，或由主 Agent 根据任务上下文自动触发。

### 💬 全局提示词 (System Prompt) 示例

```text
## JetBrains IDE Strategy
任务开始前检测 `jetbrains` 命名空间：
- **可用**：调用 @jetbrains-ide 按完整专家协议执行，禁止绕过 IDE 直接操作文件。
- **不可用**：切换通用模式并告知用户。
```

</details>

---

*欢迎补充一些好用的SKILL*
