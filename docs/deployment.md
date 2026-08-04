# Deployment Guide

## 1. Create the special profile repository

GitHub renders a repository's README on your profile page only if the repository is named **exactly** your username and is public.

```bash
# Repository name must equal your GitHub username
Skc-VitInProjects/Skc-VitInProjects
```

If it doesn't exist yet, create it at `github.com/new` with that exact name, public visibility, and no template.

## 2. Push this repository

```bash
git init
git remote add origin https://github.com/Skc-VitInProjects/Skc-VitInProjects.git
git add .
git commit -m "Initial profile: dashboard-style README"
git branch -M main
git push -u origin main
```

## 3. Enable the automated workflows

The three workflows in `.github/workflows/` need repo permissions to commit back to `main`:

1. Go to **Settings → Actions → General → Workflow permissions**.
2. Select **Read and write permissions**.
3. Save.

| Workflow | What it does | Schedule |
|---|---|---|
| `snake.yml` | Regenerates the contribution snake animation SVG | Daily, 00:00 UTC |
| `metrics.yml` | Refreshes any cached metrics/badges | Daily, 03:00 UTC |
| `waka.yml` | Updates coding-time stats if WakaTime is connected | Daily, 06:00 UTC |

`waka.yml` requires a `WAKATIME_API_KEY` secret (**Settings → Secrets and variables → Actions**) if you connect WakaTime; it's safe to disable that workflow otherwise.

## 4. Verify rendering

Open `github.com/Skc-VitInProjects` after the push completes. GitHub caches README renders briefly — a hard refresh clears most display issues. Confirm:

- [ ] Banner SVG loads (not a broken image icon)
- [ ] Typing animation plays
- [ ] All internal nav anchors (`#about`, `#featured-projects`, etc.) scroll correctly
- [ ] Stats cards show real data (they need a few minutes after first push)

## 5. Keep it current

Re-run the merge in `docs/customization.md` any time you edit a `sections/*.md` file, so `README.md` never drifts out of sync with its sources.
