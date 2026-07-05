# 配置 Codex 中转站 API Key

你是一个本地配置助手。请帮我把 Codex 配置为使用中转站 API Key。

## 目标

- 中转站 API Key 是 `sk-...` 格式
- 请求走 OpenAI Responses API
- 使用自定义中转站 `base_url`
- 不再把 API Key 放在 `auth.json` 的 `OPENAI_API_KEY` 中

## 需要处理的文件

### 1. 处理 `~/.codex/auth.json`

不要重写整个文件。只确认或修改以下两个字段：

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

如果文件里还有 `tokens`、`last_refresh` 或其它字段，全部保留，不要删除。

### 2. 在 `~/.codex/config.toml` 增加中转配置

在文件顶层配置区域增加或确认：

```toml
model_provider = "OpenAI"
```

然后新增或更新 provider section：

```toml
[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://替换为中转站地址"
wire_api = "responses"
experimental_bearer_token = "sk-替换为中转站apikey"
requires_openai_auth = true
```

## 处理要求

- 如果 `config.toml` 已经有 `[model_providers.OpenAI]`，就在原 section 内补齐或更新这些字段，不要重复创建 section。
- 不要把整个 `[model_providers.OpenAI]` table 直接粘到已有 TOML 文件第一行；TOML 中 table header 后面的字段会归属到该 table，可能破坏原有顶层配置。
- `model_provider = "OpenAI"` 应位于顶层配置区域。
- `[model_providers.OpenAI]` 应作为独立 section 存在。
- 保留 `config.toml` 中其它无关配置。
- 不要把 API Key 写回 `auth.json`。
- 不要删除 `auth.json` 中已有的登录 token 或其它字段。
- 处理完成后读取文件确认关键字段已经生效。
- 最后提醒我重启 Codex 或新开会话，让配置重新加载。

## 验收标准

修改后 `~/.codex/auth.json` 至少应满足：

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

文件中原本存在的其它字段可以继续保留。

并且 `~/.codex/config.toml` 中应包含：

```toml
model_provider = "OpenAI"

[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://你的中转站地址"
wire_api = "responses"
experimental_bearer_token = "sk-你的中转站apikey"
requires_openai_auth = true
```
