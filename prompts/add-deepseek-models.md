# 新增 DeepSeek 本地模型

请在本地 Codex 配置里新增两个 DeepSeek 模型：

- `deepseek-v4-flash`
- `deepseek-v4-pro`

要求：

1. 修改前先备份所有会改到的文件，备份文件名带时间戳。
2. 检查 `~/.codex/config.toml` 和 `~/.codex/models_cache.json`。
3. 不要修改现有 provider。
4. 不要修改 `model_provider`。
5. 不要修改任何 `[model_providers.*]`。
6. 不要修改 `base_url`。
7. 不要修改 token 或 API Key。
8. 两个模型都继续使用当前 `config.toml` 里的现有 provider。
9. 同步修改已有的 `~/.codex/models_cache.json`。
10. 保持 `models_cache.json` 现有 schema，不要凭空发明新字段结构。
11. 在模型菜单或 catalog 中，把两个模型放在现有 GPT 模型后面、`codex-auto-review` 前面。
12. `display_name` 和 `slug` 都使用实际模型名：
    - `deepseek-v4-flash`
    - `deepseek-v4-pro`
13. reasoning 不要使用 `none`，也不要使用 `max`。
14. reasoning 只允许使用：
    - `low`
    - `medium`
    - `high`
    - `xhigh`
15. 默认 `reasoning_effort` 或 `default_reasoning_level` 设置为 `medium`。
16. 修改后用 `codex debug models` 或等效方式验证 Codex 实际读取到：
    - `deepseek-v4-flash`
    - `deepseek-v4-pro`
17. 验证并说明顺序、`display_name`、`slug`、reasoning 档位是否正确。
18. 如果只修改 `models_cache.json` 后 Codex 实际菜单没有读取新增模型，可以在 `config.toml` 顶层添加：

```toml
model_catalog_json = "~/.codex/models_cache.json"
```

但仍然不要修改 provider、`base_url` 或 token。

完成后请输出：

- 修改了哪些文件
- 备份文件路径
- 是否使用了 `model_catalog_json`
- 验证结果
