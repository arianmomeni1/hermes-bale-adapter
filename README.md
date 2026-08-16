# Hermes Bale Adapter

Plugin platform adapter that connects **Hermes Agent** to [Bale](https://bale.ai) (بله), the Persian messenger, via its Telegram-compatible Bot API.

## Features

- ⚡ Long-polling over `httpx` — no webhook needed
- 💬 Text messages, Markdown parse mode
- 👥 Group and private chat support
- 🔁 Exponential backoff reconnection
- 🧹 Own-message echo suppression
- ⏱ Typing indicator (`sendChatAction`)
- 📦 Cron / notification delivery to a home channel (`BALE_HOME_CHANNEL`)
- 🔐 Allowed-users list (`BALE_ALLOWED_USERS`)

## Requirements

- Python 3.10+
- `httpx`

## Installation (Hermes plugin)

Copy the `plugins/platforms/bale/` directory into your Hermes plugins folder:

```bash
mkdir -p ~/.hermes/plugins/platforms
cp -r bale ~/.hermes/plugins/platforms/
pip install httpx
```

Add to your `~/.hermes/.env`:

```env
BALE_BOT_TOKEN=123456:your-bot-token-from-@bale_robot
BALE_ALLOWED_USERS=1861136268           # optional
BALE_HOME_CHANNEL=-1001234567890        # optional, for cron delivery
```

Then reload:

```bash
hermes plugins reload
hermes gateway run
```

## API

| Method | Purpose |
|---|---|
| `getMe` | Validate token & bot identity on connect |
| `getUpdates` | Long-poll incoming messages |
| `sendMessage` | Send text (Markdown) |
| `sendChatAction` | Typing indicator |

Base URL: `https://tapi.bale.ai/bot<token>/...` — a fork of Telegram's Bot API, so the data structures are nearly identical.

## Files

- `adapter.py` — the full `BaleAdapter` implementation (355 lines)
- `plugin.yaml` — plugin manifest (name, env vars, metadata)
- `__init__.py` — re-exports `register`

## License

MIT — see [LICENSE](LICENSE).
