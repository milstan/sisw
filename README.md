# SISW

**Live site:** <https://milstan.github.io/sisw/>

Public event page + submission flow. 100% on GitHub — no servers, no databases, no third-party services.

## How a submission flows

```
Visitor clicks "Submit your talk"  on milstan.github.io/sisw
        │
        ▼
Issue Form opens on github.com/milstan/sisw  (submitter needs a GitHub account)
        │
        ▼
GitHub Action `submission-to-pr` runs:
   • parses the issue form fields
   • validates the repo URL
   • appends an entry to _data/talks.yml on a new branch `talk/<issue#>`
   • opens a PR titled "Talk submission: <name>"
        │
        ▼
Organizer reviews PR. **Merge = approval.**
        │
        ▼
GitHub Pages rebuilds → new row appears in the "Who's coming" table.
```

If validation fails, the bot comments on the issue listing what needs fixing and labels it `needs-fixes`. Submitter closes and reopens with corrections.

**One talk per speaker.** A second submission by the same GitHub user is detected and rejected at the issue stage — no PR is created, the issue is labeled `duplicate-submission`, and the bot comments with a link to the speaker's existing submission. The dedup check looks in three places, in priority order:

1. an entry in `_data/talks.yml` whose `submitter_github` matches (an approved talk),
2. another open issue with the `talk-submission` label by the same GitHub user (a pending submission),
3. an open PR with the `talk-submission` label whose body credits the same `@author` (a pending review).

**Gist URLs are accepted.** The "GitHub repo to share" field accepts both `https://github.com/<user>/<repo>` and `https://gist.github.com/<user>/<id>`. Gists render as `<user>/<id>` in the table.

## One-time setup after pushing this repo

1. **Create the repo at https://github.com/milstan/sisw** and push these files to `main`.
2. **Settings → Pages → Build and deployment → Source:** *Deploy from a branch*, branch `main`, folder `/ (root)`. Save.
3. **Settings → Actions → General → Workflow permissions:** select *Read and write permissions*, and tick *Allow GitHub Actions to create and approve pull requests*. (This is what lets the workflow open the PR.)
4. Wait ~30s for the first Pages build. Site goes live at **https://milstan.github.io/sisw/**.

That's it. No tokens, no secrets, no other config.

## Local preview

```bash
bundle install
bundle exec jekyll serve
# open http://localhost:4000
```

## Approving / rejecting submissions

- **Approve:** open the PR, give it a quick read, click Merge. Done.
- **Reject:** close the PR with a comment. Optionally close the originating issue too.
- **Edit before approving** (worked example): say the speaker typo'd `leadbay.io` → should be `leadbay.ai`. Click the "Files changed" tab on the PR; or pull the branch locally:

  ```bash
  git fetch origin
  git checkout talk/12        # the PR branch — same number as the issue
  sed -i '' 's|leadbay\.io|leadbay.ai|' _data/talks.yml
  git commit -am "Fix speaker domain typo" && git push
  ```

  The PR auto-updates; click Merge. Pages rebuilds within ~60s.
- **Duplicate label remediation:** if the bot incorrectly flagged a submission as duplicate, remove the `duplicate-submission` label, ask the submitter to close + reopen with the corrected fields. The workflow runs on `opened` events only, so re-applying the label or re-editing won't re-trigger.

## File map

| Path | What it does |
|---|---|
| `index.md` | Homepage. Renders the "Who's coming" table from `_data/talks.yml`. |
| `_data/talks.yml` | Source of truth for approved talks. Append-only via merged PRs. |
| `_config.yml` | Jekyll config + theme (`jekyll-theme-minimal`). |
| `.github/ISSUE_TEMPLATE/talk-submission.yml` | The submission form fields. |
| `.github/ISSUE_TEMPLATE/config.yml` | Disables blank issues so people use the form. |
| `.github/workflows/submission-to-pr.yml` | Issue → validate → dedup → append → PR. |

## What `_data/talks.yml` looks like

Each merged PR appends one entry; this is the public data contract:

```yaml
- first: Milan
  last: Stanisavljevic
  domain: leadbay.ai
  repo: https://gist.github.com/milstan/3b12f938f344f4ae1f511dd19e56adce
  summary: Treat prompt authoring as a learning problem...
  submitter_github: milstan         # used by the dedup check
  submitted_at: '2026-05-05T19:28:47Z'
  issue: 1                           # links back to the originating issue
```

The file is human-readable and unicode-safe (`yaml.safe_dump(..., allow_unicode=True)`); it can be hand-edited by an organizer to fix a typo, but new entries should always come through a merged PR so the audit trail (issue → PR → merge) stays intact.

## Contacting submitters

The form doesn't ask for an email. Since submitters need a GitHub account to file the issue, organizers can reach them via `@username` on the issue/PR or through their GitHub profile. Less PII collected, less to worry about.
