# 使用 API Key 同时保留 Codex 登录态

请配置本地 Codex：模型请求使用 API Key，但保留已有 ChatGPT/Codex 登录态，这样插件、连接器和移动端控制功能仍然可用。

## 目标

- 模型请求使用 API Key。
- Codex 保持登录态。
- 保留 `auth.json` 里的 `tokens`、`last_refresh` 等登录字段。
- 不要把 API Key 写到 `auth.json` 的 `OPENAI_API_KEY`。
- API Key 写到当前启用的 model provider 配置里。

## 需要处理的文件

### 1. 处理 `~/.codex/auth.json`

不要重写整个文件。只确认或修改以下两个字段：

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

如果文件里还有 `tokens`、`last_refresh` 或其它登录相关字段，全部保留，不要删除。这些字段用于依赖登录态的 Codex 功能。

### 2. 处理 `~/.codex/config.toml`

除非我明确要求切换 provider，否则保留当前启用的 provider。

如果当前启用的是 `OpenAI` provider，对应 section 应包含类似配置：

```toml
model_provider = "OpenAI"

[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://替换为服务商地址"
wire_api = "responses"
experimental_bearer_token = "sk-替换为apikey"
requires_openai_auth = true
```

## 处理要求

- 修改前先备份所有会改到的文件。
- 保留 `config.toml` 中其它无关配置。
- 保留 `auth.json` 中已有登录态。
- 不要删除 `auth.json` 中的 `tokens`、`last_refresh` 或其它登录字段。
- 不要把 API Key 写回 `auth.json`。
- 不要重复创建已有的 `[model_providers.*]` section。
- 如果 provider section 已存在，就在原 section 内更新。
- provider 字段必须放在正确 TOML section 内，不要把 provider table 直接粘到已有 TOML 文件第一行。
- 处理完成后读取文件确认关键字段已经生效。
- 最后提醒我重启 Codex 或新开会话，让配置重新加载。

## 验收标准

`~/.codex/auth.json` 至少应满足：

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

文件中原本存在的登录字段可以继续保留。

`~/.codex/config.toml` 当前启用的 provider 中应包含：

```toml
experimental_bearer_token = "sk-你的apikey"
```

最终效果应是：Codex 模型请求走 API Key，同时插件、连接器和移动端控制等依赖登录态的功能仍然可用。
