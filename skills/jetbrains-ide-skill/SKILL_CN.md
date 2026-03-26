# JetBrains IDE MCP 全维度集成技能

| 类别 | 优化层级 |
| :--- | :--- |
| **兼容性** | 针对 2026.1+ 环境深度特调 |
| **操作模式** | 自主专家代理 (具备自愈能力) |

## 1. 专家级开发协议 (强制执行)

### 步骤 0：环境自动检测
- **首要动作**：探测 `jetbrains` 命名空间工具是否可用。
- **回退机制**：若服务离线，回退至原生 Shell/文件工具，并告知用户当前无法进行 IDE 语义校验。

### 步骤 1：上下文锚定与项目映射
1. **焦点同步**：调用 `get_active_editor_context` 和 `get_all_open_file_paths` 同步用户当前关注的代码范围。
2. **项目解析**：针对多模块项目，必须先调用 `get_project_modules` 和 `get_repositories` 解析绝对路径和 VCS 根目录。

### 步骤 2：高精度修改策略
1. **语义内省**：修改前先通过 `get_symbol_info` 和 `get_project_dependencies` 确认代码语义及库版本。
2. **滑动窗口策略**：超过 500 行的文件，**严禁全量读取**。需通过搜索定位行号，仅读取目标行前后 50 行。
3. **精准编辑**：重构优先使用 `rename_refactoring`；逻辑修改使用 `replace_text_in_file`。

### 步骤 3：校验与自愈闭环
1. **实时诊断**：代码写入后**必须立即**调用 `get_file_problems`。
2. **自主修复**：若存在错误，分析诊断信息并持续修复，直到 IDE 状态清零。
3. **验证执行**：利用 `get_run_configurations` 运行构建或测试以确认修改。
4. **格式化与同步**：执行 `reformat_file` 并调用 `open_file_in_editor` 引导用户视检。

## 2. 完整工具参考指南

### A. 搜索与导航
- `find_files_by_name_keyword`：通过部分文件名快速定位的最快方式。
- `find_files_by_glob`：使用 Glob 模式（如 `**/dto/*.java`）筛选。
- `search_in_files_by_text/regex`：基于索引的高速全局内容搜索。
- `list_directory_tree`：递归展示目录树结构，用于探索项目。
- `get_all_open_file_paths`：列出当前编辑器中所有打开的标签页。

### B. 分析与文档
- `get_file_problems`：获取 IDE 实时诊断信息（兼容 Java 26/Spring 4）。
- `get_symbol_info`：获取方法签名、类型及“快速文档”。
- `get_project_dependencies`：分析完整的依赖树（Maven/Gradle/Cargo）。

### C. 修改与重构
- `get_file_text_by_path`：读取文件内容（严格遵守滑动窗口限制）。
- `create_new_file`：自动创建文件及其父目录。
- `replace_text_in_file`：针对性的逻辑代码替换。
- `rename_refactoring`：跨文件的安全语义重命名，自动更新引用。
- `reformat_file`：应用 IDE 配置的代码风格。

### D. 执行与终端
- `get_run_configurations`：列出所有可用的运行与测试配置。
- `execute_run_configuration`：执行配置并捕获输出。
- `execute_terminal_command`：支持流式输出的受管终端执行。

### E. 数据库与 VCS (2026.1+ 专项能力)
- `get_database_schema`：内省数据库表、字段及关联关系。
- `execute_sql_query`：直接在已连接数据源上运行并验证 SQL。
- `get_vcs_diff`：获取未提交变更，用于风险评估。
- `get_repositories`：识别多库项目中的所有 VCS 根目录。
- `get_active_editor_context`：精确探测用户光标位置及选中的代码块。

## 3. 工程约束与安全
- **勇敢模式 (Brave Mode)**：仅限非破坏性构建命令。
- **数据安全**：涉及 `rm`, `git reset` 或包含 `DELETE/DROP` 的 SQL 时，**必须**请求手动确认。
- **隐私保护**：禁止在日志中泄露绝对系统路径或环境变量中的敏感密钥。
