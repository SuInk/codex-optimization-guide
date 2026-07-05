# 新增 DeepSeek 本地模型

默认教程语言是英文。英文版：[add-deepseek-models.md](add-deepseek-models.md)。

使用 [中文 prompt](../prompts/add-deepseek-models.zh-CN.md) 新增以下本地 catalog 模型：

- `deepseek-v4-flash`
- `deepseek-v4-pro`

要点：

- 修改前先备份文件。
- 复用现有 provider。
- 不修改 `model_provider`、provider section、`base_url` 或 token。
- 同步修改 `models_cache.json`。
- 使用 `codex debug models` 或等效命令验证。
