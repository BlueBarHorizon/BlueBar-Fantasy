# BlueBar Fantasy

## What this is

A paid monthly UFC fantasy league. Members pay a subscription through Whop, submit fight picks, and compete on a public leaderboard. This repo is the member facing website for that league.

Live at: https://bluebarhorizon.github.io/BlueBar-Fantasy

The league is part of BlueBar Horizon, a UFC commentary and content brand running on TikTok, Instagram, YouTube, and a paid Discord community.

## Stack

- Plain HTML, CSS, and vanilla JavaScript. No build step, no framework, no package manager.
- Hosted on GitHub Pages, published from the `main` branch.
- Data lives in Google Sheets and is read by the site through the Sheets API.
- Pick submission runs through a form on the site.
- Membership status is verified against Whop.

Do not introduce React, a bundler, or a package manager without asking first. Anything committed to `main` is live on the public site within a minute.

## How the data flows

Google Sheets is the source of truth for standings, picks, and scoring. The site reads from it. The site does not write to it. If a change would require writing back to Sheets, stop and ask before building it.

## Scoring rules

Each member gets a budget of 10 picks per month. Points are awarded on a tiered system based on the fighter's betting odds, so picking favourites pays less than picking underdogs.

| Odds | Win | Finish |
| --- | --- | --- |
| -200 or longer | 0.5 | 1 |
| -199 to -101 | 1 | 2 |
| +100 to +250 | 2 | 4 |
| +251 or higher | 4 | 8 |

Additional bonuses apply for finishes and for strike and takedown volume.

**Scoring logic is business critical.** Never modify, refactor, or "clean up" scoring calculations, the Sheets integration, or the Whop verification flow without explicitly asking first and explaining what would change. A scoring error costs real money and member trust.

## Audience and priorities

Members are casual to serious UFC fans, mostly checking standings on a phone during or right after a fight card. Mobile experience matters more than desktop. Traffic spikes hard on Saturday nights.

Priority order when making design or build decisions:

1. Mobile usability
2. Load speed and clarity of standings
3. Accessibility (contrast, touch targets, keyboard navigation)
4. Visual polish

The benchmark for quality is a mainstream sports product like ESPN or Yahoo Fantasy, adapted to a small independent league.

## Design system

If `design-system/` exists in this repo, read `MASTER.md` inside it before making any visual change and follow the colours, typography, and spacing defined there. Page specific overrides in `design-system/*/pages/` take precedence over MASTER for that page. Do not invent new colours or fonts outside that system.

## Rules of engagement

- Site code changes go on a branch and open a pull request. Do not commit site code directly to `main`.
- Configuration and documentation (`.claude/`, `design-system/`, this file) can go straight to `main`.
- Never commit API keys, Sheets credentials, Whop tokens, or any other secret. If you find one already in the repo, stop and flag it immediately rather than moving it.
- Prefer small, contained changes over sweeping rewrites.
- For anything larger than a single component, propose a plan and wait for approval before writing code.
- Keep the site dependency free. If a task seems to need a library, say so and explain why before adding one.

## Writing style

Any user facing copy on the site should avoid em dashes and hyphens used as connectors.
