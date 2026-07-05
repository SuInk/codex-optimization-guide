# 配置中转站 API Key

默认教程语言是英文。英文版：[configure-relay-api-key.md](configure-relay-api-key.md)。

使用 [中文 prompt](../prompts/configure-relay-api-key.zh-CN.md) 配置 OpenAI 兼容中转站 API Key。

要点：

- 保留 `auth.json` 中已有的 `tokens`、`last_refresh` 等登录字段。
- 中转站 key 写入 `config.toml` 的 `experimental_bearer_token`。
- provider 配置放在 `[model_providers.OpenAI]`。
- 修改后重启 Codex 或新开会话。
