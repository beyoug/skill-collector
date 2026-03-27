# Skill Collector (技能库) 🚀

这是一个个人调试并使用的 AI 专家协议与 MCP (Model Context Protocol) 技能集合，旨在提升开发效率，相关内容仅供参考。

---

## 📂 技能列表 (Skill List)

<details>
<summary><b>JetBrains IDE 全维度集成技能</b> (jetbrains-ide)</summary>

针对 JetBrains 系列 IDE 的深度 MCP 适配，支持语义内省、精准重构与实时诊断。

| 文件 | 语言 | 说明 |
| :--- | :---: | :--- |
| [SKILL_CN.md](./skills/jetbrains-ide/SKILL_CN.md) | 中文 | OpenCode Agent 标准格式 |
| [SKILL.md](./skills/jetbrains-ide/SKILL.md) | English | OpenCode Agent standard format |

### 🔧 安装方式（OpenCode）

```bash
# 全局安装（选择你偏好的语言版本）
cp skills/jetbrains-ide/SKILL_CN.md ~/.config/opencode/agents/jetbrains-ide.md
# 或
cp skills/jetbrains-ide/SKILL.md ~/.config/opencode/agents/jetbrains-ide.md

# 项目级安装
cp skills/jetbrains-ide/SKILL_CN.md .opencode/agents/jetbrains-ide.md
```

> 复制时建议重命名为 `jetbrains-ide.md`，安装后通过 `@jetbrains-ide` 调用。

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
