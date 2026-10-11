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
- The workflow installs the newest `pulsecheckcli` 0.x on every run. To pin one version, edit `PULSECHECK:` in `.github/workflows/monitor.yml`.
- How this setup works: [Scheduling → GitHub Actions](https://github.com/arian24b/pulsecheck/wiki/Scheduling). Every setting: [YAML reference](https://github.com/arian24b/pulsecheck/wiki/YAML-Reference). Other alert services: [Notifications](https://github.com/arian24b/pulsecheck/wiki/Notifications). Persian docs: [فارسی](https://github.com/arian24b/pulsecheck/wiki/FA-Home). Vercel, Cloudflare or cron instead of Actions: the [main project](https://github.com/arian24b/pulsecheck).
