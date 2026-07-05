# Use an API Key While Preserving Login State

Default language: English. Chinese version: [use-api-key-preserve-login.zh-CN.md](use-api-key-preserve-login.zh-CN.md).

Use [the English prompt](../prompts/use-api-key-preserve-login.md) when you want Codex model requests to use an API key while keeping ChatGPT/Codex login state.

Key points:

- `auth.json` should keep login fields such as `tokens` and `last_refresh`.
- `OPENAI_API_KEY` in `auth.json` should be `null`.
- The API key belongs in the active provider config, usually `experimental_bearer_token`.
- Keeping login state allows Codex plugins, connectors, and mobile control features to keep working.
