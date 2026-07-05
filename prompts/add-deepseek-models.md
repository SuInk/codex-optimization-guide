# Prompt: Add DeepSeek Models to Codex Local Catalog

请在本地 Codex 配置里新增两个 DeepSeek 模型：

- `deepseek-v4-flash`
- `deepseek-v4-pro`

## 目标

- 两个模型都继续使用当前 `~/.codex/config.toml` 里的现有 provider。
- 不修改现有 provider 配置。
- 不修改 `base_url`。
- 不修改 token 或 API Key。
- 同步修改已有的 `~/.codex/models_cache.json`。
- 修改后验证 Codex 实际读取到了新增模型。

## 修改前要求

1. 先检查 `~/.codex/config.toml` 和 `~/.codex/models_cache.json` 是否存在。
2. 修改前先备份所有会改到的文件，备份文件名带时间戳。
3. 读取现有 `models_cache.json`，先理解它的 schema，不要凭空发明字段结构。

## 禁止修改

不要修改以下内容：

- 现有 provider
- `model_provider`
- 任何 `[model_providers.*]`
- `base_url`
- token 或 API Key

唯一允许的 `config.toml` 变更：

- 如果只修改 `models_cache.json` 后 Codex 实际菜单没有读取新增模型，可以在 `config.toml` 顶层增加：

```toml
model_catalog_json = "~/.codex/models_cache.json"
```

即使使用这个兜底项，也仍然不要修改 provider、`base_url` 或 token。

## 模型插入要求

在模型菜单/catalog 中新增：

- `deepseek-v4-flash`
- `deepseek-v4-pro`

插入位置：

- 放在现有 GPT 模型后面
- 放在 `codex-auto-review` 前面

字段要求：

- `display_name = deepseek-v4-flash`
- `slug = deepseek-v4-flash`
- `display_name = deepseek-v4-pro`
- `slug = deepseek-v4-pro`
- provider 字段或 provider 引用复用现有 catalog 条目的写法
- 默认 reasoning 设置为 `medium`

reasoning 限制：

- 不要使用 `none`
- 不要使用 `max`
- 只允许：
  - `low`
  - `medium`
  - `high`
  - `xhigh`

如果 schema 里有 `reasoning_effort`、`default_reasoning_level` 或类似字段，默认值设为 `medium`。

## 验证要求

修改后运行：

```bash
codex debug models
```

如果该命令不可用，使用当前 Codex 安装支持的等效方式验证实际读取到的模型 catalog。

必须确认：

- 能看到 `deepseek-v4-flash`
- 能看到 `deepseek-v4-pro`
- 两个模型位于现有 GPT 模型后面
- 两个模型位于 `codex-auto-review` 前面
- 两个模型的 `display_name` 正确
- 两个模型的 `slug` 正确
- reasoning 档位只包含 `low`、`medium`、`high`、`xhigh`
- 默认 reasoning 是 `medium`

## 输出要求

最后请说明：

- 实际修改了哪些文件
- 备份文件路径
- Codex 实际读取到的验证结果
- 是否使用了 `model_catalog_json` 兜底项
