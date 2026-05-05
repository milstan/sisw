# SISW

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

**One talk per speaker.** A second submission by the same GitHub user is detected and rejected at the issue stage — no PR is created, the issue is labeled `duplicate-submission`, and the bot comments with a link to the speaker's existing submission (whether it's already in `_data/talks.yml`, an open issue still pending review, or an open PR awaiting merge).

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
- **Edit before approving:** push commits to the `talk/<issue#>` branch (e.g. fix a typo in the summary), then merge. Pages rebuilds automatically on merge to `main`.
- **Duplicate label:** if the bot mistakenly flagged a submission as a duplicate, remove the `duplicate-submission` label and re-trigger the workflow by editing then re-saving the issue, or simply ask the submitter to close + reopen with the correction.

## File map

| Path | What it does |
|---|---|
| `index.md` | Homepage. Renders the "Who's coming" table from `_data/talks.yml`. |
| `_data/talks.yml` | Source of truth for approved talks. Append-only via merged PRs. |
| `_config.yml` | Jekyll config + theme (`jekyll-theme-minimal`). |
| `.github/ISSUE_TEMPLATE/talk-submission.yml` | The submission form fields. |
| `.github/ISSUE_TEMPLATE/config.yml` | Disables blank issues so people use the form. |
| `.github/workflows/submission-to-pr.yml` | Issue → validate → dedup → append → PR. |

## Contacting submitters

The form doesn't ask for an email. Since submitters need a GitHub account to file the issue, organizers can reach them via `@username` on the issue/PR or through their GitHub profile. Less PII collected, less to worry about.
