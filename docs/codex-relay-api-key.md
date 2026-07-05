# Use a Relay API Key with Codex

English | [中文](#中文)

This guide configures Codex to use an OpenAI-compatible relay provider through the Responses API.

## Table of Contents

- [Target](#target)
- [Files](#files)
- [`auth.json`](#authjson)
- [`config.toml`](#configtoml)
- [Notes](#notes)
- [中文](#中文)
- [目录](#目录)
- [目标](#目标)
- [文件](#文件)
- [`auth.json`](#authjson-1)
- [`config.toml`](#configtoml-1)
- [注意事项](#注意事项)

## Target

- Use a relay API key in `sk-...` format.
- Route requests through a custom `base_url`.
- Use OpenAI Responses API wire format.
- Avoid storing the key in `~/.codex/auth.json`.

## Files

- `~/.codex/auth.json`
- `~/.codex/config.toml`

## `auth.json`

Set Codex auth mode to ChatGPT mode and clear the local OpenAI API key field:

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

## `config.toml`

Add or update `model_provider` in the top-level config area:

```toml
model_provider = "OpenAI"
```

Then add or update the OpenAI provider section:

```toml
[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://替换为中转站地址"
wire_api = "responses"
experimental_bearer_token = "sk-替换为中转站apikey"
requires_openai_auth = true
```

## Notes

- If `[model_providers.OpenAI]` already exists, update the existing section instead of adding a duplicate.
- Do not blindly paste the whole provider table as the first lines of an existing TOML file. In TOML, keys after a table header belong to that table until the next table header.
- For an existing config, keep top-level keys in the top-level area and place `[model_providers.OpenAI]` as its own section.
- Preserve unrelated settings in `config.toml`.
- Restart Codex or open a new session after changing these files so the configuration is reloaded.

---

## 中文

本教程用于将 Codex 配置为通过 OpenAI 兼容中转站调用 Responses API。

## 目录

- [目标](#目标)
- [文件](#文件)
- [`auth.json`](#authjson-1)
- [`config.toml`](#configtoml-1)
- [注意事项](#注意事项)
- [English](#use-a-relay-api-key-with-codex)
- [Table of Contents](#table-of-contents)
- [Target](#target)
- [Files](#files)
- [`auth.json`](#authjson)
- [`config.toml`](#configtoml)
- [Notes](#notes)

## 目标

- 使用 `sk-...` 格式的中转站 API Key。
- 请求通过自定义 `base_url` 转发。
- 使用 OpenAI Responses API 协议。
- 不把 API Key 存在 `~/.codex/auth.json`。

## 文件

- `~/.codex/auth.json`
- `~/.codex/config.toml`

## `auth.json`

将 Codex 认证模式设为 ChatGPT 模式，并清空本地 OpenAI API Key 字段：

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

## `config.toml`

在顶层配置区域增加或更新 `model_provider`：

```toml
model_provider = "OpenAI"
```

然后新增或更新 OpenAI provider section：

```toml
[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://替换为中转站地址"
wire_api = "responses"
experimental_bearer_token = "sk-替换为中转站apikey"
requires_openai_auth = true
```

## 注意事项

- 如果 `[model_providers.OpenAI]` 已经存在，在原 section 内补齐或更新字段，不要重复创建 section。
- 不要把整个 provider table 直接粘到已有 TOML 文件第一行。TOML 中 table header 后面的字段会归属到该 table，直到下一个 table header。
- 对已有配置文件，应保持顶层字段仍在顶层区域，并将 `[model_providers.OpenAI]` 作为独立 section 放置。
- 保留 `config.toml` 中其它无关配置。
- 修改后重启 Codex 或新开会话，让配置重新加载。
