# JetBrains IDE Full-Spectrum MCP Integration

| Category | Optimization Level |
| :--- | :--- |
| **Compatibility** | Specialized for 2026.1+ Environments |
| **Operation Mode** | Autonomous Expert Agent (Self-Healing) |

## 1. The Expert Developer Protocol (Mandatory)

### Step 0: Environment Detection
- **Initial Check**: Detect the `jetbrains` tool namespace. 
- **Fallback**: If unavailable, revert to standard Shell/File tools and notify the user that IDE-backed semantic validation is offline.

### Step 1: Context Anchoring & Mapping
1. **Focus Sync**: Use `get_active_editor_context` and `get_all_open_file_paths` to align with the user's active focus.
2. **Project Resolution**: For multi-module projects, call `get_project_modules` and `get_repositories` to resolve absolute paths and VCS roots.

### Step 2: High-Precision Modification
1. **Semantic Introspection**: Call `get_symbol_info` and `get_project_dependencies` to understand code semantics and library versions before editing.
2. **Sliding Window Strategy**: For files >500 lines, **strictly prohibit** full-file reads. Use `search_in_files_by_text` to find line numbers and read only ±50 lines surrounding the target area.
3. **Editing**: Prioritize `rename_refactoring` for symbols; use `replace_text_in_file` for logic.

### Step 3: Verification & Self-Healing
1. **Real-time Diagnostics**: Immediately call `get_file_problems` after every write.
2. **Autonomous Correction**: If errors exist, analyze diagnostics and fix until the state is zero-error.
3. **Execution**: Use `get_run_configurations` and `execute_run_configuration` to verify builds/tests.
4. **Finalization**: Run `reformat_file` and `open_file_in_editor` to sync the UI.

## 2. Exhaustive Tool Reference

### A. Search & Navigation
- `find_files_by_name_keyword`: Fastest search by partial file name.
- `find_files_by_glob`: Search using patterns (e.g., `**/dto/*.java`).
- `search_in_files_by_text/regex`: High-speed indexed global content search.
- `list_directory_tree`: Recursive visual exploration of the project.
- `get_all_open_file_paths`: List currently active editor tabs.

### B. Analysis & Documentation
- `get_file_problems`: Fetches real-time IDE inspections (Java 26/Spring 4 compatible).
- `get_symbol_info`: Retrieves signatures, types, and "Quick Documentation".
- `get_project_dependencies`: Analyzes the full dependency tree (Maven/Gradle/Cargo).

### C. Modification & Refactoring
- `get_file_text_by_path`: Reads file content (respecting sliding window limits).
- `create_new_file`: Generates new files with automatic parent directory creation.
- `replace_text_in_file`: Targeted search-and-replace for logic updates.
- `rename_refactoring`: Safe, context-aware semantic renaming across the project.
- `reformat_file`: Applies IDE-configured code style.

### D. Execution & Terminal
- `get_run_configurations`: Lists all available dev/test run targets.
- `execute_run_configuration`: Executes a run config and captures output.
- `execute_terminal_command`: Managed shell execution with streamed output support.

### E. Database & VCS (2026.1+ Specialized)
- `get_database_schema`: Introspects live tables, columns, and relations.
- `execute_sql_query`: Validates and runs SQL against connected data sources.
- `get_vcs_diff`: Retrieves uncommitted changes for risk evaluation.
- `get_repositories`: Identifies all VCS roots in multi-repo projects.
- `get_active_editor_context`: Precise detection of cursor position and selected blocks.

## 3. Engineering Constraints
- **Brave Mode**: Enabled only for non-destructive commands.
- **Data Safety**: Mandatory user confirmation for `rm`, `git reset`, or `execute_sql_query` involving `DELETE/DROP`.
- **Privacy**: Automated masking of absolute system paths and environment secrets.
