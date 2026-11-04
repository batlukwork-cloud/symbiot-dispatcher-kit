# HARNESS_ADAPTERS — AI-агент «Управление системой Симбиота»

Как агент встроен в Hermes Agent (актуально на 2026-08-08).

## Рантайм

| Параметр | Значение |
|---|---|
| Профиль | `dispatcher` |
| Папка профиля | `<рабочая папка> PC\AppData\Local\<профиль>` |
| SOUL.md | там же (главная инструкция поведения) |
| .env | там же: TELEGRAM_BOT_TOKEN, TELEGRAM_HOME_CHANNEL=<chat_id>, TELEGRAM_ALLOWED_USERS=<chat_id> |
| config.yaml | там же: модель deepseek-v4-pro (provider deepseek, base_url https://api.deepseek.com/v1, api_mode chat_completions); экономия: context_length=65536, max_turns=50, compression.threshold=0.35, protect_last_n=10; session_reset.notify=false, tool_progress="off" |

## Запуск

```bash
hermes --profile dispatcher gateway run --replace --accept-hooks   # запуск (background)
hermes --profile dispatcher gateway status                          # статус
```

Автозапуск (опционально): `hermes --profile dispatcher gateway install`.

## Каналы

личка владелец продукта <chat_id>

## Проверка подключения

```bash
hermes --profile dispatcher gateway status
# лог: profiles/dispatcher/logs/gateway.log — "Connected to Telegram (polling mode)"
```

## Адаптеры в другие harness

1. **Hermes gateway** (основной): профиль + SOUL.md + скиллы — текущий вариант.
2. **Codex/CLI**: загрузить SOUL.md как системный промпт + UNIVERSAL_SKILL.md.
3. **LangGraph/n8n**: использовать 06_RUNTIME_CONTRACTS/AGENT_MANIFEST.json как контракт узла.
4. **Ручной процесс**: читать каркас папки агента.
