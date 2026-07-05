# Configure a Relay API Key

Default language: English. Chinese version: [configure-relay-api-key.zh-CN.md](configure-relay-api-key.zh-CN.md).

Use [the English prompt](../prompts/configure-relay-api-key.md) to configure Codex with an OpenAI-compatible relay API key.

Key points:

- Keep `auth.json` login fields such as `tokens` and `last_refresh`.
- Store the relay key in `config.toml` as `experimental_bearer_token`.
- Keep provider configuration in `[model_providers.OpenAI]`.
- Restart Codex or open a new session after editing.
