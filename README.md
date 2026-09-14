# ZapchastTOP

Telegram bot for finding car spare parts by city, with self-service seller listings.

Buyers search their region ("hudud") for a part by keyword; the bot returns the closest-matching parts across active shops, grouped one-per-shop, with contact info and a map link. Sellers register their own shop from the bot, get an auth token, and manage their part listings (add/edit/delete) without needing the admin panel.

**Bot:** https://t.me/zapchastop1_bot

## Stack

- **Backend:** FastAPI + SQLAlchemy + PostgreSQL (`pg_trgm` for fuzzy search), with a [sqladmin](https://github.com/aminalaee/sqladmin) panel for managing cities, shops, parts and feedback
- **Bot:** Aiogram 3, fully inline-keyboard driven (no reply-keyboard clutter, except where Telegram requires it for contact/location sharing)
- **Deployment:** Docker Compose (`db`, `backend`, `bot`)

## Features

- Fuzzy + prefix search across car model and part name, with typo tolerance and Cyrillic/Latin transliteration
- Region hierarchy seeded from [univeluz/opendb](https://github.com/univeluz/opendb) — all 14 regions of Uzbekistan with districts and settlements, toggleable via the admin panel
- Seller self-registration (phone + location + shop details) with a UUID token gating their own listings
- Telegram inline search (`@zapchastop1_bot <query>`) for instant results in any chat
- Admin feedback notifications, shop moderation (pending → active)

## Running locally

```bash
cp .env.example .env   # fill in BOT_TOKEN, admin creds, etc.
docker compose up -d --build
```

Backend: `http://localhost:8010` · Admin panel: `http://localhost:8010/admin`
