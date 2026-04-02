# Vibers — Code Review for Vibecoded Projects

Human-in-the-loop code review for teams using cheap AI-assisted developers. We review commits against your spec, fix issues, and send pull requests.

## Quick Start

### 1. Add marsiandeployer to your repo

Go to **Settings → Collaborators → Add people** → `marsiandeployer`

### 2. Add the GitHub Action

Create `.github/workflows/vibers.yml`:

```yaml
name: Vibers Code Review
on:
  push:
    branches: [main]
  pull_request:

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 2
      - uses: marsiandeployer/vibers-action@v1.1
        with:
          spec_url: 'https://docs.google.com/document/d/YOUR_SPEC_ID/edit'
          telegram_contact: '@your_telegram'
```

### 3. Get reviews

Every push with a **"How to test"** section in the commit message triggers a review request. `marsiandeployer` reviews your commits against your spec and submits PRs with fixes.

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `spec_url` | No | `''` | URL to your spec (Google Doc, Notion, etc.) |
| `review_scope` | No | `full` | `full`, `security`, or `spec-compliance` |
| `telegram_contact` | No | `''` | Your Telegram for review delivery |
| `vibers_api_key` | No | `''` | API key from vibers.onout.org (unlocks priority queue) |

## When Reviews Trigger

The action only fires when the commit message contains **"How to test"** — so routine pushes don't generate review requests. Include a "How to test" section in commits where you actually want a human to check the result.

## How It Works

1. Action collects changed files, commit context, and CI run URL
2. Submits review request to Vibers
3. `marsiandeployer` reviews code against your spec
4. You get a PR with fixes (not just comments)

## Pricing

- **Free** (promo — GitHub ⭐ + feedback in return)
- **$15/hour** (standard — priority turnaround)

Pay as you go. No subscriptions. No minimums.

## Links

- [Landing page](https://vibers.onout.org)
- [Full docs & SKILL.md](https://github.com/marsiandeployer/human-in-the-loop-review)
- [Telegram](https://t.me/onoutnoxon)

## Changelog

### v1.1
- Added `vibers_api_key` input (priority queue)
- CI run URL now included in review payload
- Clarified "How to test" trigger requirement in docs

### v1.0
- Initial release
