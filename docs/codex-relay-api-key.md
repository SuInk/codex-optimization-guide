# Use a Relay API Key with Codex

This guide configures Codex to use an OpenAI-compatible relay provider through the Responses API.

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

Ensure `model_provider` points to `OpenAI`, then configure the OpenAI provider:

```toml
model_provider = "OpenAI"

[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://替换为中转站地址"
wire_api = "responses"
experimental_bearer_token = "sk-替换为中转站apikey"
requires_openai_auth = true
```

## Notes

- If `[model_providers.OpenAI]` already exists, update the existing section instead of adding a duplicate.
- Preserve unrelated settings in `config.toml`.
- Restart Codex or open a new session after changing these files so the configuration is reloaded.
