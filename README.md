# SISW

**Self-Improving Software Workshop** — a gathering of people building things. Each speaker gives a short talk on what they're working on and what they've learned. Audience: other builders.

> **Date and venue:** TBA — submit anyway, organizers will follow up via your GitHub profile as we firm up the schedule.
>
> **Format:** ~10 minute talks, slides or live demo. **Organizer:** [@milstan](https://github.com/milstan).

[**→ Submit your talk**](https://github.com/milstan/sisw/issues/new?template=talk-submission.yml)

*Submissions open as a GitHub issue, get auto-converted into a PR, and appear in the table below once an organizer merges. One talk per speaker; gist URLs are welcome.*

---

## Who's coming

<!-- TALKS:START -->
| Speaker | Startup | Project / gist | What they're talking about |
|---|---|---|---|
| [Milan Stanisavljevic](https://github.com/milstan) (@milstan) | [leadbay.ai](https://leadbay.ai) | [milstan/3b12f938f344f4ae1f511dd19e56adce](https://gist.github.com/milstan/3b12f938f344f4ae1f511dd19e56adce) | Treat prompt authoring as a learning problem: feed in examples of desired output, and the LLM both analyses dimensions of quality and iteratively refines a candidate prompt against them, keeping the best-of-N. The key insight is that the model discovers what to optimise for — dimensions you wouldn't think to specify — and grounds evaluation in your examples instead of self-assessment. We've used this in production at Leadbay for writing-style learning and cold-start ICP descriptions; it replaces hand-written prompts with learned ones, no fine-tuning, no GPU. I'll walk through the protocol (analyse → generate → score → refine), share what surprised us (the anti-pattern list ended up being as load-bearing as the prompt itself), and compare it to few-shot, fine-tuning, and DSPy/OPRO. |
<!-- TALKS:END -->

This section is auto-regenerated from `_data/talks.yml` by `.github/workflows/submission-to-pr.yml` on each merge — don't edit between the markers by hand.

---

## How a submission flows

```
Visitor clicks "Submit your talk"  on github.com/milstan/sisw
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
The README rebuilds → new row appears in the "Who's coming" table above.
```

If validation fails, the bot comments on the issue listing what needs fixing and labels it `needs-fixes`. Submitter closes and reopens with corrections.

**One talk per speaker.** A second submission by the same GitHub user is detected and rejected at the issue stage — no PR is created, the issue is labeled `duplicate-submission`, and the bot comments with a link to the speaker's existing submission. The dedup check looks in three places, in priority order:

1. an entry in `_data/talks.yml` whose `submitter_github` matches (an approved talk),
2. another open issue with the `talk-submission` label by the same GitHub user (a pending submission),
3. an open PR with the `talk-submission` label whose body credits the same `@author` (a pending review).

**Gist URLs are accepted.** The "GitHub repo to share" field accepts both `https://github.com/<user>/<repo>` and `https://gist.github.com/<user>/<id>`. Gists render as `<user>/<id>` in the table.

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

  The PR auto-updates; click Merge. The README's "Who's coming" block is regenerated automatically.
- **Duplicate label remediation:** if the bot incorrectly flagged a submission as duplicate, remove the `duplicate-submission` label, ask the submitter to close + reopen with the corrected fields. The workflow runs on `opened` events only, so re-applying the label or re-editing won't re-trigger.

## One-time setup after creating the repo

1. **Settings → Actions → General → Workflow permissions:** select *Read and write permissions*, and tick *Allow GitHub Actions to create and approve pull requests*. (This is what lets the workflow open the PR.)
2. (Optional) **Settings → Pages:** enable to serve a redirect at `<user>.github.io/<repo>/` that points back to this README. The canonical homepage is the README itself, viewed at https://github.com/milstan/sisw.

No tokens, no secrets, no other config.

## File map

| Path | What it does |
|---|---|
| `README.md` | The homepage. Renders natively on github.com. The "Who's coming" block between `<!-- TALKS:START -->` and `<!-- TALKS:END -->` is auto-regenerated from `_data/talks.yml` on each merge. |
| `_data/talks.yml` | Source of truth for approved talks. Append-only via merged PRs. |
| `index.md` | Tiny redirect page for the optional GitHub Pages site at `<user>.github.io/<repo>/`. |
| `_config.yml` | Jekyll config (only relevant if Pages is enabled). |
| `.github/ISSUE_TEMPLATE/talk-submission.yml` | The submission form fields. |
| `.github/ISSUE_TEMPLATE/config.yml` | Disables blank issues so people use the form. |
| `.github/workflows/submission-to-pr.yml` | Issue → validate → dedup → append-to-yml + regenerate-README → PR. |

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
