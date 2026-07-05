# 使用 API Key 同时保留登录态

默认教程语言是英文。英文版：[use-api-key-preserve-login.md](use-api-key-preserve-login.md)。

当你希望 Codex 模型请求使用 API Key，同时保留 ChatGPT/Codex 登录态时，使用 [中文 prompt](../prompts/use-api-key-preserve-login.zh-CN.md)。

要点：

- `auth.json` 要保留 `tokens`、`last_refresh` 等登录字段。
- `auth.json` 里的 `OPENAI_API_KEY` 应为 `null`。
- API Key 应写在当前启用 provider 配置里，通常是 `experimental_bearer_token`。
- 保留登录态后，Codex 插件、连接器和移动端控制功能可以继续使用。
