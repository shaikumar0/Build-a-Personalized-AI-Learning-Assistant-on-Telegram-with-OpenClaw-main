# Build a Personalized AI Learning Assistant on Telegram with OpenClaw

This repository contains the required submission for the OpenClaw project: a Telegram-based personalized learning assistant that onboards users and sends a nightly tech brief.

Contents

- `skills/user-onboarding/SKILL.md` — Onboarding skill (required)
- `skills/daily-quiz/SKILL.md` — Daily quiz generation skill (required)
- `openclaw.json.example` — Example OpenClaw configuration snippet (no secrets)
- `Dockerfile` — Container image for running OpenClaw gateway
- `docker-compose.yml` — Compose startup for OpenClaw and optional services
- `.env.example` — Example environment variables

Quick Start (local)

1. Install prerequisites: Node.js (LTS), Docker (optional), and, optionally, Ollama for a local model.
2. Copy `.env.example` to `.env` and fill in `TELEGRAM_BOT_TOKEN` and `MODEL` or `OLLAMA_URL`.
3. If using Docker:

```powershell
docker-compose up --build
```

4. Or run locally after installing `openclaw` globally:

```powershell
npm i -g openclaw
# Copy skills into ~/.openclaw/skills or set OPENCLAW_HOME
openclaw gateway start
```

openclaw.json configuration (example)

See [openclaw.json.example](openclaw.json.example) for a minimal plugin configuration that references environment variables and does not contain secrets.

Onboarding trigger choice

- This submission uses an OpenClaw Standing Order to trigger onboarding automatically when a user has no `user_profile_{{user.id}}` in memory. This is simple to implement and robust for Telegram channel integrations.
- Alternative: use a webhook/standing-order hybrid if you prefer event-driven triggers.

Submission checklist

- `skills/user-onboarding/SKILL.md` — present
- `skills/daily-quiz/SKILL.md` — present
- `openclaw.json.example` — present
- `Dockerfile`, `docker-compose.yml`, `.env.example` — present
- `README.md` — present

Notes

- Do NOT commit real secrets. Use environment variables or the OpenClaw `.env` mechanism.
- If you choose a cloud model provider, set the provider credentials in a secure secrets store and reference them in `openclaw.json` via `${env.VAR}`.
