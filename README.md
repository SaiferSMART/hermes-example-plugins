# hermes-example-plugins

Reference plugins for [hermes-agent](https://github.com/NousResearch/hermes-agent) — small, focused examples that show how a single plugin surface works, end to end.

These are **not bundled with `hermes-agent`**. The core repo ships only the plugins users actually run (memory providers, the disk-cleanup hook, platform adapters). Reference plugins live here so plugin authors can read them, copy them, install them as user plugins, and ignore them otherwise.

## Index

| Plugin | Surface | Demonstrates |
|---|---|---|
| [`plugin-llm-example`](./plugin-llm-example) | `ctx.llm.complete_structured()` | Host-owned structured LLM calls — typed text/image input, JSON Schema validation, trust-gate config |
| [`plugin-llm-async-example`](./plugin-llm-async-example) | `ctx.llm.acomplete()` + `asyncio.gather()` | Async LLM lane — concurrent forward + sentiment + back-translation pass for `/translate` |
| [`example-dashboard`](./example-dashboard) | `dashboard/manifest.json` | Bare-minimum dashboard plugin — a tab, a slot injection, a backend route |
| [`strike-freedom-cockpit`](./strike-freedom-cockpit) | dashboard theme + slot plugin | Complete custom-skin reskin — palette, layout variant, asset slots, sidebar HUD |

## Installing an example as a user plugin

Each directory is a self-contained plugin. To run one in your own Hermes Agent setup:

```bash
git clone https://github.com/NousResearch/hermes-example-plugins.git

# pick whichever you want
cp -r hermes-example-plugins/plugin-llm-example       ~/.hermes/plugins/
cp -r hermes-example-plugins/plugin-llm-async-example ~/.hermes/plugins/
cp -r hermes-example-plugins/example-dashboard        ~/.hermes/plugins/
cp -r hermes-example-plugins/strike-freedom-cockpit   ~/.hermes/plugins/

# enable any with a slash command surface
hermes plugins enable plugin-llm-example
hermes plugins enable plugin-llm-async-example
```

For dashboard plugins, restart the web UI (or `GET /api/dashboard/plugins/rescan`) to pick up the new tab. To uninstall, `rm -rf ~/.hermes/plugins/<name>` and the corresponding rescan / `hermes plugins disable`.

## Reading order for plugin authors

The plugins here are deliberately minimal — each one shows **one** plugin surface in the smallest amount of code that demonstrates it. Companion docs for each surface live in the main hermes-agent docs site under [Developer Guide → Extending](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing).

Pair each plugin in this repo with its docs page:

| Plugin here | Docs page |
|---|---|
| `plugin-llm-example` | [Plugin LLM Access](https://hermes-agent.nousresearch.com/docs/developer-guide/plugin-llm-access) |
| `plugin-llm-async-example` | [Plugin LLM Access](https://hermes-agent.nousresearch.com/docs/developer-guide/plugin-llm-access) |
| `example-dashboard` | [Extending the Dashboard](https://hermes-agent.nousresearch.com/docs/user-guide/features/extending-the-dashboard) |
| `strike-freedom-cockpit` | [Extending the Dashboard](https://hermes-agent.nousresearch.com/docs/user-guide/features/extending-the-dashboard) |

## Contributing a new example

Reference plugins should be:

- **Self-contained.** No deps beyond `hermes-agent` itself unless absolutely required.
- **Single-surface.** One plugin, one `ctx.*` API. If your example needs three `ctx.register_*` calls to make sense, it's probably not a reference example — it's a real plugin.
- **Under ~200 LOC of plugin code.** Reference plugins compete for attention with reading the docs page. Keep them small.
- **Production-shaped.** Use real types, real error handling, real audit logging — show plugin authors what we'd want them to write, not a stripped-down demo.

PRs welcome. Open an issue first if the surface you want to demonstrate isn't already covered in the hermes-agent developer-guide docs — we may want to write the docs page first, then add a companion reference plugin here.

## License

MIT, same as hermes-agent.

<!-- SAIFER_REPO_PASSPORT_BEGIN: #435 -->
## Паспорт

- **Что это:** Example plugins for hermes-agent — reference implementations and documentation companions, not bundled with the core repo..
- **Статус:** не знаю (работает / пауза / заморожено ❄️ / брошено — нет runtime-проверки).
- **Где работает:** не знаю (сервер/ПК/сайт/облако не подтверждены).
- **Как запустить или открыть:** [репозиторий](https://github.com/SaiferSMART/hermes-example-plugins); запуск приложения — не знаю (ищите инструкции в README).
- **Связанные открытые PR:** [актуальный список](https://github.com/SaiferSMART/hermes-example-plugins/pulls?q=is%3Apr+is%3Aopen).
- **Связанные открытые Issue:** [актуальный список](https://github.com/SaiferSMART/hermes-example-plugins/issues?q=is%3Aissue+is%3Aopen).
- **Дата последнего изменения GitHub:** 2026-05-10T13:49:38Z (поле `pushed_at`, любая ветка; не равно проверке эксплуатации).
- **Кто ведёт:** не знаю; владелец репозитория GitHub — `SaiferSMART`.
- **Вопрос к владелице:** подтвердить статус, площадку, точку входа и фактического ведущего.
- **Задание:** [Issue №435](https://github.com/SaiferSMART/saifer-ai-ops/issues/435).
<!-- SAIFER_REPO_PASSPORT_END -->
