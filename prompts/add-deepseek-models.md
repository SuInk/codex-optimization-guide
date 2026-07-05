# Add DeepSeek Local Models

Add these two DeepSeek models to the local Codex configuration:

- `deepseek-v4-flash`
- `deepseek-v4-pro`

Requirements:

1. Before editing, back up every file that will be modified. Use timestamped backup names.
2. Check `~/.codex/config.toml` and `~/.codex/models_cache.json`.
3. Do not modify the existing provider.
4. Do not modify `model_provider`.
5. Do not modify any `[model_providers.*]`.
6. Do not modify `base_url`.
7. Do not modify tokens or API keys.
8. Both models must continue using the existing provider from the current `config.toml`.
9. Update the existing `~/.codex/models_cache.json`.
10. Preserve the existing `models_cache.json` schema. Do not invent unrelated fields.
11. In the model menu or catalog, place both models after the existing GPT models and before `codex-auto-review`.
12. Use the real model name for both `display_name` and `slug`:
    - `deepseek-v4-flash`
    - `deepseek-v4-pro`
13. Do not use `none` or `max` for reasoning.
14. Reasoning may only use:
    - `low`
    - `medium`
    - `high`
    - `xhigh`
15. Set default `reasoning_effort` or `default_reasoning_level` to `medium`.
16. After editing, verify with `codex debug models` or an equivalent method that Codex actually reads:
    - `deepseek-v4-flash`
    - `deepseek-v4-pro`
17. Confirm the order, `display_name`, `slug`, and reasoning levels.
18. If editing only `models_cache.json` does not make the models appear in Codex, add this top-level key to `config.toml`:

```toml
model_catalog_json = "~/.codex/models_cache.json"
```

Still do not modify the provider, `base_url`, or tokens.

When done, report:

- Files changed
- Backup paths
- Whether `model_catalog_json` was used
- Verification result
