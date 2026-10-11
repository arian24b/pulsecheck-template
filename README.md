# My uptime monitor

Checks my sites every 5 minutes with [pulsecheck](https://github.com/arian24b/pulsecheck) and sends an alert when one goes down, recovers, gets slow or its certificate is about to expire. It runs on GitHub Actions: no server, no dashboard.

## Set up (3 steps)
1. **Edit `pulsecheck.yml`**: put your sites under `sites:`.
2. **Add the alert secrets**: *Settings → Secrets and variables → Actions → New repository secret*. The sample uses Telegram (`TG_TOKEN` from @BotFather, `TG_CHAT` the chat or `@channel`). Every `${NAME}` in the file needs a secret called `NAME`; list new ones under `env:` in `.github/workflows/monitor.yml`.
3. **Run it once**: *Actions → monitor → Run workflow*. Each run shows the current state of every site in its summary.

Keep this repository **private**: `pulsecheck.yml` lists your hostnames.

## Good to know
- State is kept between runs with the Actions cache; nothing is committed.
- GitHub pauses scheduled workflows after 60 days without repository activity (re-enable in the Actions tab).
- All settings, other alert services, running it on Vercel/Cloudflare or cron: [the wiki](https://github.com/arian24b/pulsecheck/wiki).
