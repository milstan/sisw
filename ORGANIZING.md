# Organizing SISW

Internal notes for organizers. The public homepage is [README.md](README.md); this file documents the GitHub-native submission/approval flow that powers it.

## How a submission flows

```
Visitor clicks "Submit your talk" on github.com/milstan/sisw
        │
        ▼
Issue Form opens on github.com/milstan/sisw  (submitter needs a GitHub account)
        │
        ▼
GitHub Action `submission-to-pr` runs:
   • parses the issue form fields
   • validates the repo URL (optional) and summary length (≤600 chars)
   • dedups against approved talks + open issues + open PRs
   • appends an entry to _data/talks.yml on a new branch `talk/<issue#>`
   • opens a PR titled "Talk submission: <name>"
        │
        ▼
Organizer reviews PR. Merge = approval.
        │
        ▼
README rebuilds (the "Who's coming" block) → new row appears in the table.
        │
        ▼
GitHub Action `post-merge-rsvp` posts a comment on the originating issue
with the Luma RSVP link, capturing email via Luma's RSVP form.
```

If validation fails, the bot comments on the issue listing what needs fixing and labels it `needs-fixes`. Submitter closes and reopens with corrections.

## Submission contract details

**One talk per speaker.** A second submission by the same GitHub user is detected and rejected at the issue stage — no PR is created, the issue is labeled `duplicate-submission`, and the bot comments with a link to the speaker's existing submission. The dedup check looks in three places, in priority order:

1. an entry in `_data/talks.yml` whose `submitter_github` matches (an approved talk),
2. another open issue with the `talk-submission` label by the same GitHub user (a pending submission),
3. an open PR with the `talk-submission` label whose body credits the same `@author` (a pending review).

**Repo URL is optional.** The "GitHub repo or gist to share" field accepts both `https://github.com/<user>/<repo>` and `https://gist.github.com/<user>/<id>`. The table shows a 🔗 icon linking to the repo/gist; rows without one omit the icon.

**Twitter/X handle is optional.** Speakers can paste a handle (with or without `@`) or a full `x.com/...` / `twitter.com/...` URL. Workflow normalizes to just the handle and validates against Twitter's actual rule (1-15 alphanumeric or underscore). When set, the speaker cell renders a `𝕏` icon linked to `x.com/<handle>`.

**Summary length cap.** Talk summaries are capped at 600 characters at submission time. The homepage table shows the first sentence (up to ~320 chars) with a clickable `[…]` linking back to the originating issue for the full text.

## Email-via-RSVP

We don't ask for email anywhere in the form. Instead, the post-merge workflow posts a comment on the originating issue with a Luma event RSVP link. Speakers RSVP-ing on Luma share their email with the organizer (standard Luma attendee-list behavior).

To configure or change the RSVP link:

1. Find the **public** Luma event URL (looks like `https://lu.ma/<slug>` or `https://luma.com/<slug>` — *not* the `/event/manage/...` URL, which is admin-only).
2. github.com/milstan/sisw → **Settings → Secrets and variables → Actions → Variables → New repository variable**: name `SISW_EVENT_URL`, value the URL.
3. Done. Future merged PRs include that link in the post-merge comment. Until the variable is set, the workflow falls back to the URL hardcoded in `.github/workflows/post-merge-rsvp.yml`.

## Approving / rejecting submissions

- **Approve:** open the PR, give it a quick read, click Merge. Done. The README's "Who's coming" block regenerates automatically; the post-merge workflow posts the RSVP comment on the originating issue.
- **Reject:** close the PR with a comment. Optionally close the originating issue too.
- **Edit before approving** (worked example): say the speaker typo'd `leadbay.io` → should be `leadbay.ai`. Click the "Files changed" tab on the PR; or pull the branch locally:

  ```bash
  git fetch origin
  git checkout talk/12        # the PR branch — same number as the issue
  sed -i '' 's|leadbay\.io|leadbay.ai|' _data/talks.yml
  git commit -am "Fix speaker domain typo" && git push
  ```

  The PR auto-updates; click Merge. The README's "Who's coming" block is regenerated automatically.
- **Duplicate label remediation:** if the bot incorrectly flagged a submission as duplicate, remove the `duplicate-submission` label, ask the submitter to close + reopen with the corrected fields. The workflow runs on `opened` events only, so re-applying the label or re-editing won't re-trigger.

## One-time setup after creating the repo

1. **Settings → Actions → General → Workflow permissions:** select *Read and write permissions*, and tick *Allow GitHub Actions to create and approve pull requests*. (This is what lets the workflow open the PR.)
2. **Settings → Secrets and variables → Actions → Variables:** add `SISW_EVENT_URL` with your Luma public event URL (see "Email-via-RSVP" above).
3. (Optional) **Settings → Pages:** enable to serve a redirect at `<user>.github.io/<repo>/` that points back to this README. The canonical homepage is the README itself, viewed at https://github.com/milstan/sisw.

No tokens, no secrets, no other config.

## File map

| Path | What it does |
|---|---|
| `README.md` | Public homepage. Renders natively on github.com. The "Who's coming" block between `<!-- TALKS:START -->` and `<!-- TALKS:END -->` is auto-regenerated from `_data/talks.yml` on each merge. |
| `_data/talks.yml` | Source of truth for approved talks. Append-only via merged PRs. |
| `index.html` | Tiny redirect for the optional GitHub Pages site at `<user>.github.io/<repo>/`. |
| `_config.yml` | Jekyll config (only relevant if Pages is enabled). |
| `.github/ISSUE_TEMPLATE/talk-submission.yml` | The submission form fields. |
| `.github/ISSUE_TEMPLATE/config.yml` | Disables blank issues so people use the form. |
| `.github/workflows/submission-to-pr.yml` | Issue → validate → dedup → append-to-yml + regenerate-README → PR. |
| `.github/workflows/post-merge-rsvp.yml` | Fires when a `talk-submission` PR is merged; posts an "approved + RSVP here" comment on the originating issue. RSVP link comes from repo variable `SISW_EVENT_URL`. |
| `ORGANIZING.md` | This file. |

## What `_data/talks.yml` looks like

Each merged PR appends one entry; this is the public data contract:

```yaml
- first: Milan
  last: Stankovic
  domain: leadbay.ai
  repo: https://gist.github.com/milstan/3b12f938f344f4ae1f511dd19e56adce
  twitter: milstan                   # X/Twitter handle, optional, no @ prefix
  summary: Treat prompt authoring as a learning problem...
  submitter_github: milstan          # used by the dedup check
  submitted_at: '2026-05-05T19:28:47Z'
  issue: 1                           # links back to the originating issue
```

The file is human-readable and unicode-safe (`yaml.safe_dump(..., allow_unicode=True)`); it can be hand-edited by an organizer to fix a typo, but new entries should always come through a merged PR so the audit trail (issue → PR → merge) stays intact.

## Contacting submitters

The form doesn't ask for an email. Submitters need a GitHub account to file the issue, so organizers can reach them via `@username` on the issue/PR or through their GitHub profile until they RSVP on Luma. Less PII collected, less to worry about.
