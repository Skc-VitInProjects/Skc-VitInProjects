# Customization Guide

## How this repository is organized

- `README.md` is the file GitHub actually renders on your profile (`github.com/<username>/<username>`). It is a **full merge** of every file in `sections/`, in display order.
- `sections/*.md` are the maintainable source pieces — edit these, not just README.md, so the two don't drift apart.
- `assets/*.svg` are hand-authored, dependency-free SVG graphics referenced by the sections.

## Editing a section

1. Edit the relevant file in `sections/`.
2. Re-run the merge (see below) or manually copy your change into the matching block of `README.md`.
3. Commit both the section file and the regenerated `README.md`.

## Regenerating README.md from sections/

From the repository root:

```bash
{
  cat sections/hero.md;          echo -e "\n<br/>\n"
  cat sections/about.md;         echo -e "\n<br/>\n"
  cat sections/dashboard.md;     echo -e "\n<br/>\n"
  cat sections/inventory.md;     echo -e "\n<br/>\n"
  cat sections/projects.md;      echo -e "\n<br/>\n"
  cat sections/experience.md;    echo -e "\n<br/>\n"
  cat sections/achievements.md;  echo -e "\n<br/>\n"
  cat sections/stats.md;         echo -e "\n<br/>\n"
  cat sections/roadmap.md;       echo -e "\n<br/>\n"
  cat sections/learning.md;      echo -e "\n<br/>\n"
  cat sections/coding-profiles.md; echo -e "\n<br/>\n"
  cat sections/opensource.md;    echo -e "\n<br/>\n"
  cat sections/socials.md;       echo -e "\n"
  cat sections/footer.md
} > README.md
```

## Swapping the color palette

Every SVG uses the same three gradient stops. To retheme, find-and-replace these hex values across `assets/*.svg`:

| Role | Hex |
|---|---|
| Cyan accent | `#00E5FF` |
| Blue accent | `#4C6FFF` |
| Purple accent | `#B24BF3` |
| Background void | `#060A14` |
| Panel background | `#0D1424` / `#0A1020` |
| Primary text | `#E7ECFB` |
| Dim/secondary text | `#8DA0C4` / `#5C6B8A` |

## Updating stats

`sections/stats.md` uses the third-party services `github-readme-stats`, `github-readme-streak-stats`, and `github-readme-activity-graph`, all driven off the `Skc-VitInProjects` username in the URL — no manual numbers to update. See `docs/badges.md` for how to point these at a different account.
