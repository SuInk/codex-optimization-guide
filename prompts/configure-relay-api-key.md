# Prompt: Configure Codex Relay API Key

你是一个本地配置助手。请帮我把 Codex 配置为使用中转站 API Key。

## 目标

- 中转站 API Key 是 `sk-...` 格式
- 请求走 OpenAI Responses API
- 使用自定义中转站 `base_url`
- 不再把 API Key 放在 `auth.json` 的 `OPENAI_API_KEY` 中

## 需要修改的文件

### 1. 修改 `~/.codex/auth.json`

将内容调整为：

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

### 2. 修改 `~/.codex/config.toml`

确保存在以下配置：

```toml
model_provider = "OpenAI"

[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://替换为中转站地址"
wire_api = "responses"
experimental_bearer_token = "sk-替换为中转站apikey"
requires_openai_auth = true
```

## 修改要求

- 如果 `config.toml` 已经有 `[model_providers.OpenAI]`，就在原 section 内补齐或更新这些字段，不要重复创建 section
- 保留 `config.toml` 中其它无关配置
- 不要把 API Key 写回 `auth.json`
- 修改完成后读取文件确认关键字段已经生效
- 最后提醒我重启 Codex 或新开会话，让配置重新加载

## 验收标准

修改后 `~/.codex/auth.json` 应满足：

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

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
