# OpenClaw in Docker (Beginner-Friendly)

This guide helps you run OpenClaw quickly and safely with Docker.

## 0) Quick Environment Check

Before You Start, make sure your machine has:

* [Docker installed](https://docs.docker.com/get-started/introduction/get-docker-desktop/)
* Bash v4+ (For example, MacOS with bash v3 only, you need upgrade with command
```
brew install bash
```
## 1) Clone this repository (HTTPS)

Use HTTPS so you don’t need to configure SSH or `git://`.

```bash
git clone https://github.com/ozbillwang/openclaw-in-docker.git
cd openclaw-in-docker
```

## 2) Set the OpenClaw Docker image

Default:

```bash
export OPENCLAW_IMAGE="alpine/openclaw:main"
```

> Note: `main` is the setup script default because it currently avoids issues
> some users have seen with `latest`.
> If you prefer the release tag, switch to:

```bash
export OPENCLAW_IMAGE="alpine/openclaw:latest"
```

## 3) Run the setup script

```bash
./docker-setup.sh
```

This script will:

* pull openclaw gateway image
* Create baseline OpenClaw config non-interactively
* Start the gateway via Docker Compose
* Generate a gateway token and store it in .env

After the gateway is running, you can run the interactive onboarding wizard:

```bash
docker compose run --rm openclaw-cli onboard --no-install-daemon
```
---

### 4) Upgrade OpenClaw
When a new version is released, pull the latest image and restart the service:
```
docker pull alpine/openclaw:latest
docker-compose down
docker-compose up -d
```
No worried, the configuration file ( `~/.openclaw/openclaw.json`) will not be affected. However, it’s good practice to back it up and store it in a safe location before upgrading.

## Onboarding screenshots (for beginners)

You can use the onboarding screenshots from this blog post:

- [Run OpenClaw (MoltBot, ClawdBot) Safely with Docker: A Practical Guide for Beginners](https://medium.com/p/94112a9b57be)
- [Running OpenClaw with a Local LLM on a Mac mini (No API Cost)](https://medium.com/p/fb3857f73e0b)

---

## Quick troubleshooting

- If startup fails with `latest`, switch to `main` and rerun setup.
- Make sure Docker is running before executing `./docker-setup.sh`.
- Re-run the script after changing `OPENCLAW_IMAGE`.
- Reguarly backup `~/.openclaw/openclaw.json` on your host server, before upgrade or re-install
